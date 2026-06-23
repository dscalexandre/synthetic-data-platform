# Synthetic Data Platform

## Objetivo

Plataforma para geração de dados sintéticos a partir de dados tabulares reais.

O projeto foca em ingestão, preparação e transformação de dados brutos, além da experimentação de geração sintética utilizando SDV por meio de notebooks Jupyter.

## Arquitetura de Alto Nível

Os dados brutos são armazenados em `raw`, explorados por meio do notebook `01_gaussian_copula.ipynb` onde os dados são sintetizados e armazenados em `processed_data.

A geração sintética utiliza o SDV como framework principal e o notebook como artefato de desenvolvimento e validação.

### Fluxo Simplificado

```text
raw -> gaussian_copula - processed_data -> output
```

## Tecnologias Utilizadas

- Python >= 3.10,<3.12
- Poetry para gerenciamento de dependências
- pandas para manipulação de dados
- pyarrow para interoperabilidade de formatos
- sdv para geração de dados sintéticos
- jupyter e ipykernel para execução de notebooks

## Estrutura do Projeto

```text
synthetic-data-platform/
│
├── .git
│
├── .github/
│   └── pull_request_template.md
│
├── .vscode/
│   └── settings.json
│
├── data/
│   ├── raw/
│   └── processed_data/
│
├── docs/
│   ├── adr/
│   │   ├── ADR-001-uso-sdv.md
│   │   ├── ADR-002-uso-poetry.md
│   │   ├── ADR-003-uso-jupyter-notebooks.md
│   │   └── ADR-004-adocao-de-adrs-individuais.md
│   ├── images/
│   └── architecture.md
│
├── notebooks/
│   └── 01_gaussian_copula.ipynb
│
├── output/
│
├── src/
│   └── sdp/
│       ├── __init__.py
│       ├── statistics.py
│       └── utils.py
│
├── .editorconfig
├── .gitignore
├── poetry.lock
├── pyproject.toml
└── README.md
```

### Principais Diretórios

```
| Diretório / Arquivo | Descrição                                                          |
| ------------------- | ------------------------------------------------------------------ |
| raw                 | Dados originais recebidos                                          |
| processed_data      | Dados sintéticos gerados pelo SDV                                  |
| docs                | Documentação do projeto, incluindo ADRs e arquitetura              |
| adr                 | Registros individuais de decisões arquiteturais                    |
| notebooks           | Notebook principal de experimentação com Gaussian Copula           |
| output              | Artefatos gerados e resultados de experimentos                     |
| pyproject.toml      | Metadados e dependências do projeto                                |
```

## Como Executar

### Instalar dependências

```bash
poetry install
```

### Executar notebook

```bash
poetry run jupyter notebook notebooks/01_gaussian_copula.ipynb
```

### Fluxo de utilização

- Utilizar `raw` como entrada de dados.
- Utilizar `processed_data` como destino das transformações.
- Salvar os resultados dos experimentos em `output`.

## Roadmap

- [ ] Documentar e formalizar o fluxo de preparação de dados
- [ ] Integrar validação de qualidade e métricas de avaliação de dados sintéticos
