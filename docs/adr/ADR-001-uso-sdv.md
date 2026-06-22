# ADR-001 — Uso de SDV para geração de dados sintéticos

## Status

Aceita.

## Contexto

- SDV é uma biblioteca especializada em geração de dados sintéticos com suporte a modelos estatísticos robustos.
- Oferece múltiplos modelos: Gaussian Copula, TVAE, CTGAN, entre outros.
- É bem documentada e está ativa em desenvolvimento.
- Possui uma comunidade estabelecida em pesquisa de privacidade e geração de dados.

## Decisão

Usar a biblioteca SDV (Synthetic Data Vault) como framework principal para geração de dados sintéticos.

## Consequências positivas

- Reduz a curva de aprendizado em geração sintética com abstrações bem desenhadas.
- Permite a experimentação com diferentes modelos sem refatoração do código-base.
- Oferece suporte nativo para avaliação da qualidade e da privacidade dos dados gerados.
- É compatível com dados tabulares, séries temporais e dados relacionais.
- Mantém, quando treinado e validado adequadamente, as distribuições marginais, correlações e probabilidades estatísticas observadas nos dados originais, facilitando análises reproduzíveis.

## Alternativas consideradas

- `gretel-synthetics`: alternativa comercial com suporte premium, mas menos flexível para exploração.
- Implementação manual com bibliotecas de machine learning, como scikit-learn e TensorFlow: maior complexidade e menor reutilização.
- `Faker` com lógica customizada: viável apenas para dados simples, pois não captura distribuições reais.
