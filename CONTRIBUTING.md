# Como contribuir

Este mapa é uma estrutura viva — cresce conforme surgem novas informações, pessoas e conexões. Qualquer pessoa pode propor uma adição ou correção.

## Antes de propor algo

1. **Tenha uma fonte**: reportagem, transcrição de vídeo, decisão judicial, documento público. Sem fonte, não entra.
2. **Classifique corretamente**:
   - `"status": "doc"` → a fonte apresenta como fato, relatório da PF, decisão judicial ou similar.
   - `"status": "alleg"` → é hipótese, suspeita, ou o citado nega.
3. Se a pessoa/empresa citada nega a irregularidade, isso precisa continuar refletido no disclaimer e no tom da descrição (`desc`) — nunca apresente suspeita como condenação.

## Onde ficam os dados

**A fonte de verdade é a planilha `data/mapa.xlsx`.** Não edite o JSON dentro de `index.html` diretamente para mudar conteúdo (pessoa, conexão, perfil) — na próxima atualização a partir da planilha, qualquer edição manual ali é sobrescrita.

A planilha tem estas abas:

| Aba | Para quê |
|---|---|
| **Nodes** | Lista de pessoas/empresas/casos/instituições (`Id`, `Label`, `Type`, `Group`, `Description`). `Degree` é só referência visual na planilha — quem calcula de verdade é o script, a partir da aba Edges. |
| **Edges** | As conexões (`Source`, `Target`, `Label`, `Status` — "Documentado" ou "Alegado ou contestado"). `Source name`/`Target name` são fórmulas, não mexa. |
| **Perfis** | O painel detalhado de quem tem perfil pesquisado: bio, situação jurídica, onde atua, milícia, ressalvas, fontes, datas — e as 3 últimas colunas (`Foto (arquivo)`, `Crédito da foto`, `Link da fonte da foto`) controlam a foto que aparece no perfil. |
| **Notes** | Só documentação da planilha — não é lida pelo script (as notas do rodapé do site ficam direto no `index.html`, mudam raramente). |

Formato da coluna **Fontes** na aba Perfis: `Título da fonte URL` — várias fontes separadas por ` | `. Exemplo:

```
CNN Brasil 12/09/2025 https://www.cnnbrasil.com.br/... | Metrópoles https://www.metropoles.com/...
```

### Como atualizar o site a partir da planilha

1. Edite `data/mapa.xlsx` (adicionar pessoa → aba Nodes; conexão → aba Edges; detalhar perfil → aba Perfis).
2. Rode o script de build:
   ```bash
   python3 scripts/build.py
   ```
   Ele regenera o bloco JSON dentro de `index.html` e avisa quais nós foram adicionados/removidos.
3. Teste localmente (veja abaixo) antes de subir.
4. Commit de `data/mapa.xlsx` **e** `index.html` juntos, push — o deploy na Vercel é automático.

Se preferir não mexer na planilha você mesma, é só me mandar o arquivo `.xlsx` atualizado (ou me dizer o que mudar) que eu rodo o resto.

### Adicionando foto de alguém

Preencha as 3 colunas no fim da aba Perfis para a pessoa: nome do arquivo (ex. `fulano.jpg`, que precisa existir em `photos/`), o crédito (ex. "Agência Senado · uso livre") e o link da fonte. Prefira sempre Wikimedia Commons ou fotos oficiais de domínio público/licença aberta — veja `photos/CREDITS.md` para o padrão já usado.

## Como propor

- **Pull request**: edite `data/mapa.xlsx`, rode `scripts/build.py`, abra PR descrevendo a fonte da informação nova.
- **Issue**: se não quiser mexer na planilha, abra uma issue descrevendo a pessoa/conexão e a fonte — alguém (ou eu) incorpora.

## Rodando localmente para testar

```bash
npx serve .
```

Abra `http://localhost:3000` e confira se o novo nó/conexão aparece certo antes de abrir o PR.
