# Schema dos dados

## `bioimpedancia.csv`

Uma linha por medição, extraída do relatório em imagem/PDF que a balança gera
(o usuário manda o relatório em anexo no chat). Fonte única de verdade para
peso — não perguntar peso separadamente no check-in semanal.

| Coluna | Descrição |
|---|---|
| `data` | `AAAA-MM-DD`, data/hora da medição mostrada no relatório. |
| `peso_kg` | Peso (Kg). |
| `imc` | IMC. |
| `gordura_pct` | Gordura (%). |
| `peso_gordura_kg` | Peso da gordura (Kg). |
| `massa_muscular_esqueletica_pct` | Percentual da massa muscular esquelética (%). |
| `massa_muscular_esqueletica_kg` | Peso da massa muscular esquelética (Kg). |
| `massa_muscular_pct` | Registro de massa muscular (%). |
| `massa_muscular_kg` | Peso da massa muscular (Kg). |
| `agua_pct` | Água (%). |
| `agua_kg` | Peso da água (Kg). |
| `gordura_visceral` | Gordura visceral (índice). |
| `ossos_kg` | Ossos (Kg). |
| `metabolismo_kcal` | Metabolismo basal (kcal). |
| `proteina_pct` | Proteína (%). |
| `obesidade_pct` | Obesidade (%). |
| `idade_metabolica` | Idade metabólica. |
| `lbm_kg` | LBM — massa magra (Kg). |
| `idade_real` | Idade real, como mostrada no relatório (referência, não muda). |
| `altura_cm` | Altura (cm), como mostrada no relatório (referência, não muda). |

**Importação de histórico via app**: se o usuário mandar uma planilha exportada
do app da balança (`.xls`/`.xlsx`/`.csv`), mesclar com o CSV existente por
`data`, sem duplicar. Esse export não traz `gordura_visceral` (só aparece no
relatório em imagem) — deixar em branco nas linhas importadas assim, sem
estimar. Guardar o arquivo original em `data/bioimpedancia/` para referência.
Datas do export costumam vir sem ano (`MM-DD`); inferir o ano pelo intervalo
declarado no cabeçalho da planilha.

O relatório original (imagem/PDF) fica salvo em
`data/bioimpedancia/AAAA-MM-DD.{png,pdf}` para consulta futura.

**Como preencher**: quando o usuário anexar o relatório no chat, ler os valores
diretamente da imagem (todos os campos listados acima aparecem nela) — nunca
pedir esses números por texto, e nunca estimar um valor que não apareça
claramente no relatório (deixar em branco).

## `checkins-semanais.csv`

Uma linha por semana. Preenchido no check-in guiado (chat), com base no que o
usuário relata + no relatório de bioimpedância do mesmo dia (via `data`, que
serve de chave para juntar os dois CSVs).

| Coluna | Tipo | Descrição |
|---|---|---|
| `data` | `AAAA-MM-DD` | Data do check-in. Deve bater com a `data` do registro correspondente em `bioimpedancia.csv` quando houver relatório na mesma sessão. |
| `circunferencia_abdominal_cm` | número | Circunferência abdominal em cm, medida com fita métrica. |
| `horas_cardio` | número | Total de horas de exercício cardio na semana. |
| `horas_forca` | número | Total de horas de exercício de força na semana. |
| `episodios_descontrole_alimentar` | inteiro | Número de episódios de descontrole alimentar na semana. |
| `alcool_doses_sociais` | inteiro | Doses de álcool consumidas em ocasiões sociais na semana. Distinção proposital: o usuário trata consumo social (aceitável em moderação, ~2-3 doses/semana) e consumo sozinho (pilar a evitar/observar) como padrões diferentes — ver `docs/autocuidado.md`, pilar 6. |
| `alcool_doses_sozinho` | inteiro | Doses de álcool consumidas sozinho na semana. |
| `sono_qualidade` | inteiro, 0 a 10 | Autorrelato de qualidade média do sono na semana. `0` = pior sono possível, `10` = sono perfeito. Um campo só (não horas + qualidade separados) por decisão do usuário — ambos seriam subjetivos mesmo, então menos atrito pesa mais que precisão extra. |
| `humor` | inteiro, -3 a 3 | Humor médio/predominante da semana. `-3` = muito para baixo/depressivo, `0` = estável, `3` = muito para cima/acelerado/eufórico. Escala simétrica de propósito: quedas e picos importam (relevante para investigação de bipolaridade). |
| `observacoes` | texto livre | Contexto relevante da semana (eventos, mudanças, gatilhos). Opcional. |

