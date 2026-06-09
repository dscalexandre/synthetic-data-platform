# Registro de Decisões Técnicas

## 1. Uso de Poetry para gerenciamento de dependências

**Decisão:** Adotar Poetry como gerenciador de dependências e ambiente do projeto.

**Motivação:**

- Poetry oferece gerenciamento de dependências consistente com resolução automática de conflitos.
- Suporta ambientes virtuais isolados no próprio projeto com `virtualenvs.in-project = true`.
- Garante reprodutibilidade entre ambientes diferentes.
- Integração com ferramentas de qualidade de código e publishing.

**Benefícios:**

- Gerenciamento simplificado de dependências com lock file (`poetry.lock`).
- Ambiente isolado e reprodutível para toda a equipe.
- Facilita onboarding com setup padrão: `poetry install`.
- Suporta grupos de dependências (dev, test) para melhor controle de escopo.

**Alternativas consideradas:**

- `pip` + `requirements.txt`: simples, mas sem resolução robusta de conflitos.
- `pipenv`: similar a Poetry, mas menos adotado em projetos novos.
- `conda`: viável, mas adiciona complexidade e overhead de espaço em disco.

---

## 2. Adoção de SDV para geração de dados sintéticos

**Decisão:** Usar a biblioteca SDV (Synthetic Data Vault) como framework principal para geração de dados sintéticos.

**Motivação:**

- SDV é uma biblioteca especializada em geração de dados sintéticos com suporte a modelos estatísticos robustos.
- Oferece múltiplos modelos: Gaussian Copula, TVAE, CTGAN, etc.
- Bem documentada e ativa em desenvolvimento.
- Comunidade estabelecida em pesquisa de privacidade e geração de dados.

**Benefícios:**

- Reduz curva de aprendizado em geração sintética com abstrações bem desenhadas.
- Permite experimentação com diferentes modelos sem refatoração de código base.
- Suporte nativo para avaliação de qualidade e privacidade de dados gerados.
- Compatível com dados tabulares, séries temporais e dados relacionais.

**Alternativas consideradas:**

- `gretel-synthetics`: alternativa comercial com suporte premium, mas menos flexível para exploração.
- Implementação manual com bibliotecas de ML puro (scikit-learn, tensorflow): maior complexidade, menos reuso.
- `Faker` + lógica customizada: viável apenas para dados simples, não captura distribuições reais.

---

## 3. Jupyter Notebooks como artefato principal de desenvolvimento

**Decisão:** Usar notebooks Jupyter como ferramenta primária para análise exploratória, experimentação e documentação.

**Motivação:**

- Notebooks combinam código, output visual e documentação no mesmo artefato.
- Facilitam exploração interativa e iterativa de dados e modelos.
- Ferramenta de facto na comunidade de Data Science e Engenharia de Dados.
- Suportam prototipagem rápida sem necessidade de refactoring para código modular.

**Benefícios:**

- Reduz tempo de experimentação e validação de hipóteses.
- Documentação viva, alinhada com código e resultados.
- Facilita comunicação com stakeholders através de outputs visuais.
- Permite rastreabilidade de experimentos através do histórico de células.

**Alternativas consideradas:**

- Python scripts com logging: mais rigoroso, mas menos adequado para exploração.
- R Markdown: linguagem diferente, menos compatível com ecossistema SDV (Python).
- Papermill/ploomber: orquestração de notebooks, mais adequado para pipelines maduros.

---

## 4. Versão mínima de Python 3.10

**Decisão:** Estabelecer compatibilidade com Python `>=3.10,<3.12`.

**Motivação:**

- Python 3.10 introduz pattern matching e melhorias em type hints.
- Balanceia modernidade com compatibilidade.
- Suporte de longo prazo disponível até outubro de 2026.
- Compatível com versões recentes de SDV, pandas e pyarrow.

**Benefícios:**

- Acesso a recursos modernos da linguagem.
- Melhor compatibilidade com ferramentas de type checking (mypy).
- Segurança de patches de vulnerabilidade garantida até 2026.
- Reduz débito técnico de versões desatualizadas.

**Alternativas consideradas:**

- Python 3.9 ou anterior: reduz acesso a features modernas, maior risco de vulnerabilidades.
- Python 3.13+: ainda em desenvolvimento, pode quebrar compatibilidade com dependências.

---

## 5. Estrutura de diretórios baseada em dados brutos vs. processados

**Decisão:** Separar dados brutos (`data/raw`) de dados processados (`data/processed_data`) em diretórios distintos.

**Motivação:**

- Garante rastreabilidade: sempre há uma cópia do dado original.
- Facilita auditoria e reprodução de problemas.
- Reduz risco de sobrescrita acidental de fontes de verdade.
- Alinha com boas práticas em Cookiecutter Data Science.

**Benefícios:**

- Maior confiabilidade na qualidade dos dados processados.
- Simplifica lógica de transformação (sempre trabalha com cópia).
- Facilita rollback em caso de erros em ETL.

**Alternativas consideradas:**

- Único diretório `data`: menos overhead de organização, mas reduz rastreabilidade.
- Bancos de dados versioned: mais robusto, mas adiciona complexidade infraestrutural.

---

## 6. Inclusão de notebooks nomeados e temáticos

**Decisão:** Criar notebooks numerados com temas específicos (e.g., `01_data_analysis.ipynb`, `02_gaussian_copula.ipynb`).

**Motivação:**

- Sequência numérica indica fluxo esperado de exploração.
- Nomes temáticos documentam o propósito de cada notebook.
- Facilita organização conforme novos experimentos são adicionados.
- Padrão comum em projetos de Data Science.

**Benefícios:**

- Clareza sobre ordem de execução e propósito de cada notebook.
- Reduz fricção no onboarding de novos contribuidores.
- Rastreabilidade de evolução através do histórico do repositório.

**Alternativas consideradas:**

- Notebooks com nomes genéricos (e.g., `analysis1.ipynb`): menos claro sobre propósito.
- Único notebook monolítico: dificulta manutenção e reutilização.

---

## 7. Uso de PyArrow para serialização de dados

**Decisão:** Incluir `pyarrow` como dependência para interoperabilidade de formatos.

**Motivação:**

- PyArrow oferece suporte para múltiplos formatos: Parquet, CSV, JSON, Arrow IPC.
- Melhor performance em leitura/escrita de grandes volumes de dados.
- Suporte nativo em SDV para dados tabulares.
- Integração com pandas para conversão de tipos.

**Benefícios:**

- Permite trabalhar com formatos comprimidos e eficientes em espaço.
- Facilita integração com ferramentas de big data (PySpark, Polars).
- Melhor performance em pipelines de dados.

**Alternativas consideradas:**

- Apenas CSV com pandas: menos eficiente em performance e espaço.
- HDF5: alternativa de formato binário, mas menos portável.

---

## 8. Escopo limitado à fase de bootstrap

**Decisão:** Manter o projeto como plataforma inicial, sem incluir código de produção ou pipelines automatizados.

**Motivação:**

- Permite iteração rápida e exploração sem overhead de arquitetura produção.
- Facilita experimentação com diferentes abordagens.
- Evita investimento prematuro em ferramentas antes de validar abordagem.
- Mantém repositório lean e focado.

**Benefícios:**

- Flexibilidade para pivotamento baseado em aprendizados.
- Reduz complexidade de manutenção nesta fase.
- Documenta claramente estado atual e expectativas futuras.

**Alternativas consideradas:**

- Projeto full-stack desde o início: maior overhead inicial, menos ágil.
- Sem documentação de escopo: risco de crescimento descontrolado.
