# ADR-004 — Adotar registros individuais de decisões arquiteturais

## Status

Aceita.

## Data da decisão

2026-06-21.

## Contexto

As decisões técnicas do projeto eram mantidas de forma centralizada no arquivo
`docs/decisions.md`. Embora essa estrutura tenha sido suficiente durante a fase
inicial, o crescimento do projeto passou a exigir melhor rastreabilidade e um
ciclo de vida independente para cada decisão.

Em um único arquivo, alterações em decisões diferentes compartilham o mesmo
histórico. Isso dificulta identificar quando uma decisão foi proposta, aceita,
substituída ou considerada obsoleta.

## Decisão

Adotar Architecture Decision Records (ADRs) individuais para registrar as
decisões arquiteturais relevantes do projeto.

Cada decisão deve ser armazenada em um arquivo Markdown próprio no diretório
`docs/adr/`, com numeração sequencial, título descritivo e status explícito.

Após a migração das decisões existentes e a atualização de todas as referências,
o arquivo centralizado `docs/decisions.md` deve ser excluído.

Quando uma decisão aceita for alterada, um novo ADR deve ser criado para
substituí-la. O registro anterior deve ser preservado com o status atualizado,
mantendo o histórico da evolução arquitetural.

## Consequências positivas

- Cada decisão passa a ter histórico, contexto e status independentes.
- As decisões podem ser revisadas individualmente em Pull Requests.
- A substituição de uma decisão não exige reescrever o histórico anterior.
- Links podem apontar diretamente para uma decisão específica.
- A evolução da arquitetura torna-se mais clara para novos contribuidores.

## Consequências negativas

- A documentação passa a conter uma quantidade maior de arquivos.
- A numeração e a nomenclatura dos ADRs precisam seguir uma convenção.
- A equipe deve manter status e referências atualizados.
- Decisões pequenas precisam ser diferenciadas de decisões arquiteturais.

## Alternativas consideradas

- Manter todas as decisões em `docs/decisions.md`: estrutura simples, mas com
  menor rastreabilidade e sem ciclo de vida independente.
- Registrar as decisões apenas em issues ou Pull Requests: preserva a discussão,
  mas dificulta a consulta junto à documentação do projeto.
- Utilizar uma ferramenta externa ou wiki: oferece recursos adicionais, mas
  separa as decisões do código e do histórico do repositório.
