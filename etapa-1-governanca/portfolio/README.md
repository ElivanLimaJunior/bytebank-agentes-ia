<div align="center">

# Elivan Lima Junior

### Business Intelligence | Data Engineering

[🌐 Portfólio](https://elivan-portifolio-ds.vercel.app) •
[💼 LinkedIn](https://www.linkedin.com/in/elivanjunior) •
[📧 E-mail](mailto:elivanjosejunior@gmail.com)

</div>

---

## 👨‍💻 Sobre Mim

Sou **Analista de Processos** com atuação em **Business Intelligence, automação e análise de dados**. Tenho experiência no desenvolvimento de dashboards em **Power BI**, criação e acompanhamento de **KPIs**, modelagem de dados e otimização de processos utilizando dados como suporte à tomada de decisão.

Atualmente estou direcionando minha carreira para **Engenharia de Dados**, aprofundando meus conhecimentos em **Python, SQL, ETL/ELT, bancos de dados e arquiteturas modernas de dados**.

Tenho interesse em construir soluções que conectem **dados, tecnologia e processos**, transformando informações em insights e melhorias operacionais.

Também curso a carreira **Especialista em IA** da Alura, onde aplico dados e IA generativa a problemas de negócio: RAG, agentes e governança de IA.

## ⭐ Projetos em Destaque

### 1. 🏦 Bytebank — Ecossistema de Agentes de IA para atendimento bancário

> 📂 Repositório: [bytebank-agentes-ia](https://github.com/ElivanLimaJunior/bytebank-agentes-ia) · 🚧 Em andamento (Etapa 1 de 4 concluída)

**🎯 Motivação.** Num banco digital, a mesma pergunta chega milhares de vezes por dia: *"qual a tarifa?"*, *"como aumento meu limite?"*, *"meus dados estão seguros?"*. Um chatbot comum, ligado direto a um LLM, responde com confiança, mas pode **inventar regras que o banco não tem**. Em um banco, isso é risco regulatório e quebra de confiança. Quis entender como construir um assistente que responda **só com base nas políticas reais** e saiba quando chamar uma pessoa.

**🧩 Problema resolvido.** O projeto projeta, do zero, o ecossistema de IA de atendimento do Bytebank (banco fictício):
1. **Governança:** composição do time de dados/IA, carreira em Y e princípios éticos (LGPD, explicabilidade, tratamento de alucinações, LLM Ops).
2. **Arquitetura RAG:** o chatbot consulta as políticas internas antes de responder e devolve as **fontes** de cada resposta, para auditoria.
3. **Pipeline RAG** em Python com ChromaDB, metadados de nível de acesso (cliente não vê conteúdo interno) e avaliação com LLM como juiz.
4. **Arquitetura multiagente** com supervisor que roteia para agentes de conta corrente, cartão e suporte, protocolos **A2A e MCP** e **Human-in-the-Loop** para decisões sensíveis (ex.: aprovação de cartão Platinum).

**⚙️ Desafios técnicos (até aqui).**
- **Dados sensíveis × embeddings:** escolhi um modelo de embeddings **open source rodando localmente** para que as políticas do banco não saiam da infraestrutura só para serem vetorizadas.
- **Um bug silencioso na busca vetorial:** num teste inicial, a pergunta *"quando meu limite muda?"* trazia um texto sobre PIX. Investigando, descobri que o ChromaDB usa distância **euclidiana (L2)** por padrão sobre vetores não normalizados. Normalizar os vetores e usar **similaridade de cosseno** corrigiu o ranking. O sistema não dava erro nenhum, só respondia pior.
- **Governança antes do código:** definir papéis (DPO, engenharia de dados, IA, MLOps) e princípios antes de programar, para o projeto ser auditável desde o início.

**🛠️ Tecnologias:** Python · LangChain · LangGraph · ChromaDB · Sentence-Transformers · Gradio · Pydantic · Mermaid

## 🚀 Tecnologias e Ferramentas

- 📊 Power BI
- 📈 Excel Avançado
- 🐍 Python
- 🗄️ SQL
- 🔄 Power Query
- 📋 DAX
- ⚙️ Power Automate
- 🔗 n8n
- 🌐 Git & GitHub

## 📚 Atualmente estudando

- Engenharia de Dados
- Modelagem de Dados
- ETL e ELT
- Bancos de Dados Relacionais
- Computação em Nuvem (Azure)
- Automação de processos com **Power Automate** e **n8n**
- Processamento e organização de dados com Python
- Inteligência Artificial: RAG, agentes e LLM Ops (carreira Especialista em IA — Alura)

## 🛠️ Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoftexcel&logoColor=white)
![Claude AI](https://img.shields.io/badge/Claude_AI-D97757?style=flat&logo=anthropic&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)

</div>

---

## 📬 Contato

- 💼 LinkedIn: [linkedin.com/in/elivanjunior](https://www.linkedin.com/in/elivanjunior)
- 📧 E-mail: [elivanjosejunior@gmail.com](mailto:elivanjosejunior@gmail.com)
- 🌐 Portfólio: [elivan-portifolio-ds.vercel.app](https://elivan-portifolio-ds.vercel.app)
- 🐙 GitHub: [github.com/ElivanLimaJunior](https://github.com/ElivanLimaJunior)

---

<div align="center">

**Elivan Lima Junior**

*"Transformando dados em decisões e processos em resultados."*

<br>

![Profile Views](https://komarev.com/ghpvc/?username=ElivanLimaJunior&color=blue&style=flat-square&label=VISITAS+NO+PERFIL)

</div>
