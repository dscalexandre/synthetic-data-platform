# ADR-001 — Usar SDV para gerar dados sintéticos

## Status

Aceito.

## Contexto

- O projeto precisa modelar e gerar dados tabulares sintéticos a partir de um
  conjunto preparado.
- O SDV oferece uma interface comum para detecção de metadados, treinamento,
  amostragem e avaliação.
- A biblioteca disponibiliza diferentes sintetizadores para tabelas, entre eles
  Gaussian Copula, CTGAN e TVAE.
- O ecossistema é compatível com Python e com o fluxo exploratório adotado pelo
  projeto.

## Decisão

Usar a biblioteca SDV (Synthetic Data Vault) como ferramenta principal de
geração e avaliação de dados sintéticos. O fluxo atual usa o
`GaussianCopulaSynthesizer` para uma única tabela.

## Consequências positivas

- Reduz a quantidade de código necessário para detectar metadados, treinar o
  modelo e gerar amostras.
- Oferece recursos para validar os dados e comparar sua qualidade estatística.
- Permite experimentar outros sintetizadores por meio de abstrações semelhantes.
- Integra-se ao ambiente Python e aos notebooks do projeto.

## Consequências negativas

- O projeto passa a depender da API, das restrições e da compatibilidade de
  versões do SDV.
- A qualidade da amostra depende da configuração dos metadados e da validação do
  modelo.

## Alternativas consideradas

- `Faker` com regras personalizadas: adequado para dados fictícios baseados em
  regras, mas não para reproduzir automaticamente relações estatísticas do
  conjunto de origem.
