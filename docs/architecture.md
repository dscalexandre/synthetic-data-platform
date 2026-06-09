# Arquitetura da Plataforma de Dados Sintéticos

## Objetivo da solução

A plataforma tem como objetivo oferecer uma base inicial para geração de dados sintéticos usando SDV. O foco é permitir a ingestão de dados brutos, preparação e transformação, e geração exploratória de dados sintéticos dentro de um repositório estruturado de notebooks.

## Componentes principais do projeto

### Ingestão / saída de dados

- `data/raw`: local destinado ao armazenamento dos dados originais recebidos ou estudados.
- `data/processed_data`: local destinado ao armazenamento de dados transformados e preparados para análise ou geração sintética.
- `output`: local para artefatos gerados, resultados de experimentos e possíveis artefatos de modelo.

### Preparação de dados

- O projeto usa notebooks Jupyter para explorar e preparar dados.
- A preparação inclui limpeza, transformação e formatação dos dados de forma compatível com os modelos SDV.
- A lógica de preparação está prevista para ser documentada e experimentada nos notebooks existentes.

### Geração sintética com SDV

- O projeto utiliza a biblioteca `sdv` para gerar dados sintéticos.
- A geração sintética é tratada como etapa de modelagem que recebe os dados processados e produz amostras geradas pelo SDV.
- Notebooks devem documentar o fluxo de treinamento e amostragem usando modelos compatíveis com `sdv`.

### Notebooks como tooling / exploração

- `notebooks/01_data_analysis.ipynb`: ponto de partida para análise exploratória dos dados.
- `notebooks/02_gaussian_copula.ipynb`: foco em experimentação com geração sintética de dados usando uma abordagem baseada em Gaussian Copula.
- Notebooks são a principal interface de desenvolvimento e validação nesta fase inicial.

## Fluxo da solução

1. Dados brutos são armazenados em `data/raw`.
2. Dados são limpos, transformados e colocados em `data/processed_data`.
3. Notebooks exploram os dados processados, avaliam qualidade e testam geração sintética.
4. Resultados de notebooks e artefatos de experimentos podem ser direcionados para `output`.

Fluxo simplificado:

`data/raw` -> `data/processed_data` -> `notebooks` / `output`

## Estrutura de diretórios

- `data/raw`: dados fonte brutos, não modificados
- `data/processed_data`: dados preparados para análise ou geração sintética
- `docs`: documentação do projeto, incluindo arquitetura e decisões
- `notebooks`: notebooks Jupyter para análise exploratória e experimentação com SDV
- `output`: artefatos gerados e resultados de experimentos
- `pyproject.toml`: configuração de dependências e metadados do projeto
- `README.md`: documento principal do repositório

## Tecnologias e dependências

- Python 3.10+ (compatível com `>=3.10,<3.12`)
- `Poetry` para gerenciamento de dependências e ambiente
- `pandas` para manipulação de dados
- `pyarrow` para leitura/escrita de dados e interoperabilidade de formatos
- `sdv` para geração de dados sintéticos
- `jupyter` e `ipykernel` para execução de notebooks

## Limites do escopo atual

- O projeto é uma plataforma inicial de bootstrap e não um produto completo.
- Não há código de pipeline de produção ou automação de ETL formalizado ainda.
- A principal implementação é exploratória, baseada em notebooks.
- Avaliação de qualidade, validação de privacidade e deploy ainda não estão formalizados.
- O repositório serve como base para evoluções futuras em engenharia de dados e geração sintética.
