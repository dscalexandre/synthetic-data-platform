# Arquitetura da Plataforma de Dados Sintéticos

## Objetivo da solução

A plataforma tem como objetivo oferecer uma base inicial para geração de dados
sintéticos usando SDV. O foco é permitir a ingestão, a preparação e a
transformação de dados brutos, além da geração exploratória de dados sintéticos
por meio de um notebook Jupyter.

## Componentes principais do projeto

### Ingestão / saída de dados

- `data/raw`: local destinado ao armazenamento dos dados originais recebidos ou
  estudados.
- `data/processed_data`: local destinado ao armazenamento de dados transformados
  e preparados para análise ou geração sintética.
- `output`: local para artefatos gerados, resultados de experimentos e possíveis
  artefatos de modelo.

### Preparação de dados

- O projeto usa um notebook Jupyter para explorar e preparar os dados.
- A preparação inclui limpeza, transformação e formatação dos dados de maneira
  compatível com os modelos SDV.
- A lógica de preparação deve ser documentada e experimentada no notebook
  `notebooks/01_gaussian_copula.ipynb`.

### Geração sintética com SDV

- O projeto utiliza a biblioteca `sdv` para gerar dados sintéticos.
- A geração sintética é tratada como uma etapa de modelagem que recebe os dados
  processados e produz amostras por meio do SDV.
- O notebook deve documentar o fluxo de preparação, treinamento e amostragem
  usando o modelo Gaussian Copula.

### Notebook como ferramenta de exploração

- `notebooks/01_gaussian_copula.ipynb`: concentra a análise exploratória, a
  preparação dos dados e a experimentação com geração sintética usando o modelo
  Gaussian Copula.
- O notebook é a principal interface de desenvolvimento e validação nesta fase
  inicial.

## Fluxo da solução

1. Dados brutos são armazenados em `data/raw`.
2. Dados são limpos, transformados e colocados em `data/processed_data`.
3. O notebook explora os dados processados, avalia sua qualidade e testa a
   geração sintética.
4. Os resultados e artefatos dos experimentos podem ser direcionados para
   `output`.

Fluxo simplificado:

`data/raw` -> `data/processed_data` -> `notebooks` / `output`

## Estrutura de diretórios

- `data/raw`: dados fonte brutos, não modificados
- `data/processed_data`: dados preparados para análise ou geração sintética
- `docs`: documentação do projeto, incluindo arquitetura e ADRs
- `notebooks`: contém o notebook `01_gaussian_copula.ipynb`, utilizado para
  análise exploratória e experimentação com SDV
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
- A principal implementação é exploratória e baseada em um notebook.
- Avaliação de qualidade, validação de privacidade e deploy ainda não estão
  formalizados.
- O repositório serve como base para evoluções futuras em engenharia de dados e
  geração sintética.
