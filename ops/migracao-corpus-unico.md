# Migração para corpus único (B4): prompt de execução

> last-reviewed: 2026-11-15 · status: **não executar antes da decisão 11 do `data/roadmap.md`**
> Por que este desenho: `context/decisoes/2026-10-29-corpus-unico-mapas-como-selecao.md`.

Este é o prompt para colar numa sessão do Claude Code, no clone do repo. Só as fases 0 a 5: as fases de validador,
CI, modelo de PR e `EDITORIAL.md` do plano original já foram feitas nos PRs #6 e #7. Os códigos V1 a V11 e as
regras R1 a R7 do plano original não valem; vale o `scripts/validate.py` real e a tabela da §7 do `EDITORIAL.md`.

## Antes de colar (a dona confere)
- [ ] Decisão 11 aprovada e **nenhum PR editorial aberto**.
- [ ] `main` limpa e o clone com `git pull --ff-only`.
- [ ] A `data/fila-f7.md` será re-chaveada por `id` no mesmo PR (hoje ela usa o número da linha da aba `Edges`).

---

Você vai migrar o conteúdo deste repositório de uma planilha Excel para arquivos de texto versionáveis, e fazer
o `build.py` e o `validate.py` lerem o novo formato. Trabalhe em português nos commits e nos docs.

## Regra de ouro
**Esta migração não muda uma vírgula de conteúdo.** É mudança de formato e organização. O site gerado depois tem
que ser idêntico ao gerado antes. Se precisar "corrigir" um dado para a migração funcionar, **pare e pergunte**:
isso é decisão editorial, não técnica.

## Para que serve
Vão existir vários mapas, e o leitor vai poder juntar dois e ver a união. Regra estrutural: cada entidade e cada
ligação existe **uma única vez** no repositório; um mapa é um recorte (seleção) sobre esse corpus, nunca um
container com cópia própria. Se o mesmo perfil existir em dois lugares, eles divergem e a união duplica.

## Contexto do repositório
- Conteúdo: `data/mapa.xlsx`, abas `Nodes`, `Edges` (com `Fontes` e `Nota da fonte`), `Perfis`, `Notes`, `Resumo`.
  Confirme os nomes reais; não assuma.
- `scripts/build.py` lê a planilha e regenera o bloco de dados do `index.html`. `scripts/validate.py` lê a mesma
  planilha e roda as regras do `EDITORIAL.md`. O CI (`.github/workflows/ci.yml`) roda validador, build e a
  checagem de sincronia do `index.html`.
- **Não toque** (o `build.py` também não toca): o bloco `notes`, o bloco `stages` e o `<head>` do `index.html`.
- O `.gitignore` bloqueia todo `*.md`. Todo `.md` novo (as entidades e o `SCHEMA.md`) precisa entrar na whitelist
  **no mesmo PR**, senão o CI passa sem eles.
- Repo público: nada de nota pessoal, e-mail ou ID de planilha em nenhum arquivo novo.

## Fase 0: preparação
1. `git status` limpo e `main` atualizada. Se não estiver, pare e avise.
2. Branch `refactor/corpus-unico` a partir da `main`.
3. Não apague branch, não mergeie nada.

## Fase 1: inventário (não escreva nenhum arquivo)
Devolva um relatório com:
- cada aba, com as colunas exatas e a contagem de linhas;
- quais colunas o `build.py` e o `validate.py` realmente leem, e quais ignoram;
- contagem de nós, ligações e perfis (hoje: 95, 213 e 95, conferir);
- campos vazios, e valores distintos das colunas de status, grupo e estágio;
- quais colunas guardam fonte, foto, crédito e licença;
- quais colunas são prosa longa (vão para o corpo do Markdown) e quais são valores curtos (frontmatter);
- **proposta** de quais entidades são institucionais (órgãos, tribunais, polícias, bancos públicos, CPIs), a partir
  da coluna de grupo. É para a dona aprovar (decisão 7 do roadmap), nunca para aplicar por conta própria;
- pares `source`/`target` repetidos, e qualquer inconsistência (não corrija, só liste).

**Pare aqui e espere aprovação.**

## Fase 2: linha de base
1. Rode `python3 scripts/build.py` na `main` e extraia o objeto de dados que ele injeta. Salve como
   `/tmp/baseline.json`, com as chaves ordenadas.
2. Salve também a saída completa de `python3 scripts/validate.py` em `/tmp/validate-antes.txt`.
3. `git tag pre-migracao` no commit atual da `main`.

Esse baseline é o critério de aceite da migração.

