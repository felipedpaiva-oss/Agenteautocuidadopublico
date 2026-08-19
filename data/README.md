# Schema dos dados

## `checkins-semanais.csv`

Uma linha por semana. Preencher no check-in guiado (chat) ou manualmente.

| Coluna | Tipo | Descrição |
|---|---|---|
| `data` | `AAAA-MM-DD` | Data do check-in (referente à semana que está terminando). |
| `peso_kg` | número | Peso em kg, da balança de bioimpedância. |
| `circunferencia_abdominal_cm` | número | Circunferência abdominal em cm, medida com fita métrica. |
| `horas_cardio` | número | Total de horas de exercício cardio na semana. |
| `horas_forca` | número | Total de horas de exercício de força na semana. |
| `episodios_descontrole_alimentar` | inteiro | Número de episódios de descontrole alimentar na semana. |
| `humor` | inteiro, -3 a 3 | Humor médio/predominante da semana. `-3` = muito para baixo/depressivo, `0` = estável, `3` = muito para cima/acelerado/eufórico. A escala é simétrica de propósito: tanto quedas quanto picos importam para observar padrões (relevante para a investigação de bipolaridade). |
| `observacoes` | texto livre | Qualquer contexto relevante da semana (eventos, mudanças, gatilhos). Opcional. |

Campos sem dado na semana devem ficar em branco — nunca estimados.

## Relatório de bioimpedância

Se quiser guardar o PDF/print do relatório de bioimpedância da balança, salve em
`data/bioimpedancia/AAAA-MM-DD.pdf` (crie a pasta na primeira vez). O check-in
semanal só pede peso e circunferência no CSV, mas o relatório completo fica
disponível para consulta futura.
