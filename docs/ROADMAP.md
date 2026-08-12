# Roadmap inicial — Assistente Contábil

## Fase 0 — Diagnóstico

- Ler `index.html` atual.
- Mapear funcionalidades existentes.
- Identificar campos inseguros.
- Separar o que será mantido, removido e reorganizado.

## Fase 1 — Segurança e estrutura base

- Remover/substituir qualquer armazenamento de senhas sensíveis.
- Criar estrutura lógica de contabilidade > clientes > documentos > pendências.
- Garantir que o app funcione sem JARVIS.

## Fase 2 — Produto operacional

- Melhorar cadastro de clientes.
- Criar painel de pendências.
- Organizar documentos por cliente.
- Criar guias/débitos por cliente.
- Criar checklists e mensagens prontas.

## Fase 3 — Multiempresa no app

- Separar dados por contabilidade.
- Preparar IDs internos: contabilidadeId, clienteId, documentoId, pendenciaId.
- Evitar mistura entre contabilidades.

## Fase 4 — Integração opcional com JARVIS

- Adicionar configuração de API key por contabilidade.
- Enviar documentos/textos ao JARVIS quando habilitado.
- Salvar análises no cliente correto.
- Manter funcionamento sem JARVIS.

## Fase 5 — Produto comercial

- Exportações melhores.
- Relatórios por cliente.
- Painel administrativo.
- Login real e banco persistente, quando sair do MVP local.
