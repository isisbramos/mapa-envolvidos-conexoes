# Mapa de Envolvidos e Conexões — router

Leia este arquivo antes de qualquer outro. Não varra o repo: abra só o que o assunto pede.

## O que é
Site estático (grafo interativo) que organiza pessoas, empresas e casos citados em investigações
jornalísticas, com status por ligação ("Reportado" ou "Alegado ou contestado") e fontes.
Repo público `isisbramos/mapa-envolvidos-conexoes`, deploy na Vercel a cada push na `main`.
Site: comquemandaflaviobolsonaro.space. Planilha → `build.py` → `index.html`.
- **Nomes:** título público neutro "Mapa de envolvidos e conexões"; o domínio mantém o nome. Nome guarda-chuva
  da coleção está em aberto (decisão 10 do `data/roadmap.md`).
- **Termo legado, não usar:** "Documentado" (hoje é "Reportado"). O `README.md` ainda usa; é para corrigir.

## Estado em 1 minuto
> last-reviewed: 2026-11-19 (números conferidos com `validate.py` nessa data; prioridades vêm de `data/roadmap.md`)
- Produção: o último PR de conteúdo mergeado é o #26 (19/11, lote 3a do A2). Sem hash de commit aqui:
  ele se invalida no próprio merge. `git log -1` responde.
- Conteúdo: 95 nós · 213 ligações · 95 perfis · 142 "Reportado" · 71 "Alegado ou contestado" · fotos 40/95.
- Validador: 0 erros, 3 avisos (V6, V7, V9); roda no CI junto com build e checagem de sincronia.
- Regra F7 (2 fontes por ligação "Alegado"): 18 de 71 cumprida (lotes 1, 2 e 3a mergeados). Hoje é aviso;
  vira erro quando V7 = 0. Nem toda ligação fechada chega a 2 fontes: 4 (3 do lote 2, 1 do lote 3a) ficaram
  com 1 fonte registrada e nota de apuração única (decisão da dona), igual ao caso mantega→vorcaro do
  `EDITORIAL.md`.
- Abertura ao público: `noindex, nofollow` ligado; assinatura por pseudônimo. Os dois mudam juntos, só depois
  do fim do F7/E6 e de leitura jurídica. Nenhum dos dois se desfaz com um commit.
- Prioridade atual: A2, fontes nas ligações "Alegado" restantes, em lotes (um lote = um PR). Lotes 1, 2 e 3a
  fechados; lote 3b é o próximo (`data/fila-f7.md`).
- Mapa 2 (prefeitos) e "juntar mapas" dependem da migração B4 (corpus único), ainda não feita.

## Onde está a verdade
| Assunto | Fonte da verdade | Atenção |
| --- | --- | --- |
| Nós, ligações, perfis | `data/mapa.xlsx` | O JSON dentro do `index.html` é gerado; nunca editar à mão |
| Regras editoriais | `EDITORIAL.md` | Planos antigos citam R1–R7; tradução na §7 |
| Regras verificáveis | `scripts/validate.py` | Códigos V1–V11 do plano antigo de migração NÃO batem com o código real |
| Build | `scripts/build.py` | Preserva `notes`, `stages` e o `<head>` do `index.html` |
| Fotos e licenças | `photos/CREDITS.md` | Foto só com licença livre verificável |
| Como contribuir | `CONTRIBUTING.md`, `.github/PULL_REQUEST_TEMPLATE.md` | — |
| Roadmap, ordem e decisões pendentes | `data/roadmap.md` | Contagens não moram lá: ficam aqui e no `validate.py` |
| Fila do F7 (fontes nas ligações "Alegado") | `data/fila-f7.md` | Números de linha deslocam se a aba `Edges` mudar; reconferir |
| Plano de organização do projeto (playbook), passo a passo | `data/plano-organizacao.md` | Passo concluído é marcado ✅, nunca apagado |
| Como operar: analytics e migração B4 | `ops/README.md` | A migração só roda depois da decisão 11 do roadmap |
| Por que o projeto é como é (decisões datadas) | `context/README.md` → `context/decisoes/` | Uma decisão por arquivo; a substituída ganha status, não some |

