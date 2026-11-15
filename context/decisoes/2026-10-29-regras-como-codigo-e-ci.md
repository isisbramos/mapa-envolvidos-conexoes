# Regras editoriais como código, com CI em cada PR

> Data: 2026-10-29 · Status: vigente

**Contexto.** O review era "a dona lê tudo". Isso cresce linearmente com o número de nós e depende de uma
revisora só: com dois mapas ao mesmo tempo, ou o review atrasa ou o padrão cai.

**Decisão.** Transformar review por leitura em review por exceção:
- `scripts/validate.py` roda as regras como código, com o código da regra no erro;
- o CI roda validador, build e **checagem de sincronia** entre `data/mapa.xlsx` e `index.html` em cada PR;
- cada ligação ganha as colunas `Fontes` e `Nota da fonte`;
- as regras, antes espalhadas em 5 planos, ficam num `EDITORIAL.md` único;
- o modelo de PR traz a tabela "o que entrou / o que ficou de fora e por quê".

**Alternativas descartadas.** Continuar com review integral por leitura; montar um banco de dados.

**Por quê.** A máquina decide o que é mecânico, a dona decide o que é julgamento. Erro bloqueia o merge; aviso vai
para a fila de julgamento.

**Consequências.** PRs #6 a #8. Ao amarrar a fonte à ligação, 4 de 7 textos que citavam veículo sem link diziam mais
do que a fonte sustentava. O validador **não julga independência** entre fontes: isso segue humano (F3).

**Onde se executa.** `scripts/validate.py`, `.github/workflows/ci.yml`, `EDITORIAL.md`,
`.github/PULL_REQUEST_TEMPLATE.md`.
