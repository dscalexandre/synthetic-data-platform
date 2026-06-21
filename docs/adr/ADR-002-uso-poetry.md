# ADR-002 — Uso de Poetry para gerenciamento de dependências

## Status

Aceita.

## Contexto

- Poetry oferece gerenciamento consistente de dependências com resolução automática de conflitos.
- Suporta ambientes virtuais isolados no próprio projeto com `virtualenvs.in-project = true`.
- Garante reprodutibilidade entre ambientes diferentes.
- Integra-se a ferramentas de qualidade de código e publicação de pacotes.

## Decisão

Adotar Poetry como gerenciador de dependências e de ambiente do projeto.

## Consequências positivas

- Gerenciamento simplificado de dependências com arquivo de lock (`poetry.lock`).
- Ambiente isolado e reprodutível para toda a equipe.
- Onboarding facilitado com o comando padrão `poetry install`.
- Suporte a grupos de dependências, como desenvolvimento e testes, para melhor controle de escopo.

## Alternativas consideradas

- `pip` com `requirements.txt`: solução simples, mas sem resolução robusta de conflitos.
- `pipenv`: semelhante ao Poetry, mas menos adotado em projetos novos.
- `conda`: alternativa viável, mas adiciona complexidade e maior uso de espaço em disco.
