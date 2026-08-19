# Guia de autocuidado — os 9 pilares

Referência para o agente usar nas conversas. Cada pilar liga por que ele importa
especificamente para TDAH, autismo nível 1 (hipersensibilidade), altas
habilidades e (potencial) bipolaridade — e formas de apoiar sem ser genérico.

## 1. Sono de qualidade
- **TDAH**: privação de sono piora drasticamente foco e regulação emocional no
  dia seguinte — efeito maior do que em neurotípicos.
- **Bipolar (potencial)**: sono irregular é gatilho conhecido de episódios de
  humor (tanto para baixo quanto para cima). Horário de sono consistente é uma
  das intervenções não-medicamentosas mais fortes.
- **Autismo/hipersensibilidade**: ambiente de sono precisa ser sensorialmente
  controlado (luz, som) — não é só "dormir 8h", é dormir num ambiente regulado.
- Apoio: perguntar sobre horário de dormir/acordar, não só duração. Notar
  variações grandes de horário como sinal de alerta, junto com o campo `humor`.

## 2. Exercício físico com frequência
- Base de dados já cobre isso (`horas_cardio`, `horas_forca`). Cardio ajuda
  regulação de humor e de dopamina (TDAH); força ajuda composição corporal e
  também tem efeito antidepressivo.
- Apoio: comparar semana a semana, comemorar consistência mais do que volume.

## 3. Vida social ativa (geral, evitar isolamento)
- TDAH e episódios de humor tendem a levar a isolamento reativo. Autismo pode
  fazer com que socializar canse mais rápido (necessidade de recuperação depois).
- Apoio: perguntar de vez em quando "quando foi o último encontro social?" sem
  cobrança — é dado, não meta rígida.

## 4. Vida social ativa com amigos de altas habilidades
- Grupo pequeno e específico — perder contato é mais fácil e mais custoso
  (poucos pares que realmente entendem). Tratar como categoria separada do
  pilar 3.
- Apoio: se muito tempo sem contato com esse grupo específico, mencionar.

## 5. Alimentação saudável
- Ligado a `episodios_descontrole_alimentar`. TDAH e humor instável aumentam
  comer impulsivo/emocional. Não é questão de "força de vontade".
- Apoio: ao notar aumento de episódios, perguntar sobre contexto (estresse,
  sono, humor da semana) em vez de focar só na comida.

## 6. Evitar álcool
- Álcool interage mal com humor instável (pode piorar episódios depressivos e
  atrapalhar sono) e reduz ainda mais o controle de impulsos já desafiado pelo
  TDAH.

## 7. Evitar açúcar
- Picos/quedas de glicose pioram sintomas de desatenção e irritabilidade no
  TDAH. Fica mais fácil monitorar via `episodios_descontrole_alimentar` e
  `observacoes`.

## 8. Evitar dooming scroll no YouTube
- Padrão clássico de hiperfoco/procrastinação do TDAH combinado com busca de
  estímulo. Pode também ser sinal de humor baixo (usar como escape) ou de humor
  acelerado (dificuldade de desligar).
- Apoio: em vez de "para de rolar o feed", ajudar a identificar o gatilho
  (tédio, cansaço, evitação de alguma tarefa) e sugerir troca por algo de
  estímulo similar mas com corte natural (ex: alarme, app com limite).

## 9. Evitar excesso de estímulos sociais e sensoriais
- Autismo nível 1 com hipersensibilidade auditiva/visual: sobrecarga sensorial
  cumulativa ao longo do dia/semana leva a shutdown ou irritabilidade — mesmo
  que cada estímulo individual pareça pequeno.
- Apoio: ajudar a reconhecer sinais precoces de sobrecarga (irritabilidade,
  vontade de fugir de ambientes) e validar a necessidade de tempo de
  recuperação sensorial, sem culpa por "precisar se isolar um pouco".

---

Esses pilares não têm campo próprio no CSV semanal (fora os que já mapeiam
para cardio/força/descontrole/humor) — o registro deles acontece na conversa.
Se no futuro fizer sentido, pode-se adicionar um checklist diário simples
(`data/checklist-diario.csv`) para os pilares 1, 3, 4, 6, 7, 8, 9.
