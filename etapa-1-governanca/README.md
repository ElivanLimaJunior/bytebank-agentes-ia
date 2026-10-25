# Etapa 1 — Governança, time de IA e preparação de carreira

> **Pergunta-chave:** como estruturar a governança de um projeto de IA em um banco digital, definindo papéis, princípios éticos e estratégia de portfólio, de modo que o projeto seja sustentável e auditável?

## Arquivos

| Missão do enunciado | Arquivo | Observação |
|---|---|---|
| Planilha de composição do time (aba 1) | [time_de_ia.csv](time_de_ia.csv) | 7 cargos: os 5 obrigatórios + MLOps/LLMOps + Product Manager de IA |
| Planilha — aba carreira em Y (aba 2) | [carreira_em_y.csv](carreira_em_y.csv) | Caminho de gestão × especialista para cada cargo |
| Planilha pronta para o Google Sheets | [time_de_ia.xlsx](time_de_ia.xlsx) | As duas abas num único arquivo |
| Gerador da planilha | [gerar_planilha.py](gerar_planilha.py) | Fonte de verdade do conteúdo; regenera CSVs e .xlsx |
| Princípios éticos e conformidade | [principios_eticos.md](principios_eticos.md) | (a) 6 princípios, (b) alucinações: 3 fatores + 5 mitigações, (c) 4 pilares do LLM Ops |
| README de portfólio | [portfolio/README.md](portfolio/README.md) | Cópia do README publicado no repositório de perfil `ElivanLimaJunior/ElivanLimaJunior` |

## Decisões desta etapa
- **Coluna extra "Por que é necessário no Bytebank"** na planilha do time: o enunciado pede as 4 colunas *e* que cada papel seja justificado; a justificativa ganhou coluna própria para não poluir a coluna "Relação com o projeto".
- **Um único nível por cargo** (Jr, Pl ou Sr): é o nível esperado para a formação inicial do time, considerando o risco de cada papel (ex.: DPO e Engenharia de IA como Sr).
- **Carreira em Y:** "tende a seguir" é uma tendência, não uma regra; a planilha mostra os dois caminhos para todo cargo.
- **Portfólio no repositório de perfil + GitHub Pages:** ver [DECISOES.md](../DECISOES.md#d1).

## O que fazer manualmente

### Importar a planilha no Google Sheets
1. Acesse [sheets.new](https://sheets.new) (cria uma planilha em branco).
2. **Arquivo → Importar → Upload** e envie `time_de_ia.xlsx`.
3. Em "Local de importação", escolha **Substituir planilha**. As duas abas ("Time de IA" e "Carreira em Y") são criadas.
4. Renomeie para *Bytebank — Time de IA* e, em **Compartilhar**, deixe "Qualquer pessoa com o link: Leitor" se for enviar o link na entrega.

> Alternativa com os CSVs: importe `time_de_ia.csv` com **Substituir planilha** e depois `carreira_em_y.csv` com **Inserir nova(s) página(s)**.

### Publicar o README de portfólio (GitHub Pages)
1. O conteúdo de [portfolio/README.md](portfolio/README.md) vai para o `README.md` do repositório **`ElivanLimaJunior/ElivanLimaJunior`** (o nome tem de ser exatamente o username, como diz a dica do enunciado).
2. No GitHub, abra esse repositório → **Settings → Pages**.
3. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
4. Em **Branch**, escolha `main` e `/ (root)` → **Save**.
5. Aguarde 1–2 minutos (acompanhe em **Actions → pages build and deployment**) e acesse **https://elivanlimajunior.github.io/ElivanLimaJunior/**.

Sem um `index.html`, o GitHub Pages usa o Jekyll para transformar o `README.md` na página inicial, por isso não é preciso nenhum workflow.

### Regenerar a planilha (opcional)
```powershell
python etapa-1-governanca/gerar_planilha.py   # requer openpyxl para o .xlsx
```