## Fase 3: formato novo
```
graph/entities/<id>.md     uma entidade por arquivo, uma única vez
graph/edges.csv            todas as ligações, uma única vez
maps/principal.yml            seleção: quais entidades e ligações este mapa mostra
```
**Entidades.** Frontmatter YAML com os campos curtos (`id`, `nome`, `tipo`, `grupo`, `estagio`, `institucional`,
`fontes`, `foto`, `credito`, `licenca`, `link_licenca`, `motivo_sem_foto`, `checado_em`, mais o que o inventário
achar). Corpo: o perfil em prosa, um cabeçalho por coluna de texto longo de `Perfis`, na mesma ordem. `institucional`
só com a lista aprovada na Fase 1; na dúvida, `false`. O `id` é o id atual da planilha.

**Ligações.** Um CSV só. Colunas mínimas: `id`, `source`, `target`, `label`, `status`, `fontes`, `nota_da_fonte`,
mais o que o inventário achar. Não crie um `edges.csv` por mapa e não use tabela Markdown (diff ilegível, e um `|`
no texto quebra a linha). Todo `id` de ligação é estável, único no repo inteiro (padrão `e-<source>-<target>-<n>`) e
gerado uma vez.

**Mapas.** `maps/principal.yml` com `slug`, `titulo`, `sujeito` (id da entidade central), `nota` e a lista explícita
de ids de entidade e de ligação que existem hoje. Critério automático de seleção fica para depois.

**Regras.** Os campos vêm do inventário: não invente, não renomeie. A tradução coluna → campo é 1 para 1. Texto
longo nunca entra no frontmatter. Preserve quebras de linha e acentuação.

Escreva `data/SCHEMA.md`: cada campo, tipo, obrigatoriedade, frontmatter ou corpo, e de qual coluna veio.

## Fase 4: script de migração
`scripts/migrate_xlsx.py` lê `data/mapa.xlsx` e escreve `graph/` e `maps/principal.yml`. Roda uma vez, é determinístico
e copia valor por valor, sem interpretar. Depois, mova a planilha para `data/legado/mapa-2026-10.xlsx` e registre no
`SCHEMA.md` que ela é histórico, não fonte.

## Fase 5: build e validador lendo o corpus
1. `scripts/build.py` monta o site a partir de `graph/` filtrado pela seleção em `maps/`. Mais nada do build muda.
2. `scripts/validate.py` passa a ler o corpus, **com os mesmos códigos de regra**. O V9 (fórmula do `Resumo`)
   deixa de existir junto com a aba; registre isso. Ajuste a mensagem da checagem de sincronia do CI, que cita
   `data/mapa.xlsx`, e a dependência que o CI instala (se precisar de PyYAML, pergunte antes).
3. Re-chaveie `data/fila-f7.md` por `id` de ligação, sem mudar o conteúdo dos lotes.
4. Atualize no mesmo PR: `CLAUDE.md` (tabela "Onde está a verdade" e "Estado em 1 minuto"), `CONTRIBUTING.md`,
   `EDITORIAL.md` §6 e a whitelist do `.gitignore`.

**Critérios de aceite, obrigatórios, comparados por código e mostrados a mim:**
- o objeto de dados gerado para `maps/principal.yml` é **idêntico** a `/tmp/baseline.json`;
- a saída do validador é igual a `/tmp/validate-antes.txt`, exceto o V9 e as referências de linha (que passam a
  ser `id`).
Qualquer diferença: não siga; mostre campo a campo e espere.

## Fora do escopo
A interface de juntar mapas, o mapa 2 e qualquer critério automático de seleção. Aqui só se torna isso possível.

## Pronto quando
- [ ] dados gerados idênticos ao baseline e validador com a mesma saída
- [ ] CI verde no PR; `index.html` em sincronia
- [ ] `SCHEMA.md` criado e `.md` novos na whitelist; planilha preservada em `data/legado/`
- [ ] um commit por fase, em português
- [ ] PR aberto com a tabela "o que entrou / o que ficou de fora e por quê", **sem merge**

## Não faça
- Editar texto de conteúdo (perfil, rótulo, fonte, nota), nem adicionar, remover ou fundir nó ou ligação.
- Mudar status de ligação ou estágio de nó.
- Decidir sozinho quais entidades são institucionais.
- Tocar em `notes`, `stages` ou no `<head>` do `index.html`.
- Apagar branch, mergear na `main` ou publicar.
- Instalar dependência pesada sem perguntar.

## Pare e pergunte quando
- o baseline não bater;
- o inventário revelar dado ambíguo ou contraditório;
- o validador acusar violação que exija decisão editorial;
- qualquer passo exigir mudar conteúdo para funcionar.
