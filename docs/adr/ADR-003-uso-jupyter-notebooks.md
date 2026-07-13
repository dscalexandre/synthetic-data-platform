# ADR-003 — Usar Jupyter Notebooks para exploração e experimentação

## Status

Aceito.

## Contexto

- No `synthetic-data-engine`, notebooks combinam código, resultados visuais e
  documentação no mesmo artefato.
- Facilitam a análise exploratória e a investigação iterativa dos dados.
- Permitem visualizar o comportamento e a distribuição das variáveis por
  meio de gráficos.
- Ajudam a identificar padrões, tendências, correlações, valores ausentes e
  possíveis anomalias.
- São uma ferramenta consolidada nas áreas de ciência e engenharia de dados.
- Suportam prototipagem rápida sem a necessidade imediata de refatoração para
  código modular.

## Decisão

Usar notebooks Jupyter como ferramenta principal para análise exploratória,
preparação, experimentação, avaliação e documentação do fluxo atual. Organizar a
execução em dois artefatos sequenciais:

- `notebooks/01_data_analysis.ipynb` para consolidar os CSVs particionados,
  inspecionar qualidade, transformar datas, analisar `age_group` e exportar os
  dados processados;
- `notebooks/02_gaussian_copula.ipynb` para modelar, gerar e avaliar os dados
  sintéticos.

Os notebooks devem poder ser executados a partir da raiz do repositório ou do
diretório `notebooks/`, ajustando o diretório de trabalho para a raiz do
projeto.

## Consequências positivas

- Reduz o tempo de experimentação e validação de hipóteses.
- Mantém uma documentação viva, alinhada ao código e aos resultados.
- Oferece retorno imediato após a execução de cada etapa da análise.
- Permite comparar transformações, modelos e resultados de forma interativa.
- Facilita a comunicação com as partes interessadas por meio de tabelas,
  gráficos e outros resultados visuais.
- Reúne explicações, código e evidências da análise em uma sequência narrativa.

## Consequências negativas

- A execução fora de ordem pode produzir resultados inconsistentes.
- Diferenças no estado do kernel dificultam a reprodução de uma sessão.
- A lógica de preparação e avaliação permanece menos reutilizável enquanto não
  for extraída para módulos Python.

## Alternativa considerada

- Scripts Python com logging: abordagem mais rigorosa, mas menos adequada para
  exploração.
