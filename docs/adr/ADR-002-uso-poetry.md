# ADR-002 — Usar Poetry para gerenciar dependências

## Status

Aceito.

## Contexto

- O projeto precisa declarar, resolver e instalar dependências Python de forma
  reproduzível.
- O ambiente inclui dependências obrigatórias para manipulação e síntese de
  dados e um conjunto opcional para a execução dos notebooks.
- O projeto não distribui um pacote Python próprio.

## Decisão

Adotar Poetry como gerenciador de dependências e do ambiente do projeto. Manter o modo de empacotamento desabilitado (`package-mode = false`) e registrar as versões resolvidas em `poetry.lock`.

## Consequências positivas

- Centraliza metadados e restrições de dependências em `pyproject.toml`.
- Mantém as versões resolvidas no arquivo `poetry.lock`.
- Separa as ferramentas de notebook no conjunto opcional `notebooks`.
- Permite instalar o ambiente de execução dos notebooks com um único comando:
  `poetry install -E notebooks`.

## Consequências negativas

- Colaboradores precisam instalar e conhecer os comandos do Poetry.
- Alterações de dependências exigem manter `pyproject.toml` e `poetry.lock`
  sincronizados.
- A reprodução também depende de uma versão de Python compatível
  (`>=3.10,<3.12`).

## Alternativas consideradas

- `pip` com `requirements.txt`: solução mais simples, mas separa a declaração do
  projeto do arquivo de versões instaláveis.
- Pipenv: também gerencia ambiente e arquivo de bloqueio, com fluxo diferente do
  adotado pela equipe.
- Conda: gerencia dependências Python e de sistema, mas acrescentaria outro
  formato de ambiente ao projeto.
