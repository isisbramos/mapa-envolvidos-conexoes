# Pós-eleição: como o site fala do 2º turno

> Data: 2026-10-26 · Status: vigente

**Contexto.** O 2º turno foi em 25/10/2026. O site ainda tinha texto no futuro ("o 2º turno é em 25/10") e descrevia
o nó central como candidato.

**Decisões.**
1. **Número:** publicar o resultado oficial, com a fonte e a data no texto, e não esperar uma apuração mais
   completa. O texto no ar traz 51,79% × 48,21% dos votos válidos, "segundo o TSE".
2. **Redação:** "disputou a Presidência em 2026", em vez de "candidato derrotado".
3. **Mandato:** escrever a data-limite (até 31/01/2027) no perfil, só com duas fontes oficiais. Se divergirem, não
   escrever data.
4. **Nota "Este mapa não pede voto em nenhum candidato":** manter. É registro de conduta, não de período.
5. **SEO:** liberar o merge mantendo a indexação desligada (ver 2026-10-28-seo-neutro-indexacao-desligada).

**Alternativas descartadas.** Esperar a apuração fechar; "candidato derrotado" (mesma informação, tom menos
neutro e envelhece pior); passar a nota para o passado ou retirá-la.

**Consequências.** A copy eleitoral vencida saiu do ar (perfil, descrição dos nós e nota de contexto). A varredura de
cargos eletivos (plano de 26/10, não reconferida) foi negativa: nenhum dos 12 candidatos dos 6 pleitos de 2º turno (AC, AM, ES, RN, TO, DF) é nó do
mapa. Registrar a data de checagem em todo perfil tocado.

**Onde se executa.** `data/mapa.xlsx` (Nodes, Perfis), `notes` do `index.html` (o `build.py` não toca nele).