Campos sem dado na semana devem ficar em branco — nunca estimados.

## Análise de padrões ao final do check-in

Depois de registrar os dois CSVs (bioimpedância + check-in semanal), fechar o
check-in com **uma única análise** olhando todo o histórico acumulado — não é
mais "leitura do dia" separada de "tendência de longo prazo", virou uma coisa
só. Objetivo: achar padrões, tendências e relações de causa e efeito entre os
indicadores ao longo do tempo, e sinalizar sinais de alerta. Exemplos
(fictícios, só pra ilustrar o tipo de leitura esperada, não são regras fixas):
- "Nas semanas em que o consumo de álcool subiu, o peso também subiu na
  semana seguinte."
- "Oscilações grandes de humor parecem antecipar aumento de episódios de
  descontrole alimentar, que por sua vez pesam no peso."

Como fazer:
- Olhar a série completa de `bioimpedancia.csv` e `checkins-semanais.csv`
  (todo o histórico, não só o último ponto vs. o anterior) — peso, gordura
  corporal, massa muscular, circunferência, cardio/força, descontroles,
  álcool (social x sozinho), sono, humor.
- Procurar correlações temporais plausíveis entre indicadores (ex: humor vs.
  descontroles, álcool vs. peso, sono vs. humor, atividade física vs.
  peso/humor), não só comparar a semana atual com a anterior.
- Sinalizar extremos e sinais de alerta (humor muito alto ou muito baixo,
  vários check-ins seguidos fora da meta de algum indicador — ver "Metas de
  equilíbrio" abaixo) sem alarmismo e sem diagnosticar.
- Gordura visceral não é mais acompanhada por pedido do usuário (17/11/2026)
  — ainda é lida e guardada no CSV se aparecer no relatório, só não entra na
  análise nem no dashboard.
- Ligar com `docs/autocuidado.md` quando fizer sentido.

Regra: é leitura de padrão, não diagnóstico nem prescrição médica. Direto ao
ponto (ver `CLAUDE.md` sobre tom) — sem limite rígido de frases, mas sem
enrolação; o tamanho certo é o que o padrão encontrado pedir. Se o histórico
ainda for curto pra uma leitura confiável, dizer isso e seguir.

## Metas de equilíbrio (referência para as prioridades da semana)

Valores que o próprio usuário definiu como equilibrados. Usados para decidir
as **3 prioridades da semana** (ver `dashboard/README.md`): a análise de
padrões acima, somada a qualquer comentário do usuário no chat, é comparada
contra estas metas para escolher o que priorizar — não é só "qual número está
pior", é também "qual tem mais sinal de causa na análise de padrões".

| Indicador | Meta |
|---|---|
| Humor | 0 (estável) |
| Peso | 83 kg |
| Qualidade do sono | 8/10 |
| Circunferência abdominal | 92 cm |
| Atividade física (cardio + força) | 5 a 10 horas/semana |
| Episódios de descontrole alimentar | 2 ou menos por semana |
| Álcool (total na semana) | 2 doses ou menos; 3-4 numa semana isolada é tolerável |

Os demais indicadores (gordura %, massa muscular %, água, gordura visceral
etc.) não têm meta — entram na análise de padrões, mas não nas prioridades.
