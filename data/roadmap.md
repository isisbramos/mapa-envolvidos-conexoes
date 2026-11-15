# Roadmap

> last-reviewed: 2026-11-15

Responde "o que falta fazer, em que ordem e o que depende de decisão". Os planos de execução de cada
item ficam nos arquivos apontados. Contagens e cobertura **não moram aqui**: ficam no "Estado em 1 minuto"
do `CLAUDE.md` e no relatório de `python3 scripts/validate.py`. Quando este arquivo e o código discordam,
o código vence.

## Fechado

| PR | Entrega |
|---|---|
| #1 a #5 (23 a 28/10) | Base piauí/InterSecLab, revisão pós-2º turno, lacunas pós-eleição, SEO neutro (canonical, JSON-LD, sitemap), ajuste de descrição |
| #6 | Colunas `Fontes` e `Nota da fonte` na aba Edges, `scripts/validate.py`, `EDITORIAL.md`, modelo de PR |
| #7 | CI: validador, build e checagem de sincronia entre planilha e `index.html` |
| #8 | Fonte nas 7 ligações que citavam veículo sem link, e 4 correções de texto |
| #9 (30/10) | Regra F7: "Alegado ou contestado" exige 2 fontes na própria ligação. Entra como aviso (V7) |
| #10 e #11 (15/11) | `CLAUDE.md` como router, liberado no `.gitignore`; estado sem hash de commit |

