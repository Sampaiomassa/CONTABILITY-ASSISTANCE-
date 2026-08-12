# ARQUIVO MESTRE — PROJETO ASSISTENTE CONTÁBIL
## Continuação pelo Claude Code

## 1. Objetivo central

Criar um software funcional para escritórios de contabilidade, vendável para várias contabilidades diferentes, com custo inicial zero de desenvolvimento e arquitetura segura multiempresa.

O sistema deve funcionar por conta própria, mesmo sem JARVIS.

O JARVIS entra como camada opcional/premium de inteligência, automação, análise documental e apoio operacional. Ele não é dependência obrigatória para o produto funcionar.

Frase guia:

> O Assistente Contábil organiza a rotina da contabilidade por conta própria. Com o JARVIS integrado, ele ganha inteligência, análise automática e automações avançadas.

## 2. Posicionamento do produto

O Assistente Contábil não substitui o Domínio.

O Domínio continua sendo o sistema oficial para escrituração, apuração, folha, fiscal, contábil, obrigações e envios formais.

O Assistente Contábil complementa o Domínio atuando antes dele, organizando documentos, clientes, pendências, guias, mensagens, checklists e relatórios.

Frase comercial principal:

> O Assistente Contábil organiza a bagunça antes do Domínio.

Fluxo ideal:

Cliente manda bagunça → Assistente Contábil organiza → Equipe confere → JARVIS potencializa quando necessário → Domínio recebe informação pronta.

## 3. Regra arquitetural obrigatória

O JARVIS e o Assistente Contábil são projetos separados.

### JARVIS

O JARVIS é API central independente, cérebro externo de IA, camada de autenticação, memória, upload e contexto.

O repositório do JARVIS não deve receber nenhuma pasta ou código do Assistente Contábil, nem de qualquer outro aplicativo terceiro.

Não colocar no repositório JARVIS:

- pasta do Assistente Contábil;
- código específico de contabilidade;
- frontend final de produto externo;
- código de cliente final;
- app terceiro.

### Assistente Contábil

O Assistente Contábil deve ter repositório próprio.

Ele deve ser funcional sozinho.

Quando precisar de IA, ele chama o JARVIS via API segura:

```http
Authorization: Bearer <API_KEY_DA_CONTABILIDADE>
```

## 4. Modelo comercial

O produto será vendido para múltiplas contabilidades.

Cada contabilidade terá seu próprio ambiente lógico.

Exemplo:

- Contabilidade A usa o sistema;
- Contabilidade B usa o sistema;
- Contabilidade C usa o sistema.

A Contabilidade A não pode ver dados da Contabilidade B.

A Contabilidade B não pode ver dados da Contabilidade A.

O isolamento deve valer para:

- clientes;
- documentos;
- pendências;
- guias;
- débitos;
- mensagens;
- relatórios;
- análises do JARVIS;
- usuários internos;
- configurações.

## 5. Estrutura lógica multiempresa

Estrutura desejada:

```text
Contabilidade contratante
 ├── Usuários internos
 ├── Clientes
 │    ├── Documentos
 │    ├── Pendências
 │    ├── Guias e débitos
 │    ├── Mensagens
 │    ├── Checklists
 │    └── Relatórios
 ├── Configurações
 ├── Exportações
 └── Integração opcional com JARVIS
```

IDs mínimos recomendados desde o início:

- contabilidadeId;
- usuarioId;
- clienteId;
- documentoId;
- pendenciaId;
- guiaDebitoId;
- relatorioId.

Todo registro sensível deve estar vinculado a `contabilidadeId`.

## 6. MVP funcional sem JARVIS

O primeiro MVP deve funcionar sem IA.

Funcionalidades obrigatórias do MVP básico:

1. Cadastro de contabilidades.
2. Cadastro de clientes por contabilidade.
3. Cadastro e organização de documentos por cliente.
4. Painel de pendências.
5. Registro de guias e débitos.
6. Checklists mensais por tipo de cliente.
7. Mensagens prontas para WhatsApp/e-mail.
8. Dossiê/resumo do cliente.
9. Exportação PDF/CSV/Excel simples.
10. Separação segura entre contabilidades.

