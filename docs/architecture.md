# Arquitetura da Plataforma do Gerador de Dados Sintéticos

## Visão geral

A solução implementa um fluxo exploratório para preparar dados tabulares e gerar
uma amostra sintética com o SDV. Nesta fase, os notebooks são simultaneamente a
interface de execução, a implementação do fluxo e o registro das análises.

```text
Dados brutos       Dados preparados       Dados sintéticos
data/raw/ ───────► data/processed/ ─────► data/synthetic/
           notebook 01             notebook 02
```

## Componentes

### Armazenamento local

- `data/raw/`: dados de origem, preservados sem transformação;
- `data/processed/`: dados consolidados e preparados para a modelagem;
- `data/synthetic/`: metadados detectados pelo SDV e amostras sintéticas.

O arquivo `.gitignore` exclui o conteúdo desses diretórios do versionamento e
mantém apenas seus respectivos arquivos `.gitkeep`. Assim, dados de entrada e
artefatos gerados permanecem locais.

### Preparação de dados

O notebook [`01_data_preparation.ipynb`](../notebooks/01_data_preparation.ipynb) executa as seguintes etapas:

1. lê os arquivos CSV particionados disponíveis em `data/raw/customers/`;
2. consolida os registros em um único conjunto de dados;
3. realiza as transformações e validações necessárias;
4. grava o resultado em `data/processed/customers.csv`.

### Geração sintética

O notebook [`02_gaussian_copula.ipynb`](../notebooks/02_gaussian_copula.ipynb):

1. carrega `data/processed/customers.csv`;
2. detecta e ajusta os metadados da tabela;
3. treina um `GaussianCopulaSynthesizer`;
4. gera e valida uma amostra sintética;
5. compara características dos dados preparados e sintéticos;
6. grava os metadados e a amostra em `data/synthetic/`.

Os artefatos esperados são:

- `data/synthetic/customers_metadata.json`;
- `data/synthetic/customers_synthetic.csv`.

### Configuração do ambiente

- `pyproject.toml`: metadados, versão compatível do Python e dependências;
- `poetry.lock`: versões resolvidas para reprodução do ambiente;
- `.vscode/settings.json`: seleção local do ambiente Poetry no Visual Studio
  Code. O diretório `.vscode/` não é versionado;
- `.editorconfig`: regras básicas de formatação dos arquivos de texto.

O projeto usa o Poetry com `package-mode = false`, pois não distribui um pacote
Python. As dependências do Jupyter pertencem ao conjunto opcional `notebooks`.

### Documentação do projeto

- `README.md`: visão geral, pré-requisitos, instalação e instruções de execução;
- `docs/architecture.md`: componentes, fluxo de dados e limites arquiteturais da
  solução;
- `docs/adr/`: registros individuais das decisões arquiteturais e de suas
  consequências.

## Sequência de execução

Os notebooks devem ser iniciados a partir da raiz do repositório, pois usam
caminhos relativos:

1. instalar o ambiente com `poetry install -E notebooks`;
2. colocar os CSVs de origem em `data/raw/customers/`;
3. executar `notebooks/01_data_preparation.ipynb`;
4. verificar `data/processed/customers.csv`;
5. executar `notebooks/02_gaussian_copula.ipynb`;
6. verificar os artefatos em `data/synthetic/`.

## Limites do escopo atual

- A execução é manual e não há orquestrador de pipeline.
- O conjunto e os caminhos usados nos notebooks são específicos de `customers`.
- A preparação e a modelagem ainda não foram extraídas para módulos Python.
- Não há suíte automatizada de testes ou integração contínua.

As escolhas que sustentam esta estrutura estão registradas nos
[ADRs do projeto](adr/).
