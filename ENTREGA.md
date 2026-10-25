# Mapa da entrega

Cada missão do enunciado → arquivo que a atende. Legenda: ✅ concluído · ⏳ pendente · 🖐️ ação manual fora do repositório.

> **Estado em 2026-10-25:** Etapa 1 concluída. Etapas 2 a 4 com estrutura criada e conteúdo pendente, aguardando o dataset `politicas_bytebank.csv`.

## Etapa 1 — Governança, time de IA e preparação de carreira ✅

| Missão | Arquivo | Status |
|---|---|---|
| Planilha de composição do time (Cargo, Responsabilidades, Nível, Relação com o projeto + justificativa; ≥ 5 papéis) | [etapa-1-governanca/time_de_ia.csv](etapa-1-governanca/time_de_ia.csv) · [time_de_ia.xlsx](etapa-1-governanca/time_de_ia.xlsx) (aba "Time de IA") | ✅ 7 papéis · 🖐️ importar no Google Sheets |
| Aba carreira em Y (gestão × especialista por cargo) | [etapa-1-governanca/carreira_em_y.csv](etapa-1-governanca/carreira_em_y.csv) · [time_de_ia.xlsx](etapa-1-governanca/time_de_ia.xlsx) (aba "Carreira em Y") | ✅ |
| Princípios éticos (a) privacidade/LGPD, imparcialidade, transparência, explicabilidade, reprodutibilidade, responsabilidade | [etapa-1-governanca/principios_eticos.md](etapa-1-governanca/principios_eticos.md#a-princípios-éticos-aplicáveis) | ✅ |
| (b) Alucinações: 3 fatores contribuintes + ≥ 2 mitigações | [principios_eticos.md](etapa-1-governanca/principios_eticos.md#b-tratamento-de-alucinações-de-llms) | ✅ 3 fatores, 5 mitigações |
| (c) 4 pilares do LLM Ops no contexto bancário | [principios_eticos.md](etapa-1-governanca/principios_eticos.md#c-os-quatro-pilares-do-llm-ops-no-contexto-bancário) | ✅ |
| README de portfólio ("Sobre Mim", "Projetos em Destaque" com storytelling, "Contato") | [etapa-1-governanca/portfolio/README.md](etapa-1-governanca/portfolio/README.md) | ✅ conteúdo · 🖐️ publicar em `ElivanLimaJunior/ElivanLimaJunior` |
| Publicação via GitHub Pages | Passo a passo em [etapa-1-governanca/README.md](etapa-1-governanca/README.md#publicar-o-readme-de-portfólio-github-pages) | 🖐️ ativar o Pages |

## Etapa 2 — Arquitetura RAG e glossário técnico ⏳

| Missão | Arquivo previsto | Status |
|---|---|---|
| Diagrama da pipeline RAG (a)–(j) | `etapa-2-arquitetura-rag/diagrama_arquitetura.md` (Mermaid + instruções draw.io) | ⏳ |
| Glossário técnico (≥ 15 termos) | `etapa-2-arquitetura-rag/glossario.csv` | ⏳ |
| ADR (RAG × fine-tuning, embeddings, metadados) | `etapa-2-arquitetura-rag/ADR-001-banco-vetorial-e-embeddings.md` | ⏳ |

## Etapa 3 — Pipeline RAG funcional com avaliação ⏳

| Missão | Arquivo previsto | Status |
|---|---|---|
| Dataset de políticas | `dados/politicas_bytebank.csv` | ⏳ aguardando o conteúdo do enunciado |
| Carregamento, chunking e categorias | `etapa-3-pipeline-rag/src/` | ⏳ |
| Embeddings, ChromaDB e retriever (k=4), 3 perguntas de teste | `etapa-3-pipeline-rag/src/` | ⏳ |
| Cadeia RAG com re-ranking; com × sem RAG | `etapa-3-pipeline-rag/src/` | ⏳ |
| Avaliação (≥ 8 pares, LLM como juiz, tabela) | `etapa-3-pipeline-rag/dataset_validacao.csv` · `resultados_avaliacao.md` | ⏳ |

## Etapa 4 — Arquitetura multiagente, protocolos e Human-in-the-Loop ⏳

| Missão | Arquivo previsto | Status |
|---|---|---|
| Diagrama multiagente (a)–(h) | `etapa-4-multiagente/diagrama_multiagente.md` | ⏳ |
| Documento de protocolos e decisões | `etapa-4-multiagente/protocolos.md` | ⏳ |
| Agent Cards | `etapa-4-multiagente/agent_cards/*.json` | ⏳ |
| Protótipo LangGraph | `etapa-4-multiagente/grafo_langgraph.py` | ⏳ |
| Interface Gradio | `etapa-4-multiagente/app_gradio.py` | ⏳ |
| Atualização do README de portfólio | `etapa-1-governanca/portfolio/README.md` | ⏳ |

## Documentos transversais
| Documento | Arquivo |
|---|---|
| Visão geral do projeto | [README.md](README.md) |
| Registro de decisões | [DECISOES.md](DECISOES.md) |
| Relatório do projeto | [RELATORIO_DO_PROJETO.md](RELATORIO_DO_PROJETO.md) |