**Quando código e doc discordam, o código vence.**
**Ignore:** `redesign-visual` (planilha antiga, não mergear); planos de 22–26/10 no Projeto claude.ai (históricos).

## Quando ler o quê
- **O que fazer a seguir, decisões pendentes:** `data/roadmap.md`.
- **Por que uma regra ou escolha existe, antes de propor mudá-la:** `context/README.md` (índice das decisões).
- **Editar perfil, ligação ou status:** `EDITORIAL.md` → `CONTRIBUTING.md` → rodar `validate.py` e `build.py`.
- **Fonte por ligação (F7/A2):** `data/fila-f7.md` + `EDITORIAL.md` §1 e §2.
- **Foto ou logo:** `EDITORIAL.md` §4 → `photos/CREDITS.md`.
- **SEO, indexação, assinatura:** não mexer sem decisão da dona do projeto.
- **Analytics (Umami):** `ops/analytics.md` (o código vale: `<head>` do `index.html`).
- **Migração para corpus único:** `ops/migracao-corpus-unico.md` (fases 0–5; só depois da decisão 11 do roadmap).

## Regras de produção
- Merge e publicação só com aprovação explícita da dona. Um lote = um PR = um review.
- Antes de qualquer sessão no clone local, `git pull --ff-only`: a pasta do Mac já chegou a 16 commits atrás.
- Todo PR traz a tabela "o que entrou / o que ficou de fora e por quê".
- `data/mapa.xlsx` e `index.html` vão no mesmo commit; o CI barra quem esquecer o build.
- Nunca citar como lida matéria que não foi aberta. Paywall: a dona cola o texto.
- Pessoa não pública e menor: sem foto; local só em nível cidade/UF.
- **Repo público:** não entra nota pessoal, e-mail, ID de planilha, estratégia jurídica, de funding ou do
  pseudônimo. Isso mora no vault privado.
- O `.gitignore` bloqueia todo `*.md` (as notas privadas moram na mesma pasta, no Mac). Só os `.md` da
  whitelist vão ao GitHub; arquivo novo de contexto precisa entrar na whitelist no mesmo PR.
- [2026-11-15] Entradas da whitelist na raiz levam `/` na frente (`!/README.md`). Sem isso, um `README.md` ou
  `CLAUDE.md` de subpasta escapa do bloqueio. Depois de criar `.md` privado: `git check-ignore -v <arquivo>`.

## Write-back
- Quando eu corrigir algo ou decidirmos algo, atualize o arquivo certo e diga em 1 linha o que mudou:
  - mudou estado, contagem ou prioridade → "Estado em 1 minuto" deste arquivo
  - decisão com alternativas → `context/decisoes/AAAA-MM-DD-<slug>.md` (criar junto com a 1ª decisão)
  - correção editorial recorrente → `EDITORIAL.md` (editar a regra, não duplicar)
  - algo quebrou e foi resolvido → `ops/runbook.md` (criar junto com o 1º caso)
- Gravou num arquivo da área? Confira se o "Estado em 1 minuto" também mudou.
- No "Estado em 1 minuto", só entra fato que sobrevive ao merge: contagens, regras, prioridade. Nada de hash.
- [2026-11-19] Nada de "PR aberto" ou "aguardando aprovação" no estado nem na fila: no PR do lote, escreva já como
  ficará depois do merge ("Fechado, PR #N"), no mesmo PR. Não abra um PR separado só de write-back.
- Regras novas entram com data: `- [AAAA-MM-DD] ...`. Antes de adicionar, procure uma parecida.
- Write-back nunca muda conteúdo publicado: isso segue o fluxo de PR e aprovação.

## Manutenção
- No máximo 150 linhas. Se `last-reviewed` passar de 30 dias, avise no início da sessão.
- Mensal: conferir este estado contra `validate.py` e a `main`; conferir as instructions do Projeto claude.ai
  e a memória contra este arquivo; mostrar o diff antes de salvar.