## 7. Funcionalidades principais

### 7.1 Cadastro de contabilidades

Campos recomendados:

- id;
- nome;
- CNPJ;
- responsável principal;
- e-mail;
- telefone;
- status da conta;
- plano contratado;
- data de cadastro;
- configurações internas;
- chave JARVIS opcional.

### 7.2 Cadastro de clientes

Campos recomendados:

- id;
- contabilidadeId;
- nome ou razão social;
- CPF/CNPJ;
- tipo de cliente;
- regime tributário;
- responsável interno;
- WhatsApp;
- e-mail;
- status;
- categoria;
- observações;
- data de cadastro.

Tipos de cliente:

- MEI;
- Simples Nacional;
- Lucro Presumido;
- Pessoa Física;
- Doméstico;
- Produtor Rural;
- Outro.

Regra de segurança:

Não armazenar senha GOV.br, senha e-CAC, senha de prefeitura, senha de certificado ou qualquer credencial sensível.

Usar campos seguros como:

- procuração pendente;
- certificado disponível;
- acesso autorizado;
- cliente precisa enviar código;
- aguardando documentação.

### 7.3 Central de documentos

Tipos de arquivo previstos:

- PDF;
- imagem/print;
- TXT;
- CSV;
- Excel;
- comprovante;
- guia;
- relatório;
- documento fiscal;
- extrato.

Funções:

- anexar documento;
- vincular ao cliente;
- classificar documento;
- registrar origem;
- registrar data;
- marcar status;
- adicionar observações;
- exportar;
- enviar ao JARVIS quando habilitado.

Status de documento:

- recebido;
- em análise;
- pendente de confirmação;
- aprovado;
- rejeitado;
- ilegível;
- arquivado.

### 7.4 Guias e débitos

Tipos que o sistema deve organizar:

- DAS MEI;
- DAS Simples Nacional;
- Parcelamento MEI;
- Parcelamento Simples Nacional;
- DARF;
- IRRF;
- INSS;
- CP-SEGUR;
- PGFN;
- Regularize;
- Dívida Ativa da União;
- Dívida Ativa Municipal;
- ISS;
- TFE;
- comprovantes de pagamento;
- guias vencidas.

Campos recomendados:

- id;
- contabilidadeId;
- clienteId;
- tipo;
- competência;
- vencimento;
- valor;
- status;
- origem do documento;
- observação;
- responsável interno;
- data de registro.

Status:

- aberta;
- paga;
- vencida;
- parcelada;
- aguardando comprovante;
- aguardando cliente;
- conferida.

### 7.5 Painel de pendências

Tipos de pendência:

- documento faltante;
- guia sem comprovante;
- guia vencida;
- documento ilegível;
- cliente não respondeu;
- informação incompleta;
- falta extrato;
- falta nota fiscal;
- falta folha;
- falta pró-labore;
- acesso pendente;
- procuração pendente.

Status:

- aberta;
- urgente;
- vencida;
- aguardando cliente;
- aguardando escritório;
- resolvida;
- arquivada.

A tela deve mostrar:

- o que falta;
- de qual cliente falta;
- quem é responsável;
- desde quando está pendente;
- urgência;
- próxima ação recomendada.

### 7.6 Mensagens prontas

O sistema deve ter modelos fixos mesmo sem JARVIS.

Tipos:

- solicitar documento;
- cobrar guia;
- pedir comprovante;
- avisar vencimento;
- cobrar pendência mensal;
- confirmar recebimento;
- explicar para cliente leigo;
- mensagem formal;
- mensagem urgente.

Com JARVIS, as mensagens podem ser personalizadas com base no contexto do cliente.

### 7.7 Checklists mensais

MEI:

- faturamento mensal;
- DAS do mês;
- comprovante de pagamento;
- notas emitidas;
- declaração anual.

Simples Nacional:

- notas emitidas;
- notas tomadas;
- extratos bancários;
- pró-labore;
- folha;
- DAS;
- parcelamentos;
- pendências fiscais.

