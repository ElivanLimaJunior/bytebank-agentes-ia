# Princípios éticos e conformidade — Agentes de IA do Bytebank

> **Documento fundacional da governança do projeto.** Define como o Bytebank vai construir e operar seu ecossistema de agentes de IA para atendimento digital (RAG sobre políticas internas e arquitetura multiagente) de forma ética, auditável e em conformidade com a LGPD.
>
> **Escopo:** chatbot de atendimento ao cliente e agentes especializados (conta corrente, cartão de crédito, suporte).
> **Responsáveis:** DPO (conformidade), Engenharia de IA (implementação), MLOps/LLMOps (operação). Ver [time_de_ia.csv](time_de_ia.csv).

## Sumário
- [(a) Princípios éticos aplicáveis](#a-princípios-éticos-aplicáveis)
- [(b) Tratamento de alucinações de LLMs](#b-tratamento-de-alucinações-de-llms)
- [(c) Os quatro pilares do LLM Ops no contexto bancário](#c-os-quatro-pilares-do-llm-ops-no-contexto-bancário)
- [Como este documento é mantido](#como-este-documento-é-mantido)

---

## (a) Princípios éticos aplicáveis

Cada princípio vem com **o que significa**, **como se aplica ao Bytebank** e **como verificamos** (um princípio sem verificação é só uma intenção).

### 1. Privacidade e LGPD
- **O que significa:** tratar dados pessoais apenas com base legal, finalidade definida e o mínimo necessário (Lei 13.709/2018, art. 6º: finalidade, necessidade, segurança, transparência, entre outros).
- **No Bytebank:**
  - A base do RAG contém **políticas do banco, não dados de clientes**. Dados pessoais (CPF, saldo, fatura) só são acessados no momento do atendimento, via recursos MCP com autenticação, e não são indexados no vector store.
  - Cada trecho indexado tem o metadado `nivel_acesso`. O chatbot de clientes **só recupera trechos de nível público**; trechos internos/restritos ficam disponíveis apenas para agentes de uso interno.
  - Embeddings gerados com modelo **open source executado localmente**, para que o texto das políticas não seja enviado a terceiros só para vetorização (decisão detalhada no ADR da Etapa 2).
  - Antes de enviar uma pergunta a um LLM externo, dados pessoais identificáveis são mascarados (ex.: CPF → `***.***.***-**`).
- **Como verificamos:** RIPD (Relatório de Impacto à Proteção de Dados) aprovado pelo DPO; teste automatizado garantindo que o retriever do canal de clientes nunca devolve `nivel_acesso` diferente de público; logs sem dados pessoais em texto aberto.

### 2. Imparcialidade
- **O que significa:** o sistema não deve tratar clientes de forma desigual por características como gênero, idade, região ou renda, quando isso não tiver justificativa legítima.
- **No Bytebank:** o chatbot informa regras (tarifas, limites, prazos) que valem para todos; ele **não decide** crédito. Decisões de crédito acima de um limite passam por pessoa humana (Human-in-the-Loop, Etapa 4).
- **Como verificamos:** o dataset de avaliação inclui a mesma pergunta formulada de jeitos diferentes (linguagem formal e informal, com e sem erros de digitação) e compara a qualidade das respostas; o Cientista de Dados revisa periodicamente amostras por segmento.

### 3. Transparência
- **O que significa:** o cliente sabe que está falando com uma IA e entende os limites do que ela faz.
- **No Bytebank:** a interface informa "Você está falando com o assistente virtual do Bytebank"; quando não houver base para responder, o assistente diz isso e oferece atendimento humano, em vez de improvisar.
- **Como verificamos:** revisão de UX e teste de perguntas fora do escopo (o assistente deve recusar ou transferir).

### 4. Explicabilidade
- **O que significa:** ser possível explicar **por que** o sistema deu uma resposta.
- **No Bytebank:** toda resposta do RAG retorna os **`source_documents`** (id da política, domínio, seção). O atendente humano ou o auditor consegue ver de qual trecho a resposta veio. No multiagente, a classificação de intenção (para qual agente a pergunta foi roteada) também fica registrada.
- **Como verificamos:** nenhuma resposta do canal de clientes é exibida sem ao menos uma fonte associada.

### 5. Reprodutibilidade
- **O que significa:** conseguir refazer o mesmo resultado com as mesmas entradas, para auditar ou investigar uma reclamação.
- **No Bytebank:** versionamos o dataset de políticas, o código, os prompts, o modelo de embeddings e a versão do LLM; usamos temperatura baixa (0) nas respostas; snapshots do estado do grafo multiagente são guardados nos pontos de decisão.
- **Como verificamos:** a avaliação (Etapa 3) pode ser executada novamente a partir do repositório e deve produzir resultados comparáveis.

### 6. Responsabilidade (accountability)
- **O que significa:** sempre há pessoas responsáveis pelas decisões do sistema; "foi a IA" não é justificativa.
- **No Bytebank:** cada componente tem um dono (ver planilha do time). Ações com impacto financeiro (aprovação de cartão Platinum, contestação de fraude, crédito acima do limite) **exigem aprovação humana** antes de serem executadas.
- **Como verificamos:** trilha de auditoria registrando quem aprovou/cancelou cada ação interrompida pelo Human-in-the-Loop.

---

## (b) Tratamento de alucinações de LLMs

### O que é (e o que não é) alucinação
**Alucinação** é quando o modelo gera um conteúdo **plausível, bem escrito e confiante, porém incorreto ou sem base nos fatos**. Exemplo no Bytebank: perguntar "Qual a tarifa de manutenção da conta?" e o modelo responder "R$ 12,90 por mês" sem que esse valor exista em nenhuma política do banco.

Não é alucinação um **erro simples de processamento**: um timeout da API, um JSON malformado ou uma falha ao ler o CSV. Esses erros aparecem como falha; a alucinação é perigosa justamente porque **parece uma resposta correta**.

### Os três fatores contribuintes

| # | Fator | Por que causa alucinação | Como aparece no Bytebank |
|---|---|---|---|
| 1 | **Dados de treinamento limitados, desatualizados ou enviesados** | O modelo só "sabe" o que estava no treinamento, que tem data de corte, lacunas e erros. | O LLM nunca viu as políticas internas do Bytebank; se perguntado, preenche a lacuna com o que é comum em outros bancos. |
| 2 | **Natureza probabilística da geração** | O LLM prevê o próximo token mais provável; ele otimiza plausibilidade, não verdade, e não tem um mecanismo interno de checagem de fatos. Temperatura alta aumenta a variação. | Gera um prazo "típico" (ex.: "7 dias úteis") porque essa sequência é estatisticamente provável, não porque é a regra do banco. |
| 3 | **Falta de contexto ou prompt ambíguo** | Sem informação de referência e sem instrução para admitir desconhecimento, o modelo tende a responder algo em vez de dizer "não sei". | "Qual o limite?" (de qual produto? PIX? cartão?) leva a uma resposta inventada para uma interpretação qualquer. |

### Técnicas de mitigação adotadas

1. **RAG com fontes (grounding):** o LLM responde **somente com base nos trechos recuperados** das políticas do Bytebank e devolve os `source_documents`. Ataca os fatores 1 e 3: o conhecimento vem da base atualizada do banco e o contexto passa a existir.
2. **Engenharia de prompt com instrução de recusa:** o prompt de sistema determina: *"Responda apenas com base no contexto fornecido. Se a informação não estiver no contexto, diga que não sabe e ofereça atendimento humano."* Ataca o fator 3.
3. **Temperatura 0 e saída estruturada (Pydantic):** reduz a variação aleatória e obriga o modelo a preencher campos definidos (ex.: resposta + fontes), facilitando validação automática. Ataca o fator 2.
4. **Re-ranking:** reordena os trechos recuperados por relevância antes de enviá-los ao LLM, reduzindo o contexto irrelevante que poderia induzir erros.
5. **Avaliação contínua com LLM como juiz e Human-in-the-Loop:** um conjunto de perguntas com gabarito é avaliado a cada mudança (Etapa 3); ações de impacto financeiro passam por aprovação humana (Etapa 4).

> **Evidência prevista no projeto:** a Etapa 3 compara a resposta do LLM **sem RAG** com a resposta **com RAG** para as mesmas perguntas. O resultado esperado é que, sem RAG, o modelo invente regras do Bytebank, o que ilustra os fatores 1 e 2 desta seção.

---

## (c) Os quatro pilares do LLM Ops no contexto bancário

**LLM Ops** é o conjunto de práticas para colocar e manter aplicações com LLM em produção de forma confiável, assim como o MLOps faz para modelos de ML tradicionais.

| Pilar | O que é | Aplicação no Bytebank | Exemplo de indicador |
|---|---|---|---|
| **Gerenciamento** | Controle e versionamento de todos os ativos: modelos, prompts, dados, índices e configurações; governança de acesso. | Prompts versionados no Git; registro de qual versão do LLM, do modelo de embeddings e do dataset de políticas gerou cada resposta; controle de quem pode alterar a base de conhecimento; chaves de API em cofre de segredos, nunca no código. | 100% das respostas em produção rastreáveis até a versão de prompt e da base. |
| **Otimização** | Melhorar custo, latência e qualidade: escolha do modelo, tamanho do contexto, cache, chunking, re-ranking. | Modelo menor (GPT-4o-mini) para classificação de intenção e respostas simples; contexto limitado aos 4 melhores trechos após o re-ranking; cache de perguntas frequentes (ex.: "como abrir conta"). | Custo por atendimento; latência p95 abaixo da meta do canal. |
| **Automação** | Esteiras de CI/CD e de dados que executam testes, reindexação e deploy sem passos manuais. | Ao atualizar o `politicas_bytebank.csv`, a esteira recria o ChromaDB, roda a avaliação com o dataset de validação e só publica se a taxa de acerto não cair; rollback automático para a versão anterior. | Tempo entre mudança de política e chatbot atualizado. |
| **Qualidade** | Avaliação e monitoramento contínuos da saída: exatidão, alucinação, segurança, vieses, conformidade. | LLM como juiz sobre o dataset de validação; monitoramento de respostas sem fonte; amostragem semanal revisada por humanos; alertas se o retriever do canal de clientes retornar trecho não público. | % de acertos na avaliação; taxa de respostas sem fonte; incidentes de vazamento (meta: zero). |

---

## Como este documento é mantido
- **Dono:** DPO, com apoio da Engenharia de IA.
- **Revisão:** a cada nova funcionalidade com impacto em dados pessoais e, no mínimo, semestralmente.
- **Relação com outras etapas:** metadados e embeddings (Etapa 2 — ADR), comparação com/sem RAG e avaliação (Etapa 3), Human-in-the-Loop e snapshots (Etapa 4).
