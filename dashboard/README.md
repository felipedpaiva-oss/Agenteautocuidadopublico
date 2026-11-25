# Dashboard visual

`index.html` é o painel publicado como Artifact (link fixo, ver `CLAUDE.md` →
"Dashboard visual"). É um HTML autocontido (sem dependências externas) com os
dados de `data/bioimpedancia.csv` e `data/checkins-semanais.csv` **embutidos
diretamente no `<script>`** — não lê os CSVs em tempo real.

## Como atualizar (toda vez que um check-in é registrado)

0. Antes de qualquer outra coisa no check-in, leia o array `priorities` como
   está agora (as 3 prioridades da semana anterior) e pergunte ao usuário
   como foi a execução de cada uma — isso vem antes até de pedir o relatório
   de bioimpedância (ver `CLAUDE.md`, item 3). Só depois de colher essa
   resposta o array é sobrescrito com as prioridades da nova semana.
1. Depois de acrescentar as novas linhas aos CSVs, edite os arrays `bio` e
   `checkins` no `<script>` deste arquivo, adicionando os novos registros (no
   mesmo formato dos existentes — todos os campos do schema em
   `data/README.md`).
2. Publique de novo com a ferramenta Artifact, usando `url` igual à URL já
   publicada (guardada em `CLAUDE.md`) para atualizar no mesmo link em vez de
   criar um novo.
3. As seções de texto ("Análise de padrões" — olha todo o histórico, não só a
   semana atual — e "Prioridades da semana" — compara a análise + comentários
   do chat contra as metas de `data/README.md`) precisam ser reescritas à mão
   a cada semana com base na conversa do check-in — só os números/gráficos
   são recalculados automaticamente a partir dos arrays.
