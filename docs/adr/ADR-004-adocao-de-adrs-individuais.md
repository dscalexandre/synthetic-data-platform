# ADR-004 — Adotar registros individuais de decisões arquiteturais

## Status

Aceito.

## Contexto

As decisões técnicas do projeto seriam registradas de forma centralizada no arquivo docs/decisions.md. Considerando a evolução prevista do projeto, foi identificada a necessidade de adotar uma abordagem que proporcionasse maior rastreabilidade, melhor organização e um ciclo de vida independente para cada decisão arquitetural.

Manter todas as decisões em um único arquivo faz com que alterações em decisões distintas compartilhem o mesmo histórico de versionamento, dificultando identificar quando cada decisão foi proposta, aprovada, revisada, substituída ou considerada obsoleta.

## Decisão

Adotar Architecture Decision Records (ADRs) individuais para registrar as
decisões arquiteturais relevantes do projeto.

Cada decisão deve ser armazenada em um arquivo Markdown próprio no diretório
`docs/adr/`, com numeração sequencial, título descritivo e status explícito.

Quando uma decisão aceita for alterada, um novo ADR deve ser criado para
substituí-la. O registro anterior deve ser preservado com o status atualizado,
mantendo o histórico da evolução arquitetural.

## Consequências positivas

- Cada decisão passa a ter histórico, contexto e status independentes.
- As decisões podem ser revisadas individualmente em pull requests.
- A substituição de uma decisão não exige reescrever o histórico anterior.
- A evolução da arquitetura torna-se mais clara para novos contribuidores.

## Consequências negativas

- A documentação passa a conter uma quantidade maior de arquivos.
- A numeração e a nomenclatura dos ADRs precisam seguir uma convenção.
- A equipe deve manter status e referências atualizados.
- Decisões pequenas precisam ser diferenciadas de decisões arquiteturais.

## Alternativas consideradas

- Manter todas as decisões em `docs/decisions.md`: estrutura simples, mas com
  menor rastreabilidade e sem ciclo de vida independente.
- Registrar as decisões apenas em issues ou pull requests: preserva a discussão,
  mas dificulta a consulta junto à documentação do projeto.
- Utilizar uma ferramenta externa: oferece recursos adicionais, mas
  separa as decisões do código e do histórico do repositório.
