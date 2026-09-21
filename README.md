# Assistente Contábil

Software operacional para escritórios de contabilidade e firmas pequenas — **independente e autossuficiente**. Não depende de nenhuma IA externa, API ou serviço de terceiros para funcionar.

## Proposta

Organizar a rotina da contabilidade antes dela chegar ao sistema oficial de escrituração: clientes, documentos, pendências, guias, débitos e cobranças — reconhecendo padrões automaticamente (tributos, vencimentos, valores) a partir do que o cliente manda (prints, boletos, PDFs, planilhas).

Frase guia:

> O Assistente Contábil organiza a bagunça do cliente antes dela virar trabalho manual do escritório.

Contexto de mercado: a partir de 2026 começa a transição da Reforma Tributária (IBS/CBS), trazendo mudanças relevantes nas obrigações fiscais. Isso deve gerar forte demanda por ferramentas que ajudem escritórios pequenos e firmas a se organizarem e se adaptarem rápido. O produto deve estar pronto para capturar essa demanda.

## Regra principal

O Assistente Contábil é um projeto 100% independente.

- Nenhuma funcionalidade essencial depende de API, IA ou serviço externo.
- Reconhecimento de documentos, organização, checklists e exportações rodam localmente.
- Se no futuro o produto ganhar algum recurso de chat/IA, ele é opcional: apenas um campo de configuração onde a contabilidade cadastra quantas API keys quiser, de qualquer serviço que já tenha à disposição. Sem hub, sem projeto de terceiros embutido, sem dependência de nenhum fornecedor específico.
- Nenhum fornecedor de IA específico é parte da arquitetura do Assistente Contábil.

## Arquivos iniciais

- `index.html` — HTML base atual do Assistente Contábil.
- `ARQUIVO_MESTRE.md` — documento mestre técnico/produto para orientar Claude Code/Codex.
- `prompts/PROMPT_CLAUDE_INICIAL.md` — prompt inicial recomendado para Claude Code.
- `docs/ROADMAP.md` — fases sugeridas para evolução.

## Objetivo do MVP

Criar uma central funcional para contabilidades e firmas pequenas com:

- cadastro de contabilidades;
- cadastro de clientes;
- documentos por cliente, com reconhecimento automático de padrões (tributo, valor, vencimento, status);
- pendências;
- guias e débitos;
- checklists;
- mensagens prontas;
- relatórios/exportações;
- separação entre contabilidades (multiempresa);
- campo opcional de configuração de API keys do cliente, para uso futuro em recursos de chat/IA, caso implementados.

## Segurança obrigatória

- Não armazenar senha GOV.br, e-CAC, prefeitura ou qualquer credencial sensível.
- Não hardcodar API keys.
- Não misturar dados entre contabilidades.
- Não vender como substituto do Domínio.

## Estado atual (MVP local, `index.html`)

Implementado e funcional, 100% no navegador (localStorage/IndexedDB, sem backend):

- Multiempresa: cada contabilidade é um workspace isolado (troca pelo seletor no cabeçalho), com todos os dados namespaced por `contabilidadeId`.
- Cadastro de cliente sem nenhum campo de senha — apenas "Situação de Acesso" (procuração pendente / certificado disponível / acesso autorizado / aguardando documentação).
- Importação de planilha com detecção e remoção automática de colunas de senha/credencial antes de qualquer exibição ou armazenamento.
- Painel de Pendências (cadastro, urgência, status, filtro).
- Guias/Dívidas vinculadas a cliente, com status (aberta/vencida/paga/parcelada/etc.), reconhecimento automático via OCR de boletos/prints (inclui DAS, IRRF, INSS, ICMS, ISS, IBS, CBS, Imposto Seletivo) e exportação PDF/Excel.
- Checklist mensal por regime tributário e dossiê exportável em PDF, dentro do cadastro de cada cliente.
- Frases prontas (mensagens de cobrança/orientação), incluindo modelo padrão sobre a Reforma Tributária 2026.
- Assistente de IA local (sem API) com base de conhecimento sobre DAS MEI, Simples Nacional, IRPF, dívida ativa, parcelamentos e Reforma Tributária (IBS/CBS).
- Configurações: campo opcional para cadastrar API keys (não utilizado por nenhuma função hoje — reservado para o futuro).

Pendente para as próximas fases (fora do escopo de um app 100% front-end):

- Login real e permissões por usuário interno.
- Backend com banco persistente (hoje os dados vivem no navegador de quem usa — não sincronizam entre dispositivos nem fazem backup automático em nuvem).
- Painel administrativo e planos pagos.
