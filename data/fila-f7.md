# Fila do F7 (item A2 do roadmap)

> last-reviewed: 2026-11-19

Fila de trabalho para fechar a regra F7: toda ligação "Alegado ou contestado" precisa de 2 fontes
independentes na própria ligação. As "Reportado" seguem apoiadas nas fontes do perfil das duas pontas e
**não entram** aqui. Prioridade e contexto: `data/roadmap.md`. Regras de fonte: `EDITORIAL.md` §1 e §2.

**Objetivo e critério de saída:** V7 = 0. No mesmo PR, `EXIGIR_FONTE_NA_LIGACAO = True` em
`scripts/validate.py`, e a regra passa a bloquear no CI. Isso destrava A3 e, depois, a abertura ao público.

## Ponto de partida

71 ligações abaixo do mínimo. Uma 72ª tem 2 fontes próprias, mas as duas remetem à mesma apuração, então falha
na independência (F3): é o item A5 do roadmap, decisão da dona, fora desta fila.

As linhas abaixo são da aba `Edges` e foram conferidas em 15/11 contra o `validate.py` (71 de 71 batem).
**Inserir ou apagar linha na aba desloca os números.** Antes de abrir um lote, reconfira: copie
`scripts/validate.py` para fora do repo, troque `EXIGIR_FONTE_NA_LIGACAO` para `True` e rode; cada
ligação faltante sai com o número da linha.

## Protocolo por ligação

1. **Fontes que já estão no perfil.** Veja se alguma das duas pontas já cita uma fonte que sustenta a
   linha. É o caminho mais barato.
2. **Abrir cada URL antes de registrar** (F4). Não se cita como lido o que não foi aberto. Paywall: a
   dona cola o texto.
3. **Independência (F3).** URL diferente **e** apuração própria. Republicação de agência ou de outro veículo
   não conta. Se as duas remetem à mesma apuração, o caso vai para `Nota da fonte`.
4. **Texto x fonte.** A descrição só pode dizer o que a fonte sustenta. Na rodada do PR #8, 4 de 7 textos
   diziam mais do que a fonte.
5. **Sem 2ª fonte independente**, três saídas, nesta preferência: rebaixar para "Reportado" (só se a fonte
   for registro oficial que apresenta o fato); reescrever para o que a fonte sustenta; cortar. Nunca manter
   "Alegado" com uma fonte só depois que o F7 virar erro.
6. **Registro.** Colunas `Fontes` e `Nota da fonte` da aba `Edges`; depois `build.py` e `validate.py` sem erro.

Quem decide é a dona do projeto. A sessão propõe a fonte, abre, compara e registra o que ela aprovar.
As decisões 2, 3 e 4 do roadmap (rebaixar ou cortar, paywall, ritmo) valem para toda a fila.

## Lotes

Um lote = um PR = um review. Ordem por peso do dano (ligação mais exposta) e por fonte já disponível.
Lotes pequenos podem ser juntados: estimativa de 6 a 8 PRs. Os mesmos veículos aparecem em várias ligações,
então o número de URLs únicas deve ser bem menor que 142.

| Lote | Perfil do lote | Qtd | Linhas da aba `Edges` | Estado |
|---|---|---|---|---|
| 1 | Núcleo do site, com mais cobertura pública. **Revisão extra** | 7 | 60, 61, 62, 121, 122, 123, 124 | Fechado, PR #21 (16/11) |
| 2 | Testemunhas já citadas; 2ª fonte provável no perfil | 7 | 56, 100, 105, 106, 107, 108, 182 | Fechado, PR #24 (19/11) |
| 3a | Ligações institucionais, parte com fonte única de jornal | 8 | 33, 34, 35, 110, 114, 115, 129, 168 | Fechado, PR #26 (19/11) |
| 3b | Maior bloco; muita fonte de relatório da PF | 10 | 134, 135, 136, 137, 138, 145, 146, 147, 150, 152 | Aberto |
| 4 | Mensagens e relatórios da PF | 10 | 130, 153, 157, 158, 159, 162, 164, 201, 210, 212 | Aberto |
| 5 | O mais sensível. **Revisão extra** | 7 | 65, 66, 67, 68, 70, 73, 74 | Aberto |
| 6a | Empresas e holdings; uma já tem 1 URL | 9 | 25, 26, 27, 141, 167, 185, 186, 189, 191 | Aberto |
| 6b | Emendas e outro caso; uma já tem 1 URL | 5 | 170, 171, 177, 178, 179 | Aberto |
| 6c | Uma já tem 1 URL, com texto corrigido no PR #8 | 5 | 97, 98, 195, 197, 198 | Aberto |
| 6d | Menor volume | 3 | 7, 11, 12 | Aberto |

Total: 71. Ao fechar um lote, atualize a coluna "Estado" (PR e data) e o `last-reviewed` deste arquivo.

- [2026-11-19] Linha 182 (lote 2) foi rebaixada para "Reportado" (decisão da dona) e saiu do universo
  "Alegado ou contestado" — por isso não entra mais na contagem do V7, mesmo citada na linha do lote 2 acima.
- [2026-11-19] Linhas 56, 105, 106 (lote 2) ficaram fechadas com 1 fonte só e nota de apuração única — ver
  `Nota da fonte` na planilha. O validador continua contando como "abaixo de 2 fontes" (V7); é esperado.
- [2026-11-19] Linha 168 (lote 3a) fechada com 1 fonte só (apuração do PlatôBR, só repercutida por outros
  veículos) — mesmo caso das três linhas acima.

## Riscos

| Risco | Mitigação |
|---|---|
| Texto derivar da fonte de novo | Passo 4: comparação lado a lado |
| URL que não abre ou não existe | Passo 2: nenhuma URL entra sem ser aberta |
| Republicação contada como 2ª fonte | Passo 3 e `Nota da fonte` |
| Fato mudar durante o trabalho (o caso é ativo) | Data de checagem por lote, na tabela do PR |
| Cortar deixa o mapa mais pobre | Aceito: mais vale faltar do que errar (F5) |
| F7 ficar em aviso para sempre | Critério de saída explícito; conferir a cada lote |
| Número de linha envelhecer | Reconferir contra o validador antes de cada lote |
