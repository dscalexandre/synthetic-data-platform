# Arquitetura da Plataforma de Dados Sintéticos

## Visão geral

A solução implementa um fluxo exploratório para analisar, preparar, gerar e
avaliar dados tabulares sintéticos com o SDV. Nesta fase, os notebooks são
simultaneamente a interface de execução, a implementação do fluxo e o registro
das análises.

```text
Dados brutos       Dados preparados       Dados sintéticos
data/raw/ ───────► data/processed/ ─────► data/synthetic/
          notebook 01              notebook 02
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

O notebook [`01_data_analysis.ipynb`](../notebooks/01_data_analysis.ipynb)
executa as seguintes etapas:

1. lê os arquivos CSV particionados disponíveis em `data/raw/customers/`;
2. consolida os registros em um único conjunto de dados;
3. inspeciona estrutura, colunas, valores ausentes, registros duplicados e
   duplicidade de `id`;
4. converte `creation_date` e `last_activity_date` para `datetime`;
5. executa análise exploratória da variável `age_group`, incluindo estatísticas
   descritivas, teste de normalidade, histograma e tabela de frequência;
6. grava o resultado em `data/processed/customers.csv`.

### Geração sintética

O notebook [`02_gaussian_copula.ipynb`](../notebooks/02_gaussian_copula.ipynb):

1. carrega `data/processed/customers.csv`;
2. reconverte as colunas de data para `datetime`;
3. detecta os metadados da tabela com `Metadata.detect_from_dataframe`;
4. salva os metadados detectados em JSON;
5. treina um `GaussianCopulaSynthesizer`;
6. gera uma amostra sintética com o mesmo número de linhas do conjunto
   preparado;
7. preserva deliberadamente a coluna `id` original para compatibilidade com
   relacionamentos externos;
8. valida estrutura e qualidade com `run_diagnostic` e `evaluate_quality`;
9. compara características dos dados preparados e sintéticos;
10. grava a amostra em `data/synthetic/`.

As colunas `country` e `last_country_logged` são mantidas como categóricas pelo
fluxo atual. Os dados usam códigos de país em padrão ISO Alpha-3, enquanto o
tipo semântico `country_code` do SDV é voltado a códigos ISO Alpha-2.

Os artefatos esperados são:

- `data/synthetic/customers_metadata.json`;
- `data/synthetic/customers_synthetic.csv`.

## Contrato de dados atual

O fluxo está especializado na tabela `customers` e espera partições CSV com as
seguintes colunas:

```text
firstname,lastname,email,address,country,last_country_logged,
creation_date,last_activity_date,age_group,id
```

As premissas operacionais são:

- todas as partições em `data/raw/customers/` possuem o mesmo esquema;
- `creation_date` e `last_activity_date` usam o formato `%m-%d-%Y %H:%M:%S`;
- `age_group` é uma variável numérica discreta;
- `id` identifica os registros e é preservado no CSV sintético;
- `country` e `last_country_logged` contêm códigos ISO Alpha-3 tratados como
  categorias.

## Avaliação dos dados sintéticos

O segundo notebook aplica duas avaliações complementares do SDV:

- `run_diagnostic`: verifica validade dos valores e compatibilidade estrutural
  com os metadados;
- `evaluate_quality`: compara distribuições individuais e tendências entre
  pares de colunas.

Também são geradas visualizações comparando a distribuição de `age_group` nos
dados preparados e sintéticos. O diagnóstico estrutural não deve ser confundido
com garantia de anonimização, privacidade ou utilidade analítica.

## Configuração do ambiente

- `pyproject.toml`: metadados, versão compatível do Python e dependências;
- `poetry.lock`: versões resolvidas para reprodução do ambiente;
- `.editorconfig`: regras básicas de formatação dos arquivos de texto.

O projeto usa o Poetry com `package-mode = false`, pois não distribui um pacote
Python. As dependências do Jupyter pertencem ao conjunto opcional `notebooks`.

As dependências obrigatórias são:

- `pyarrow`;
- `sdv`.

As dependências opcionais para os notebooks incluem:

- `jupyter`;
- `ipykernel`;
- `watermark`;
- `pandas`;
- `plotly`;
- `scipy`.

## Documentação do projeto

- `README.md`: visão geral, pré-requisitos, instalação e instruções de execução;
- `docs/architecture.md`: componentes, fluxo de dados e limites arquiteturais da
  solução;
- `docs/adr/`: registros individuais das decisões arquiteturais e de suas
  consequências.

## Sequência de execução

Os notebooks devem ser iniciados a partir da raiz do repositório ou do diretório
`notebooks/`, pois ambos ajustam o diretório de trabalho para a raiz do projeto:

1. instalar o ambiente com `poetry install -E notebooks`;
2. colocar os CSVs de origem em `data/raw/customers/`;
3. executar `notebooks/01_data_analysis.ipynb`;
4. verificar `data/processed/customers.csv`;
5. executar `notebooks/02_gaussian_copula.ipynb`;
6. verificar os artefatos em `data/synthetic/`.

## Limites do escopo atual

- A execução é manual e não há orquestrador de pipeline.
- O conjunto e os caminhos usados nos notebooks são específicos de `customers`.
- A preparação, a modelagem e a avaliação ainda não foram extraídas para módulos
  Python.
- Não há suíte automatizada de testes ou integração contínua.
- A coluna `id` original é preservada no conjunto sintético.
- O fluxo não define limiares formais de aceite para qualidade estatística,
  privacidade ou risco de reidentificação.
- O `GaussianCopulaSynthesizer` é o único sintetizador implementado.

As escolhas que sustentam esta estrutura estão registradas nos
[ADRs do projeto](adr/).
