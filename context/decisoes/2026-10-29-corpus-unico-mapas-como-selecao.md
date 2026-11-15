# Corpus único, mapas como seleção

> Data: 2026-10-29 · Status: **desenho decidido, execução pendente (B4)**

**Contexto.** Vai existir um segundo mapa ("Com quem anda…", de prefeitos candidatos), e o leitor deve poder juntar
dois mapas e ver a união. A proposta de 28/10 previa uma pasta por mapa, cada uma com o seu `edges.csv`.

**Decisão.** Cada entidade e cada ligação existe **uma única vez** no repo; um mapa é um recorte (seleção) sobre esse
corpus, nunca um container com cópia própria.
- Entidades: um arquivo `.md` por entidade, com frontmatter para os campos curtos e o perfil em prosa no corpo.
- Ligações: um único `edges.csv`, com `id` estável e único.
- Mapas: um arquivo de seleção por mapa (ids de entidades e de ligações).
- Flag `institucional` nas entidades: órgãos (polícia, tribunais, receita) não contam como ponte entre redes.

**Alternativas descartadas.** Um `edges.csv` por mapa (o mesmo perfil existiria em dois lugares, divergiria, e a
união duplicaria); banco de dados (o Git já dá diff, review e histórico imutável); manter o `.xlsx` (sem diff nem
merge).

**Por quê.** Se o mesmo perfil existe em dois lugares, em seis meses ele diz coisas diferentes em dois sites, e a
credibilidade vai junto.

**Em aberto (decisão 11 do `data/roadmap.md`).** O plano de 28/10 diz "nunca migrar com PRs editoriais em voo":
mistura refactor e conteúdo no mesmo diff. O A2 (fonte nas ligações) são vários PRs editoriais seguidos. A migração
tem de mudar "nem uma vírgula" de conteúdo, e o critério de aceite é o JSON gerado idêntico ao de antes.

**Onde se executa.** Prompt de migração (interino, no Projeto claude.ai); ainda não há arquivo no repo.
