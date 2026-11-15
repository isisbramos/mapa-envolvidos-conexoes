# Planilha como fonte de verdade do conteúdo

> Data: 2026-10-20 · Status: vigente (será substituída por 2026-10-29-corpus-unico-mapas-como-selecao)

**Contexto.** O conteúdo morava num JSON editado à mão dentro do `index.html`. O contexto de uma conversa de chat
ficou grande demais para ser a única fonte de verdade entre sessões.

**Decisão.** O conteúdo passa a viver em `data/mapa.xlsx` (abas `Nodes`, `Edges`, `Perfis`, `Notes`), e
`scripts/build.py` gera o JSON dentro do `index.html`. Ninguém edita esse JSON à mão: o próximo build o sobrescreve.

**Alternativa descartada.** Continuar com o JSON manual no HTML.

**Por quê.** Uma fonte estruturada que qualquer sessão consegue abrir e conferir, sem depender do histórico de uma
conversa.

**Consequências.**
- O `.xlsx` é binário: não tem diff legível nem faz merge. A branch `redesign-visual` carrega uma versão velha da
  planilha (90 nós, 197 ligações e 35 perfis, contra 95, 213 e 95 na `main`, conferido em 15/11) e não dá para
  mergear. Isso motivou a decisão de corpus único.
- `data/mapa.xlsx` e `index.html` vão no mesmo commit, e o CI confere a sincronia.

**Onde se executa.** `data/mapa.xlsx`, `scripts/build.py`, `EDITORIAL.md` §6.