Pessoa Física:

- informe de rendimentos;
- recibos;
- despesas médicas;
- aluguel;
- extratos;
- documentos patrimoniais.

### 7.8 Dossiê do cliente

Gerar resumo consolidado por cliente:

- status geral;
- pendências abertas;
- documentos recebidos;
- guias identificadas;
- possíveis débitos;
- resumo operacional;
- próximos passos.

### 7.9 Exportações

Exportações úteis:

- PDF do cliente;
- relatório mensal;
- lista de pendências;
- lista de débitos;
- checklist;
- CSV/Excel;
- backup local.

### 7.10 Preparação para o Domínio

Criar indicador “Pronto para Domínio”.

Checklist exemplo:

- documentos recebidos;
- guias conferidas;
- pendências cobradas;
- comprovantes anexados;
- débitos revisados;
- observações internas preenchidas;
- pronto para lançar/conferir no Domínio.

## 8. Papel opcional/premium do JARVIS

O JARVIS não é obrigatório para o funcionamento básico.

Sem JARVIS, o sistema continua com cadastros, documentos, pendências, guias, checklists, mensagens prontas e exportações.

Com JARVIS, o sistema ganha:

- análise automática de documentos;
- resumo inteligente de PDFs;
- classificação de guias;
- interpretação de prints;
- sugestão de pendências;
- geração de mensagens personalizadas;
- explicação de impostos em linguagem simples;
- criação de relatórios inteligentes;
- apoio para funcionários novos;
- automação de conferência.

Fluxo com JARVIS:

```text
Usuário anexa uma guia
Assistente extrai texto
Assistente envia texto ao JARVIS
JARVIS identifica o documento
JARVIS sugere pendência ou ação
Assistente salva o resultado no cliente correto
```

## 9. Estado atual do JARVIS

O JARVIS já está com as seguintes fases concluídas:

- Fase 1: segurança base;
- Fase 2: isolamento inicial por contexto autenticado;
- Fase 3: multiempresa inicial por API keys;
- Fase 4: frontend/painel de teste com API key.

URL atual:

```text
https://jarvis-e32a.onrender.com
```

Health público:

```text
GET https://jarvis-e32a.onrender.com/api/health
```

Autenticação recomendada:

```http
Authorization: Bearer <API_KEY_DA_CONTABILIDADE>
```

Endpoints úteis:

```text
GET /api/health
GET /api/conversations
POST /api/conversations
GET /api/conversations/:id
DELETE /api/conversations/:id
POST /api/chat
POST /api/upload
GET /api/upload/:id/analyze
GET /api/memory/search?q=termo
POST /api/memory/search
```

Atenção: o JARVIS ainda usa armazenamento em memória no estado atual. Deploy/restart pode apagar conversas/uploads temporários. Persistência real fica para fase futura do JARVIS.

## 10. Segurança obrigatória

Regras:

- não armazenar senhas sensíveis;
- não misturar dados entre contabilidades;
- não hardcodar API keys;
- não salvar chave real em repositório;
- não depender do JARVIS para funções básicas;
- não vender como substituto do Domínio;
- não prometer apuração oficial automática;
- não expor dados fiscais em logs;
- não deixar uma contabilidade acessar dados de outra.

## 11. Stack inicial sugerida

Como o objetivo é custo zero no início, começar simples.

Opções de MVP:

- HTML/CSS/JavaScript;
- IndexedDB para armazenamento local inicial;
- exportações locais;
- GitHub para versionamento;
- Render/Vercel/Netlify Free quando necessário;
- integração com JARVIS via API.

Evolução futura:

- backend próprio;
- banco persistente;
- login real;
- multiusuário;
- permissões;
- auditoria;
- planos pagos;
- painel administrativo;
- gestão de API keys.

## 12. Fases recomendadas no Assistente Contábil

### Fase A — Fundação do projeto

- criar repositório próprio;
- organizar arquivos;
- remover credenciais sensíveis;
- definir estrutura de dados;
- garantir que nenhum código do Assistente vá para o repositório JARVIS.

