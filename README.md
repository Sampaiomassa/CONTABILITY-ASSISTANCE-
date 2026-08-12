# Assistente Contábil

Software operacional para escritórios de contabilidade, funcional por conta própria, com integração opcional/premium ao JARVIS.

## Regra principal

O Assistente Contábil é um projeto independente do JARVIS.

- O repositório JARVIS não deve receber código deste app.
- Este app pode consumir o JARVIS via API segura.
- O sistema deve funcionar sem JARVIS nas rotinas básicas.
- O JARVIS entra como camada opcional de IA, análise, automação e apoio.

## Arquivos iniciais

- `index.html` — HTML base atual do Assistente Contábil.
- `ARQUIVO_MESTRE.md` — documento mestre técnico/produto para orientar Claude Code/Codex.
- `prompts/PROMPT_CLAUDE_INICIAL.md` — prompt inicial recomendado para Claude Code.
- `docs/ROADMAP.md` — fases sugeridas para evolução.

## Objetivo do MVP

Criar uma central funcional para contabilidades com:

- cadastro de contabilidades;
- cadastro de clientes;
- documentos por cliente;
- pendências;
- guias e débitos;
- checklists;
- mensagens prontas;
- relatórios/exportações;
- separação entre contabilidades;
- integração opcional com JARVIS.

## Segurança obrigatória

- Não armazenar senha GOV.br, e-CAC, prefeitura ou qualquer credencial sensível.
- Não hardcodar API keys.
- Não misturar dados entre contabilidades.
- Não depender do JARVIS para as funções básicas.
- Não vender como substituto do Domínio.

