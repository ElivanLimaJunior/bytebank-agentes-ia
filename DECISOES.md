# Registro de decisões do projeto

Decisões tomadas onde o enunciado é ambíguo, inconsistente ou deixa escolhas em aberto. Cada decisão aponta o trecho do enunciado, a alternativa escolhida e o porquê.

<a id="d1"></a>
## D1 — README de portfólio: repositório de perfil + GitHub Pages
- **Enunciado:** "Crie um repositório no GitHub com seu nome de usuário e configure o README.md como página de apresentação pessoal […] Publique via GitHub Pages." Dica: "o nome deve ser exatamente seu username".
- **Ambiguidade:** o repositório `ElivanLimaJunior/ElivanLimaJunior` é o *README de perfil* (aparece em github.com/ElivanLimaJunior); o *site de usuário* do Pages exige outro nome, `ElivanLimaJunior.github.io`.
- **Decisão:** usar o repositório **`ElivanLimaJunior/ElivanLimaJunior`** (atende literalmente à dica) e ativar o GitHub Pages nele como site de projeto, publicado em `https://elivanlimajunior.github.io/ElivanLimaJunior/`.
- **Por quê:** um único repositório atende às duas exigências e evita manter dois READMEs sincronizados (a Etapa 4 pede para atualizar este README).
- **Detalhe:** o repositório de perfil já tinha um README pessoal; o conteúdo existente foi preservado e as seções exigidas ("Sobre Mim", "Projetos em Destaque", "Contato") foram acrescentadas. Uma cópia fica em [etapa-1-governanca/portfolio/README.md](etapa-1-governanca/portfolio/README.md).

<a id="d2"></a>
## D2 — Execução do LLM
- **Contexto:** o projeto é desenvolvido sem chave de API de LLM.
- **Decisão:** o código que usa o LLM (re-ranking, geração, LLM como juiz, classificação de intenção) é escrito para o **ChatOpenAI (GPT-4o-mini)**, configurado via `.env`, mas **não é executado**. Tudo o que não depende do LLM é executado e verificado de verdade. Nenhum resultado de LLM é inventado: tabelas de avaliação ficam marcadas como "não executado".

<a id="d3"></a>
## D3 — Embeddings open source locais
- **Enunciado:** "OpenAIEmbeddings (ou HuggingFace Embeddings)"; "dados bancários são sensíveis — isso deve pesar na decisão".
- **Decisão:** HuggingFace (`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`), executado localmente, com vetores normalizados e similaridade de cosseno no ChromaDB.
- **Por quê:** o texto não sai da máquina para ser vetorizado, não há custo por chamada e o modelo é multilíngue (português). A configuração cosseno foi adotada após um teste em que a distância L2 padrão do ChromaDB ordenou errado os resultados. Justificativa completa no ADR da Etapa 2.

<a id="d4"></a>
## D4 — Ambiente Python
- **Decisão:** Python 3.14. Em 2026-10-25, chromadb 1.5.9, torch 2.14.1, gradio 6.30, langchain 1.4.7, langgraph 1.2.17 e sentence-transformers 6.2.0 instalaram e importaram sem erro nessa versão (ver [requirements.txt](requirements.txt)).