### Fase B — Produto funcional sem JARVIS

- cadastro de contabilidades;
- cadastro de clientes;
- documentos por cliente;
- pendências;
- guias/débitos;
- checklists;
- mensagens prontas;
- exportações.

### Fase C — Separação multiempresa

- implementar contabilidadeId em todos os registros;
- garantir que uma contabilidade não veja dados de outra;
- criar seletor/ambiente por contabilidade no MVP local.

### Fase D — Integração opcional com JARVIS

- campo de configuração da API key por contabilidade;
- chamada ao endpoint /api/chat;
- chamada ao endpoint /api/upload;
- análise de documentos;
- geração de mensagens inteligentes;
- resumo de cliente.

### Fase E — Comercialização

- polir interface;
- criar página inicial/apresentação;
- criar documentação de uso;
- criar fluxo de onboarding;
- preparar demonstração para escritórios.

## 13. Prompt inicial recomendado para Claude Code

Use este prompt no Claude Code quando o repositório do Assistente Contábil estiver criado e o arquivo base estiver no projeto:

```text
Você é um arquiteto sênior fullstack, especialista em SaaS multiempresa, segurança, automações, contabilidade operacional, UX de sistemas internos e integração com APIs de IA.

Contexto:
Este projeto é o Assistente Contábil, um software funcional para escritórios de contabilidade. Ele deve funcionar por conta própria, sem depender do JARVIS. O JARVIS será apenas uma camada opcional/premium para análise, automação e inteligência.

Regra obrigatória:
Este repositório é somente do Assistente Contábil. Não colocar código do JARVIS aqui além de chamadas externas via API. O repositório JARVIS também não deve receber nenhuma pasta deste app.

Objetivo do produto:
Criar uma central operacional para contabilidades organizarem clientes, documentos, pendências, guias, débitos, mensagens, checklists e relatórios, complementando o Domínio sem substituí-lo.

Nesta primeira etapa, NÃO altere arquivos. Apenas analise o projeto atual.

Verifique:
1. Estrutura atual do arquivo/projeto.
2. Funcionalidades existentes.
3. O que pode ser reaproveitado.
4. O que deve ser removido por segurança, especialmente campos de senha GOV.br/e-CAC/prefeitura.
5. Onde falta separação por contabilidadeId.
6. Como transformar o app em produto multiempresa.
7. Como manter funcionamento sem JARVIS.
8. Onde futuramente integrar JARVIS como camada opcional.
9. Quais riscos técnicos existem.
10. Qual é o menor plano seguro de evolução.

Entregue:
- diagnóstico objetivo;
- módulos atuais;
- módulos faltantes;
- riscos;
- plano por fases;
- arquivos que devem ser alterados futuramente;
- primeira correção recomendada.

Não faça commit.
Não abra PR.
Não altere arquivos nesta etapa.
```

## 14. Critério de sucesso

O projeto será considerado bem estruturado quando:

- o Assistente Contábil funcionar sem JARVIS;
- cada contabilidade tiver dados separados;
- clientes/documentos/pendências/guias estiverem organizados;
- exportações funcionarem;
- não houver senhas sensíveis armazenadas;
- o JARVIS puder ser ativado como plus;
- a integração com JARVIS não quebrar o produto básico;
- o produto puder ser demonstrado e vendido para escritórios reais.

## 15. Resumo executivo

O Assistente Contábil será um software operacional vendável para escritórios de contabilidade.

Ele organiza clientes, documentos, pendências, guias, débitos, mensagens, checklists e relatórios.

Ele complementa o Domínio, preparando informações antes das rotinas oficiais.

O sistema deve funcionar sozinho.

O JARVIS será uma camada opcional/premium para inteligência, análise e automação.

A arquitetura deve ser multiempresa, segura e com repositórios separados.

Visão final:

```text
Cliente manda bagunça.
Assistente Contábil organiza.
Equipe confere.
JARVIS potencializa quando necessário.
Domínio recebe informação pronta.
```
