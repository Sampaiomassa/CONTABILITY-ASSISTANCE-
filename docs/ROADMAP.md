# Roadmap inicial — Assistente Contábil

## Fase 0 — Diagnóstico

- Ler `index.html` atual.
- Mapear funcionalidades existentes.
- Identificar campos inseguros.
- Separar o que será mantido, removido e reorganizado.

## Fase 1 — Segurança e estrutura base

- Remover/substituir qualquer armazenamento de senhas sensíveis.
- Criar estrutura lógica de contabilidade > clientes > documentos > pendências.
- Garantir que o app funcione 100% sozinho, sem dependência externa.

## Fase 2 — Produto operacional

- Melhorar cadastro de clientes.
- Criar painel de pendências.
- Organizar documentos por cliente, com reconhecimento automático de padrões (tributo, valor, vencimento).
- Criar guias/débitos por cliente.
- Criar checklists e mensagens prontas.

## Fase 3 — Multiempresa no app

- Separar dados por contabilidade.
- Preparar IDs internos: contabilidadeId, clienteId, documentoId, pendenciaId.
- Evitar mistura entre contabilidades.

## Fase 4 — Recurso opcional de chat/IA

- Adicionar campo de configuração de API keys por contabilidade (quantas o cliente quiser cadastrar).
- Estrutura de plugin/adaptador simples para o serviço que o cliente escolher plugar.
- Manter funcionamento 100% completo sem esse recurso.

## Fase 5 — Produto comercial

- Exportações melhores.
- Relatórios por cliente.
- Painel administrativo.
- Login real e banco persistente, quando sair do MVP local.
- Posicionamento de venda aproveitando a janela da Reforma Tributária (2026).
