# "Reportado" no lugar de "Documentado"

> Data: 2026-10-23 · Status: vigente

**Contexto.** A revisão editorial antes de abrir a indexação apontou que o rótulo "Documentado" não se sustentava.
A base era, em boa parte, transcrição de vídeo e acervo de terceiros; quem lê "Documentado" entende "comprovado em
documento". 146 das 220 ligações estavam com esse status, e as ligações não tinham fonte própria: a fonte vivia no
perfil dos nós.

**Decisão.** O status passa a se chamar **"Reportado"** (a fonte apresenta como fato, registro, relatório oficial,
decisão judicial ou ato público). O outro valor, "Alegado ou contestado", fica como está. O texto do "Sobre" foi
reescrito, e itens de maior risco saíram do mapa no mesmo commit.

**Alternativa descartada.** Manter "Documentado" e explicar no "Sobre".

**Por quê.** O rótulo é lido antes do texto de apoio. Prometer mais do que a fonte entrega é o erro mais caro num
site que nomeia pessoas reais.

**Consequências.**
- O mapa passou de 96 nós, 220 ligações e 96 perfis para 95, 213 e 95; o status ficou em 141 "Reportado" e 72
  "Alegado ou contestado" (conferido nas duas versões da planilha).
- O `build.py` trata status desconhecido como "Reportado", então um erro de digitação promoveria uma alegação a
  fato. Por isso o validador barra (V3).
- O `README.md` ainda usa "Documentado": pendente de correção.

**Onde se executa.** `EDITORIAL.md` §2, `scripts/validate.py` (V3).
