# Linha do tempo: camada de tempo no mapa

> Data: 2026-10-22 · Status: **proposta, não aprovada** (feature D4, travada pela migração B4)

**Contexto.** Nenhuma ligação tem data estruturada. A ideia é um controle sob o grafo que mostre **quando cada
conexão veio a público**, com histograma por ano clicável. Animação e linha do tempo criam narrativa mesmo quando o
dado não sustenta uma: por isso o desenho vem com riscos explícitos.

**Decisões propostas.**
| # | Proposta | Alternativa descartada |
|---|---|---|
| D1 | O eixo é a **data da revelação** (primeira fonte pública que documenta a conexão) | Data do fato |
| D2 | Exibição por **ano** (mês e dia são guardados, mas não exibidos) | Mês ou dia (falsa precisão) |
| D3 | Modo padrão **acumulado** ("tudo o que já era público até X") | Modo "só o ano" (fica para a v2) |
| D4 | **Sem autoplay**: o site abre no estado atual | Abrir animando |
| D5 | Ligação **sem data nunca some** | Esconder quem não tem data |
| D6 | Cada ligação ganha um `Id` estável | Chave `source` + `target` (há pares repetidos) |

**Riscos que o desenho precisa cobrir.** Causalidade implícita (A depois de B parece plano); confundir revelação com
fato; falsa precisão; ausência de data lida como inexistência; alegação ganhando peso de fato (sem vermelho, tracejado
preservado); frame tirado de contexto (o aviso fica dentro da área do grafo); relação encerrada parecendo ativa.

**Critério para ir ao ar.** Pelo menos 70% das ligações datadas (abaixo de 50% a camada não faz sentido), toda data
com fonte, e um teste de entendimento com 5 pessoas fora da bolha (4 de 5 acertam o eixo e a diferença entre
alegação e fato).

**Em aberto.** Aprovação de D1 a D6; meta de cobertura (70% ou 80%); a ordem em relação ao redesign.
O `Id` estável (D6) já está previsto na migração para corpus único.

**Onde se executa.** Ainda não há código. A proposta completa (riscos R1 a R10 e fases) está no plano original,
`claude/plano-linha-do-tempo.md`, no Projeto claude.ai (histórico).
