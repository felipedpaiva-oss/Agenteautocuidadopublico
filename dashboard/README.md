# Dashboard visual

`index.html` é o painel publicado como Artifact (link fixo, ver `CLAUDE.md` →
"Dashboard visual"). É um HTML autocontido (sem dependências externas) com os
dados de `data/bioimpedancia.csv` e `data/checkins-semanais.csv` **embutidos
diretamente no `<script>`** — não lê os CSVs em tempo real.

## Como atualizar (toda vez que um check-in é registrado)

1. Depois de acrescentar as novas linhas aos CSVs, edite os arrays `bio` e
   `checkins` no `<script>` deste arquivo, adicionando os novos registros (no
   mesmo formato dos existentes — todos os campos do schema em
   `data/README.md`).
2. Publique de novo com a ferramenta Artifact, usando `url` igual à URL já
   publicada (guardada em `CLAUDE.md`) para atualizar no mesmo link em vez de
   criar um novo.
3. As seções de texto ("Leitura integrada", "Tendência de longo prazo" é
   parcialmente automática, "Prioridades da semana") precisam ser reescritas
   à mão a cada semana com base na conversa do check-in — só os números/
   gráficos são recalculados automaticamente a partir dos arrays.
