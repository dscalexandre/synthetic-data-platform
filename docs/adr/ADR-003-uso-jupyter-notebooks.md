# ADR-003 — Uso de Jupyter Notebooks como artefato principal de desenvolvimento

## Status

Aceita.

## Contexto

- Notebooks combinam código, resultados visuais e documentação no mesmo
  artefato.
- Facilitam a análise exploratória e a investigação iterativa dos dados.
- Permitem visualizar o comportamento e a distribuição das variáveis por
  meio de gráficos.
- Ajudam a identificar padrões, tendências, correlações, valores ausentes e
  possíveis anomalias.
- São uma ferramenta consolidada na comunidade de Data Science e Engenharia
  de Dados.
- Suportam prototipagem rápida sem a necessidade imediata de refatoração para
  código modular.

## Decisão

Usar notebooks Jupyter como ferramenta primária para análise exploratória,
experimentação e documentação.

## Consequências positivas

- Reduz o tempo de experimentação e validação de hipóteses.
- Mantém uma documentação viva, alinhada ao código e aos resultados.
- Oferece retorno imediato após a execução de cada etapa da análise.
- Permite comparar transformações, modelos e resultados de forma interativa.
- Facilita a comunicação com stakeholders por meio de tabelas, gráficos e
  outros resultados visuais.
- Reúne explicações, código e evidências da análise em uma sequência narrativa.
- Permite a rastreabilidade de experimentos pelo histórico de células.

## Alternativas consideradas

- Scripts Python com logging: abordagem mais rigorosa, mas menos adequada para
  exploração.
- R Markdown: utiliza outra linguagem e possui menor compatibilidade com o
  ecossistema SDV, baseado em Python.
- Papermill ou Ploomber: ferramentas de orquestração de notebooks mais
  adequadas para pipelines maduros.
