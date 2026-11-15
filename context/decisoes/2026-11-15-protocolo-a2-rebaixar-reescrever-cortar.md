# Protocolo do A2: rebaixar, reescrever ou cortar; paywall; ritmo

> Data: 2026-11-15 · Status: vigente · Fecha as decisões 2, 3 e 4 do `data/roadmap.md`

**Contexto.** A regra F7 exige 2 fontes independentes em cada ligação "Alegado ou contestado". Das 72, 71 estão
abaixo do mínimo (fila em `data/fila-f7.md`, 10 lotes). Sem regra prévia, a primeira ligação difícil trava a
sessão: o que fazer quando a 2ª fonte independente não existe, quando a fonte está atrás de paywall e em que
ritmo revisar.

**Decisões.**
1. **Sem 2ª fonte independente**, nesta ordem de preferência:
   - **rebaixar** para "Reportado", só se a fonte for registro oficial que apresenta o fato (decisão judicial,
     ato público, relatório oficial);
   - **reescrever** para o que a fonte sustenta, quando o texto for mais forte que ela;
   - **cortar**, quando não sobrar nada. Nunca manter "Alegado" com uma fonte só depois que o F7 virar erro.
2. **Paywall:** vale a fonte que só a dona consegue ler. Ela cola o texto; fica registrada em `Nota da fonte` com
   "lida em DD/MM". Nenhuma URL entra sem ter sido aberta por alguém (F4).
3. **Ritmo:** um lote por PR, com aprovação de cada um. **Revisão extra** nos lotes mais sensíveis (1 e 5 da fila).

**Alternativas descartadas.**
- Manter "Alegado" com fonte única: contradiz F5 e deixaria o F7 em aviso para sempre.
- Só cortar: empobrece o mapa, e há ligações corretas que só falham por falta de uma 2ª cobertura.
- Aprovar a fila inteira de uma vez: um erro de leitura se espalharia por 71 ligações sem chance de revisão.

**Por quê.** A ordem vai da menor perda de informação (rebaixar só quando a fonte já é o próprio registro) à
maior (cortar), e cada degrau preserva o que a fonte realmente sustenta. O ritmo por lote mantém o review humano
no ponto em que o dano de um erro é maior: uma alegação sobre pessoa real.

**Consequências.**
- O A2 pode começar pelo lote 1 sem pergunta de protocolo.
- `Nota da fonte` passa a registrar leitura da dona e dependência entre fontes.
- A estimativa continua de 6 a 8 PRs.

**Onde se executa.** `data/fila-f7.md`, `EDITORIAL.md` §1 e §2, `scripts/validate.py` (V7).
