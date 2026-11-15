# Analytics do site (Umami Cloud)

> last-reviewed: 2026-11-15 · conferido contra o `<head>` e o JS do `index.html` nessa data

No ar desde 22/10/2026, via deploy automático da Vercel. O que vale é o código: o script está no `<head>` do
`index.html` e o helper `track` no JS. Este arquivo explica o porquê e lista os eventos.

## Por que Umami
- **Gratuito**: plano free do Umami Cloud com 100 mil eventos por mês, 1 site e 6 meses de histórico.
- **Cookieless**: sem cookies, sem banner. Importa porque o site é político e visitar já pode indicar opinião
  política, dado sensível pela LGPD.
- O Vercel Web Analytics free só conta pageviews (50 mil eventos por mês, 1 mês de histórico); o Umami tem
  custom events.
- Descartado: GA4 (cookies e banner pela LGPD).

## Como está ligado
- Script no `<head>` com `data-domains` (só conta no domínio de produção; testes locais e previews da Vercel não
  entram nos números) e `data-do-not-track="true"` (respeita o Do Not Track do navegador).
- `track(name, data)` chama `window.umami.track` dentro de try/catch e falha em silêncio: o site funciona igual
  com adblock.
- O `build.py` não toca o `<head>`. Se alguém regenerar o `index.html` de outra forma, conferir que o script
  continua lá.
- Acesso: conta do Umami Cloud da dona do projeto. Login e identificadores de conta moram no vault privado, não
  aqui.

## Eventos
| Evento | Quando dispara | Dados enviados |
|---|---|---|
| `node_select` | Seleção de um nó (só ao trocar de nó) | `id`, `label`, `group` |
| `group_filter` | Clique num filtro de grupo | `group` |
| `status_filter` | Liga ou desliga um tipo de ligação | `status` (valores internos `doc` e `alleg`) |
| `list_open` | Abre a lista de envolvidos | `stage` (ou `all`) |
| `search_used` | Primeira busca da sessão com 3 ou mais caracteres | nada: o texto digitado **não** é enviado, de propósito |
| `about_open` | Abre o "Sobre" | nada |

Onde ver: Umami, abrindo o site → *Overview* (visitas, origem, país, dispositivo) e aba *Events*.

## Atenção
- Os valores `doc` e `alleg` são códigos internos do status "Reportado" e "Alegado ou contestado". O nome público
  mudou; o código não, para não quebrar o histórico dos eventos.
- Qualquer branch longa (a linha do tempo, por exemplo) deve ser atualizada com a `main` antes de publicar, senão o
  script do analytics some do site.
- Evento novo: não enviar texto livre digitado pela pessoa nem nada que a identifique.
- Se o site passar de 100 mil eventos por mês, considerar somar o Cloudflare Web Analytics (grátis, só pageviews)
  como reserva.