**Lição de método (#8):** das 7 ligações sem fonte amarrada, 4 tinham texto que dizia mais do que a fonte
sustenta. A coluna `Fontes` existe para tornar isso visível.

## Cinco trilhas

| Trilha | O que é | Estado |
|---|---|---|
| **A. Conteúdo editorial** | Fontes, perfis e fotos que faltam | **Caminho crítico** |
| **B. Dados e processo** | Migração, tags, arrumação | Base pronta |
| **C. Abertura ao público** | Indexação e assinatura | Travada pela A e por leitura jurídica |
| **D. Features** | Juntar mapas, pontos de encontro, linha do tempo | Travada pela B |
| **E. Mapa 2** | Primeiro mapa de prefeito | Travada pela B e pela D |

## Backlog

### A. Conteúdo editorial

| # | Item | Esforço | Estado |
|---|---|---|---|
| A2 | **Fonte nas ligações "Alegado" abaixo de 2 fontes** (V7 lista as linhas). Para cada uma: achar a 2ª fonte independente, reescrever, rebaixar para "Reportado" (só se for registro oficial) ou cortar. 10 lotes, estimativa de 6 a 8 PRs, um lote por PR. Plano e lotes: `data/fila-f7.md` | M a L | **Próximo passo** |
| A3 | Nenhuma "Reportado" apoiada só em uma fonte que não é primária (ICL, vídeo). Depende de A2 | L | Aberto |
| A5 | Uma ligação "Alegado" cujas duas coberturas remetem à mesma apuração. Decidir: manter, rebaixar ou cortar | S | Decisão 1 |
| A6 | Fotos: faltam em 55 perfis. Só entra com licença livre verificável | M | Decisão 5 |
| A7 | Matéria da piauí sobre valores de viagens de um dos nós: a dona precisa colar o texto (paywall) | S | Depende dela |
| A8 | Perguntas à piauí/InterSecLab sobre método e divergências internas da reportagem | L | Depende dela enviar |

### B. Dados e processo

| # | Item | Esforço | Estado |
|---|---|---|---|
| B1 | Aba `Resumo`: fórmulas param na linha 36 e `Perfis` tem 96 linhas; os totais subcontam (V9) | S | Aberto |
| B2 | Tag no Git a cada publicação + arquivamento externo (Internet Archive) | S | Aberto |
| B3 | Apagar branches já contidas na `main`: `feature/analytics`, `feature/base-piaui`, `regra-fonte-por-ligacao`, `revisao-pos-2-turno`. Conferido em 15/11: nenhuma tem trabalho inédito (`feature/base-piaui` está na `main` com outros hashes, por rebase). Aprovado; falta rodar o comando no GitHub | S | **Aprovado, pendente** |
| B4 | Migração para corpus único: um arquivo por entidade, ligações num CSV, mapas como seleção. Prompt de execução: `ops/migracao-corpus-unico.md` (as fases de validador, CI e `EDITORIAL.md` do plano original já foram feitas nos PRs #6 e #7) | M | Aberto |
| B5 | Flag `institucional` nas entidades (órgãos não contam como ponte entre mapas) | S | Decisão 8 |
| B6 | ~~Sincronizar o checkout local com a `main`~~ | S | ✅ 15/11 |

### C. Abertura ao público

| # | Item |
|---|---|
| C1 | Leitura jurídica |
| C2 | `noindex` → `index, follow` e Search Console |
| C3 | Assinatura do site |
| C4 | Política de correção: canal, prazo, log público |

C2 e C3 saem juntos, depois de C1. Nenhum dos dois se desfaz com um commit.

### D. Features e E. Mapa 2

| # | Item |
|---|---|
| D1 a D5 | Hub multi-mapa · juntar mapas · pontos de encontro (instituições separadas das pontes reais) · linha do tempo · perfil cross-map |
| E1 a E4 | Escolher o prefeito com critério declarado · teto de ~40 nós · produção · capacidade (segundo revisor ou 1 mapa por ciclo) |

A linha do tempo (D4) tem plano e decisões D1 a D6 prontos (`context/decisoes/2026-10-22-linha-do-tempo-proposta.md`).

## Ordem recomendada

| Quando | O quê |
|---|---|
| **Agora** | A2 em lotes |
| **Lote rápido** | B1, B2 e B3 juntos |
| **Entre dois lotes de A2** | B4 (migração), se a decisão 11 for aprovada; senão, depois de A2 |
| **Depois de A2** | A3 → C1 → C2 e C3 |
| **Depois de B4** | D1 → D2 → D3 |
| **2027** | E |

## Decisões pendentes (da dona do projeto)

| # | Decisão | Trava |
|---|---|---|
| 1 | Ligação de apuração única (A5): manter, rebaixar ou cortar | A5 |
| 2 | Ligação "Alegado" sem 2ª fonte independente: cortar, reescrever ou rebaixar. *Recomendação:* rebaixar quando couber (registro oficial), reescrever quando o texto for mais forte que a fonte, cortar quando não sobrar nada | A2 |
| 3 | Fonte que só a dona consegue ler (paywall), registrada em `Nota da fonte` com "lida em DD/MM". *Recomendação:* aceitar | A2 |
| 4 | Ritmo: um lote por PR com aprovação de cada um. *Recomendação:* sim, com revisão extra nos lotes mais sensíveis | A2 |
| 5 | Foto sem licença livre: deixar sem, ou pedir autorização | A6 |
| 6 | Destino da branch `redesign-visual` (4 commits únicos, sobre planilha antiga) | Antes de B4 |
| 7 | Quais entidades são institucionais | B5 |
| 8 | Qual prefeito é o mapa 2, com que critério; teto de nós; segundo revisor ou 1 mapa por ciclo | E |
| 9 | Assinatura do site e momento de indexar | C |
| 10 | Nome guarda-chuva da coleção | Antes de D1 e da indexação |
| 11 | Quando migrar para corpus único (B4): em paralelo com A2, ou só depois? O plano de 28/10 diz "nunca migrar com PRs editoriais em voo" (mistura refactor e conteúdo no mesmo diff), e A2 são 6 a 8 PRs seguidos. A `data/fila-f7.md` também está chaveada por linha da aba `Edges`, que a migração muda. *Recomendação:* migrar só entre dois lotes, sem PR editorial aberto, com o JSON gerado idêntico ao anterior como critério de aceite e a fila re-chaveada por `id` no mesmo PR. Detalhe em `context/decisoes/2026-10-29-corpus-unico-mapas-como-selecao.md` | B4 |

## Riscos vivos

| Risco | Mitigação |
|---|---|
| Texto derivar do que a fonte diz | A coluna `Fontes`; comparar lado a lado; nenhuma URL entra sem ser aberta |
| F7 ficar em aviso para sempre | Critério de saída: V7 = 0, e `EXIGIR_FONTE_NA_LIGACAO = True` no mesmo PR |
| Indexar antes de A3 | C2 depende de A3 |
| Assinar antes da leitura jurídica | C3 só depois de C1 |
| Juntar mapas sugerir uma rede que não existe | Flag `institucional` (B5) |
| Sem registro do que estava no ar em tal data | Tag por publicação (B2) |
| Clone local atrás da `main` | `git pull --ff-only` antes da sessão (regra no `CLAUDE.md`) |

## Organização do contexto (playbook "folders as architecture")

| Fase | Estado |
|---|---|
| 0. Inventário | ✅ 15/11 |
| 1. Router | ✅ `CLAUDE.md` no ar; gate nas 3 portas em ajuste |
| 2. Migração | Em andamento, um PR por conteúdo: roadmap ✅ → fila do F7 ✅ → decisões ✅ → analytics e prompt de migração ✅ → planos executados |
| 3. Write-back | Observar 2 sessões reais gravando sozinhas |
| 4. Manutenção | `ops/manutencao.md` + tarefa mensal agendada |
| 5. Legado | Arquivar cópias e trocar notas externas por links |
