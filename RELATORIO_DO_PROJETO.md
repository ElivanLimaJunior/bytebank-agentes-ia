# Relatório do projeto — Bytebank: Ecossistema de Agentes de IA

> **Checkpoint Especialista em IA — Nível 2 (Alura)** · Autor: Elivan Lima Junior · Repositório: [bytebank-agentes-ia](https://github.com/ElivanLimaJunior/bytebank-agentes-ia)
>
> **Estado em 2026-10-25:** Etapa 1 concluída; Etapas 2 a 4 com estrutura criada e conteúdo pendente. Este relatório descreve apenas o que foi efetivamente produzido e verificado; as seções das etapas pendentes serão preenchidas quando forem concluídas.

## 1. Contexto
A equipe de inovação do Bytebank (banco digital fictício) está estruturando um ecossistema de agentes de IA para atendimento digital. O projeto cobre quatro frentes: governança e time de IA; arquitetura de um sistema RAG que consulta políticas internas; implementação e avaliação desse pipeline; e uma arquitetura multiagente com roteamento, protocolos A2A/MCP e Human-in-the-Loop.

## 2. Estrutura do repositório

```
dados/                      dataset de políticas (pendente) e dados derivados
etapa-1-governanca/         planilha do time, carreira em Y, princípios éticos, README de portfólio
etapa-2-arquitetura-rag/    diagrama, glossário, ADR (pendente)
etapa-3-pipeline-rag/       código do pipeline, dataset de validação, resultados (pendente)
etapa-4-multiagente/        diagrama, protocolos, Agent Cards, LangGraph, Gradio (pendente)
DECISOES.md                 decisões tomadas onde o enunciado deixa escolhas
ENTREGA.md                  mapa missão → arquivo
```

## 3. Etapa 1 — Governança, time de IA e preparação de carreira ✅

**Pergunta-chave:** como estruturar a governança de um projeto de IA em um banco digital de modo que ele seja sustentável e auditável?

### 3.1 Composição do time
Foram definidos **7 papéis** ([time_de_ia.csv](etapa-1-governanca/time_de_ia.csv)): os cinco exigidos (engenheiro de dados, analista de dados, cientista de dados, DPO, engenheiro de IA) e dois adicionais, **engenheiro de MLOps/LLMOps** e **Product Manager de IA**, que materializam respectivamente os pilares de LLM Ops e as decisões de negócio sobre automação e intervenção humana.

| Cargo | Nível | Papel central no projeto |
|---|---|---|
| Engenheiro(a) de Dados | Pl | Ingestão e atualização da base de políticas e do vector store |
| Analista de Dados | Jr | KPIs do chatbot e lacunas da base de conhecimento |
| Cientista de Dados | Pl | Avaliação com × sem RAG, LLM como juiz, vieses |
| Engenheiro(a) de IA | Sr | RAG, agentes, protocolos A2A/MCP, guardrails |
| DPO | Sr | LGPD, RIPD, regras de nível de acesso |
| Engenheiro(a) de MLOps/LLMOps | Pl | Versionamento, CI/CD, monitoramento |
| Product Manager de IA | Sr | Escopo dos agentes e pontos de Human-in-the-Loop |

A aba de **carreira em Y** ([carreira_em_y.csv](etapa-1-governanca/carreira_em_y.csv)) indica a tendência de cada cargo: especialista para engenharia de dados, ciência de dados, engenharia de IA e MLOps; gestão para análise de dados, DPO e produto. Para todos os cargos, os dois caminhos de evolução estão descritos.

### 3.2 Princípios éticos e conformidade
O documento [principios_eticos.md](etapa-1-governanca/principios_eticos.md) estabelece:
- **Seis princípios** (privacidade/LGPD, imparcialidade, transparência, explicabilidade, reprodutibilidade, responsabilidade), cada um com aplicação concreta e forma de verificação. Exemplos: o metadado `nivel_acesso` restringe o que o chatbot de clientes pode recuperar; toda resposta retorna `source_documents`; ações financeiras sensíveis exigem aprovação humana.
- **Alucinações:** definidas como conteúdo plausível porém incorreto, distintas de erros de processamento. Três fatores contribuintes (dados de treinamento, natureza probabilística da geração, falta de contexto/prompt ambíguo) e cinco mitigações (RAG com fontes, instrução de recusa, temperatura 0 e saída estruturada, re-ranking, avaliação contínua e Human-in-the-Loop).
- **LLM Ops:** os quatro pilares (gerenciamento, otimização, automação, qualidade) com aplicação bancária e indicadores.

### 3.3 Portfólio
O README de portfólio ([portfolio/README.md](etapa-1-governanca/portfolio/README.md)) preserva o README de perfil já existente e acrescenta "Sobre Mim", "Projetos em Destaque" (Bytebank em primeiro, com motivação, problema resolvido e desafios técnicos) e "Contato". A publicação é no repositório `ElivanLimaJunior/ElivanLimaJunior` com GitHub Pages (decisão D1).

## 4. Etapa 2 — Arquitetura RAG e glossário técnico ⏳
Pendente. Depende do dataset `politicas_bytebank.csv` (colunas e valores reais de `nivel_acesso`).

## 5. Etapa 3 — Pipeline RAG funcional com avaliação ⏳
Pendente. Ver decisão D2: o código que depende de LLM será escrito, mas não executado (sem chave de API); não haverá resultados de LLM inventados.

## 6. Etapa 4 — Arquitetura multiagente, protocolos e Human-in-the-Loop ⏳
Pendente.

## 7. Decisões e verificações já realizadas
Detalhadas em [DECISOES.md](DECISOES.md):
- **D1** — Portfólio no repositório de perfil com GitHub Pages.
- **D2** — LLM (GPT-4o-mini) não executado por ausência de chave de API.
- **D3** — Embeddings HuggingFace locais com similaridade de cosseno. Verificado em teste: com a configuração padrão do ChromaDB (distância L2 sobre vetores não normalizados), a pergunta "quando meu limite muda?" recuperou primeiro um texto sobre PIX; com vetores normalizados e cosseno, o texto correto ficou em primeiro (distâncias 0,655 × 0,800).
- **D4** — Python 3.14 validado com a stack do projeto.

## 8. Ações manuais pendentes
- Importar `time_de_ia.xlsx` no Google Sheets.
- Publicar o README de portfólio no repositório de perfil e ativar o GitHub Pages.
- Fornecer o conteúdo do `politicas_bytebank.csv` para as Etapas 2 e 3.
