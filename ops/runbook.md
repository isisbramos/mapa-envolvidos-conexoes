# Runbook: o que já quebrou e como se resolveu

> last-reviewed: 2026-11-15 · um caso por seção, mais recente primeiro. Sem nome de pessoa, e-mail ou credencial.

Formato: sintoma, causa, como diagnosticar, correção, como evitar.

## 2026-11-15: `README.md` de subpasta escapava do `.gitignore`

- **Sintoma:** depois de criar uma pasta privada com notas (`docs/historico/`), o `git status` mostrou a pasta
  inteira como não rastreada (`?? docs/`). Um `git add -A` mandaria notas privadas para o repo público.
- **Causa:** a whitelist tinha `!README.md` sem âncora. Sem `/`, o padrão vale em qualquer nível, então um
  `README.md` (ou `CLAUDE.md`, `EDITORIAL.md`, `CONTRIBUTING.md`) em subpasta deixava de ser ignorado.
- **Diagnóstico:** `git check-ignore -v <arquivo>`. Se não imprime nada, o arquivo não está ignorado.
- **Correção:** as entradas da raiz passaram a ser ancoradas (`!/README.md` etc.). Arquivos de subpasta têm
  entrada própria e explícita (`!context/README.md`, `!ops/*.md`).
- **Evitar:** depois de criar qualquer `.md` privado, rodar `git status` e `git check-ignore -v`. Nunca `git add -A`
  sem ler o `git status` antes. Nome de índice privado: use `LEIA-ME.md`, que o `*.md` bloqueia.

## 2026-11-15: `git pull` no clone local falha com `index.lock` ("Operation not permitted")

- **Sintoma:** o `git pull --ff-only` abortou no meio e deixou a árvore pela metade (`index.html` modificado,
  `robots.txt` e `sitemap.xml` como não rastreados).
- **Causa:** o ambiente da sessão não pode apagar arquivos na pasta conectada, então o git não conseguiu remover o
  próprio `index.lock` nem trocar os arquivos rastreados.
- **Diagnóstico:** `ls .git/*.lock` e conferir que não há processo git rodando (`pgrep git`).
- **Correção:** pedir permissão de exclusão para a pasta, remover só os locks (depois de confirmar que não há
  processo git), conferir que os arquivos "modificados" são idênticos ao commit (`git diff` vazio contra o
  commit esperado), restaurar e rodar `git pull --ff-only` de novo.
- **Evitar:** antes de qualquer sessão no clone local, `git pull --ff-only` (regra no `CLAUDE.md`), com a permissão
  de exclusão já concedida na pasta. Nunca apagar lock sem confirmar que nenhum git está rodando.
