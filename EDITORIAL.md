# Regras editoriais

Este arquivo reúne, num lugar só, as regras que antes estavam espalhadas pelos
planos do projeto. **Nada aqui é regra nova**: é consolidação. O que estava
divergente entre documentos está na seção "A decidir", não resolvido por conta
própria.

O que for verificável por programa está implementado em `scripts/validate.py`,
com o código da regra (V1, V2, …) na mensagem de erro.

---

## 1. Fontes e verificação

| Regra | O que diz | Verificação |
|---|---|---|
| **F1** | Sem fonte, não entra. Reportagem, transcrição de vídeo, decisão judicial ou documento público | — |
| **F2** | **Mínimo de 2 fontes por perfil.** Exceção: estágio "Não pesquisado" (pessoas privadas, não nomeadas ou de identidade não confirmada) | `V1` |
| **F3** | Republicação do mesmo texto **não** conta como segunda fonte | humana |
| **F4** | Não citar como lida uma matéria que não foi possível abrir | humana |
| **F5** | Identidade incerta fica de fora até confirmar. Mais vale faltar do que atribuir à pessoa errada | humana |
| **F6** | Quando as fontes divergem sobre uma data, vale a mais antiga verificável | humana |

### Hierarquia de fontes

1. **Primária:** reportagem original; relatório da PF; decisão judicial; nota
   metodológica de quem produziu o dado.
2. **Corroboração independente:** veículo com equipe editorial identificável e
   apuração própria.
3. **Não usar:** blogs, agregadores, posts em rede social, sites sem equipe
   editorial identificável.

---

## 2. Status da ligação

Só existem dois valores, e eles são a diferença entre afirmar e relatar:

| Status | Quando usar |
|---|---|
| **Reportado** | A fonte apresenta como fato, registro, relatório oficial, decisão judicial ou ato público, com a fonte indicada no perfil dos envolvidos |
| **Alegado ou contestado** | É hipótese, suspeita, ou o citado nega |

- O valor precisa ser exatamente um desses dois (`V3`). O `build.py` trata
  status desconhecido como "Reportado" — um erro de digitação promove uma
  alegação a fato. Por isso o validador barra.
- Estágio ≠ culpa. Só quem está em "Condenado" tem decisão condenatória.
- Quando a pessoa ou empresa nega, a negativa entra em
  "Divergências / ressalvas" e o tom da descrição acompanha.
- Nenhum texto pode sugerir que contato registrado equivale a irregularidade.
  O dado mede volume de contato, não conteúdo.

---

## 3. Pessoas e exposição

| Regra | O que diz | Verificação |
|---|---|---|
| **P1** (antiga R4) | **Nunca expor crianças.** Sem foto, e o nome de menor não entra no contexto | humana |
| **P2** (antiga R5) | **Pessoa não pública não tem foto.** Só tem foto quem é figura pública: mandato ou cargo público, ministros, juízes, líderes religiosos com persona pública, influenciadores. Advogados privados, parentes, laranjas, funcionários e envolvidos anônimos podem ter contexto, se nomeados em fonte, mas não ganham foto | humana |
| **P3** | Pessoas privadas, não nomeadas ou de identidade não confirmada ficam no estágio "Não pesquisado" e não recebem perfil pesquisado | humana |

---

## 4. Imagens e licenças

| Regra | O que diz | Verificação |
|---|---|---|
| **I1** (antiga R1) | **Só imagem real**: a foto da própria pessoa, do próprio imóvel ou do próprio órgão. Nada genérico ou ilustrativo. Sem isso, o nó fica sem imagem | humana |
| **I2** (antiga R2) | **Licença livre e verificável**: domínio público, CC0, CC BY, CC BY-SA ou uso livre com crédito. Nada de agência paga nem print de reportagem | `V2` (presença de crédito e link) |
| **I3** (antiga R3) | **Empresa pode usar o próprio logo.** Empresa de fachada ou offshore sem marca pública fica sem imagem | humana |
| **I4** | Toda foto precisa de arquivo em `photos/`, crédito e link da fonte, e de uma linha em `photos/CREDITS.md` | `V2` |
| **I5** | Nó sem foto por regra tem o **motivo registrado** no `CREDITS.md` | humana |

---

## 5. Local

| Regra | O que diz | Verificação |
|---|---|---|
| **L1** (antiga R7) | Localização só em nível de cidade, UF ou bairro. **Nunca endereço exato** de imóvel | humana |

---

## 6. Processo

- **Um lote = um PR = um review.** Nada vai ao ar sem aprovação.
- Todo PR traz a tabela: o que entrou, o que ficou de fora e por quê.
- A fonte de verdade é `data/mapa.xlsx`. Não editar o JSON dentro do
  `index.html` para mudar conteúdo — o próximo build sobrescreve.
- Antes do commit: `python3 scripts/validate.py` e `python3 scripts/build.py`,
  sem erro, e teste em desktop e mobile.
- `data/mapa.xlsx` e `index.html` vão no mesmo commit.

---

## 7. Equivalência com a numeração antiga

Os planos existentes citam R1 a R7. A numeração antiga nasceu dentro do plano
de fotos, então cinco das sete regras eram sobre imagem. Esta é a tradução:

| Antiga | Agora |
|---|---|
| R1 — só imagem real | **I1** |
| R2 — licença livre e verificável | **I2** |
| R3 — empresa pode usar logo | **I3** |
| R4 — nunca expor crianças | **P1** |
| R5 — pessoa não pública sem foto | **P2** |
| R6 — contexto exige 2 fontes | **F2** |
| R7 — local em nível cidade/UF | **L1** |

---

## 8. A decidir

Pontos em que os documentos de plano divergem ou deixaram a pergunta em
aberto. **Não foram resolvidos aqui.**

1. **Duas fontes por ligação, ou só por perfil?** O plano de pendências
   propôs exigir 2 fontes também por ligação "Alegado ou contestado", e a
   decisão não ficou registrada. Hoje a regra F2 vale por perfil. A coluna
   `Fontes` da aba Edges existe para tornar essa regra verificável quando a
   decisão for tomada.
2. **Foto sem licença livre:** deixar o nó sem foto, ou pedir autorização ao
   fotógrafo?
3. **Quais entidades são institucionais** (PF, STF, Receita e afins). A
   distinção passa a importar quando dois mapas forem exibidos juntos: um
   órgão em comum não é ponto de encontro entre duas redes.
