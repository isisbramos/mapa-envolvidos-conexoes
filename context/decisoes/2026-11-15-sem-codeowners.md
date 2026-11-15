# Não criar CODEOWNERS

> Data: 2026-11-15 · Status: vigente · Reabrir quando houver um segundo revisor

**Contexto.** O plano original de migração previa um `CODEOWNERS` exigindo a revisão da dona em `graph/`, `maps/`
e `EDITORIAL.md`. Ele nunca foi criado.

**Decisão.** Não criar o `CODEOWNERS`. O controle vem de outra camada: proteção da `main` exigindo pull request e
o check `validar` verde (passo 1.4 de `data/plano-organizacao.md`), e a regra de produção de que merge só com
aprovação explícita da dona.

**Alternativas descartadas.**
- Criar o `CODEOWNERS` com a dona como dona de tudo.
- Criar e exigir "revisão de code owner" na proteção da `main`.

**Por quê.** O `CODEOWNERS` só tem efeito quando alguém precisa pedir a revisão de outra pessoa. Com uma dona só,
ela seria a autora e a revisora do mesmo PR, e o GitHub não deixa o autor aprovar o próprio PR. Exigir a revisão de
code owner travaria o próprio merge dela. Sem a exigência, o arquivo seria só um comentário.

**Consequências.**
- A trava real é a proteção da `main` e o CI.
- Quando entrar um segundo revisor, esta decisão é reaberta: aí o `CODEOWNERS` passa a ter função.
- O prompt de migração (`ops/migracao-corpus-unico.md`) não cria `CODEOWNERS`.

**Onde se executa.** Configuração de branch protection no GitHub (fora do repo) e `data/plano-organizacao.md`.
