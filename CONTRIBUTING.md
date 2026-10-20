# Como contribuir

Este mapa é uma estrutura viva — cresce conforme surgem novas informações, pessoas e conexões. Qualquer pessoa pode propor uma adição ou correção.

## Antes de propor algo

1. **Tenha uma fonte**: reportagem, transcrição de vídeo, decisão judicial, documento público. Sem fonte, não entra.
2. **Classifique corretamente**:
   - `"status": "doc"` → a fonte apresenta como fato, relatório da PF, decisão judicial ou similar.
   - `"status": "alleg"` → é hipótese, suspeita, ou o citado nega.
3. Se a pessoa/empresa citada nega a irregularidade, isso precisa continuar refletido no disclaimer e no tom da descrição (`desc`) — nunca apresente suspeita como condenação.

## Onde ficam os dados

Os dados do mapa (pessoas, empresas, conexões) estão embutidos em `index.html`, dentro de uma tag:

```html
<script id="graph-data" type="application/json">
  { "groups": [...], "nodes": [...], "links": [...], "notes": {...} }
</script>
```

É só esse bloco JSON que precisa ser editado — o resto do arquivo é a aplicação (visualização, estilos, lógica) e normalmente não muda.

### Adicionar uma pessoa, empresa ou caso (`nodes`)

```json
{
  "id": "slug_unico",
  "label": "Nome exibido",
  "type": "Pessoa",
  "group": "Nome de um dos grupos já existentes",
  "desc": "Descrição curta e factual, com a fonte implícita ou citada",
  "degree": 1
}
```

- `type`: um de `Pessoa`, `Empresa`, `Casa ou ativo`, `Instituição ou caso`.
- `group`: precisa bater com um dos nomes em `"groups"` no topo do JSON (ou você pode propor um grupo novo lá).
- `degree`: número de conexões do nó — depois de adicionar os `links`, ajuste esse número (é o que define o tamanho do círculo no mapa).

### Adicionar uma conexão (`links`)

```json
{
  "source": "id_do_no_1",
  "target": "id_do_no_2",
  "label": "Como essa conexão é descrita",
  "status": "doc"
}
```

`source`/`target` precisam ser `id`s que já existem em `nodes`.

## Como propor

- **Pull request**: edite o JSON em `index.html`, abra PR descrevendo a fonte da informação nova.
- **Issue**: se não quiser editar o código, abra uma issue descrevendo a pessoa/conexão e a fonte — alguém (ou eu) incorpora.

## Rodando localmente para testar

```bash
npx serve .
```

Abra `http://localhost:3000` e confira se o novo nó/conexão aparece certo antes de abrir o PR.
