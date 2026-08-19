# Agente de autocuidado e equilíbrio de vida

Agente pessoal (conversacional, via Claude) para apoio em autocuidado, foco em
metas pessoais e equilíbrio de vida — com atenção específica a TDAH, autismo
nível 1, altas habilidades e investigação de bipolaridade.

## Estrutura

- `CLAUDE.md` — perfil e instruções de como o agente deve se comportar.
- `docs/autocuidado.md` — guia dos 9 pilares de autocuidado, mapeados para cada
  condição.
- `data/bioimpedancia.csv` — histórico das medições da balança (peso, gordura,
  massa muscular, água, gordura visceral etc.), extraído do relatório que você
  manda em anexo no chat. Relatórios originais ficam em `data/bioimpedancia/`.
- `data/checkins-semanais.csv` — histórico semanal (circunferência abdominal,
  horas de cardio/força, episódios de descontrole alimentar, humor).
  Schema completo em `data/README.md`.

## Como funciona

- Converse normalmente pedindo apoio em qualquer um dos pilares de autocuidado.
- Toda semana (terça-feira, 6h de Brasília) uma rotina agendada reabre a
  conversa e conduz o check-in semanal, registrando os dados no CSV.
- Peça para ajustar horário/frequência dos lembretes a qualquer momento.
