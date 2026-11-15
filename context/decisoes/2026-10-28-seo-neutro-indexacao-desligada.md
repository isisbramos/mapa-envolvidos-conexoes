# SEO neutro com a indexação desligada

> Data: 2026-10-28 · Status: vigente (abertura da indexação segue pendente)

**Contexto.** O site estava com `noindex` e sem `robots.txt` nem `sitemap.xml` (404). Antes de abrir para o Google,
a camada de SEO precisava existir, para não indexar a versão errada.

**Decisão.**
- Título e descrição **neutros**, sem o nome do candidato; o domínio mantém o nome.
- Só a **home** é indexável; os perfis por pessoa não ganham página própria no buscador.
- Entram `canonical`, JSON-LD, `robots.txt` e `sitemap.xml` (entre os PRs #1 a #5), mas o **`noindex, nofollow` continua ligado**.
- Abrir a indexação e mudar a assinatura do site acontecem **juntos**, num PR só, e só depois do F7 completo (A3) e de
  leitura jurídica.

**Alternativas descartadas.** Indexar uma página por pessoa (ampliaria a busca pelo nome de cada citado); abrir a
indexação antes do F7.

**Por quê.** Abrir a indexação muda a descoberta, não a publicação, mas expõe nomes em busca. É a mudança menos
reversível do projeto: por isso depende de condições, não de data.

**Consequências.** `/robots.txt` e `/sitemap.xml` respondem 200 e `noindex` segue no `<head>`. O racional da
assinatura fica fora do repo (público).

**Onde se executa.** `<head>` do `index.html` (o `build.py` não toca), `robots.txt`, `sitemap.xml`.
