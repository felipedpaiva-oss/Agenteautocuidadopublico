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
| `humor` | inteiro, -3 a 3 | Humor médio/predominante da semana. `-3` = muito para baixo/depressivo, `0` = estável, `3` = muito para cima/acelerado/eufórico. Escala simétrica de propósito: quedas e picos importam (relevante para investigação de bipolaridade). |
| `observacoes` | texto livre | Contexto relevante da semana (eventos, mudanças, gatilhos). Opcional. |

Campos sem dado na semana devem ficar em branco — nunca estimados.

## Leitura integrada ao final do check-in

Depois de registrar os dois CSVs (bioimpedância + check-in semanal), fechar o
check-in com uma leitura integrada curta, cruzando:

- Tendência de peso/gordura/massa muscular/gordura visceral (`bioimpedancia.csv`,
  comparando com a medição anterior).
- Circunferência abdominal (`checkins-semanais.csv`) — confirma ou destoa da
  tendência de gordura visceral?
- Cardio/força da semana — hipótese plausível para a tendência observada?
- Descontroles alimentares e humor — algum dos dois ajuda a explicar variação
  de peso/água/gordura? (ex: mais descontroles + humor baixo numa semana com
  peso subindo é diferente de peso subindo com tudo estável — pode ser
  retenção de água, ganho de massa muscular, etc.)
- Ligar com `docs/autocuidado.md` quando fizer sentido (ex: gordura visceral
  alta + sono ruim relatado na conversa).

Regra: é leitura de padrão, não diagnóstico nem prescrição médica. 2-4 frases,
direto ao ponto (ver `CLAUDE.md` sobre tom). Se não houver dado suficiente pra
uma leitura (ex: primeira medição, sem histórico prévio), dizer isso e seguir.
