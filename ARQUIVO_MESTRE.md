# ARQUIVO MESTRE — PROJETO ASSISTENTE CONTÁBIL
## Continuação pelo Claude Code

## 1. Objetivo central

Criar um software funcional para escritórios de contabilidade e firmas pequenas, vendável para várias contabilidades diferentes, com custo inicial zero de desenvolvimento e arquitetura segura multiempresa.

O sistema é **100% independente e autossuficiente**. Não depende de nenhuma IA externa, API paga ou serviço de terceiro para funcionar. Todo o reconhecimento de documentos, organização, checklists e exportações rodam por conta própria.

Frase guia:

> O Assistente Contábil organiza a rotina da contabilidade por conta própria, reconhecendo padrões em documentos e cobranças automaticamente — sem depender de nenhum serviço externo.

Gatilho de mercado: a partir de 2026 começa a transição da Reforma Tributária (IBS/CBS). Escritórios pequenos e firmas terão que se adaptar rápido a mudanças nas obrigações fiscais, o que deve aumentar a demanda por ferramentas de organização e triagem documental. O produto deve estar pronto para essa janela.

## 2. Posicionamento do produto

O Assistente Contábil não substitui o Domínio.

O Domínio continua sendo o sistema oficial para escrituração, apuração, folha, fiscal, contábil, obrigações e envios formais.

O Assistente Contábil complementa o Domínio atuando antes dele, organizando documentos, clientes, pendências, guias, mensagens, checklists e relatórios.

Frase comercial principal:

> O Assistente Contábil organiza a bagunça antes do Domínio.

Fluxo ideal:

Cliente manda bagunça → Assistente Contábil reconhece padrões e organiza → Equipe confere → Domínio recebe informação pronta.

## 3. Recursos futuros de IA/chat (opcional)

O Assistente Contábil não tem nenhuma dependência de API externa, IA ou serviço de terceiros embutida na arquitetura.

Se no futuro o produto ganhar algum recurso de chat/IA, ele entra apenas como um campo de configuração onde a contabilidade cadastra quantas API keys quiser, de qualquer serviço que já tenha à disposição. Não há hub, não há projeto de terceiros embutido, não há fornecedor fixo — a contabilidade escolhe o que (e se) quer plugar.

Regras:

- O Assistente Contábil tem repositório próprio e funciona sozinho.
- Nenhum código de integração é obrigatório no core do produto.
- Qualquer recurso de chat/IA entra como módulo plugável e desligável, nunca como dependência.
- Não hardcodar chave alguma no repositório do Assistente Contábil.

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
 └── Configuração opcional de API keys do cliente (uso futuro em chat/IA)
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

## 6. MVP funcional

O MVP deve ser 100% funcional por conta própria, sem qualquer integração externa.

Funcionalidades obrigatórias do MVP básico:

1. Cadastro de contabilidades.
2. Cadastro de clientes por contabilidade.
3. Cadastro e organização de documentos por cliente, com reconhecimento automático de padrões (tributo, valor, vencimento, status).
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
- API keys cadastradas pelo cliente (opcional, para uso futuro em chat/IA).

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
- classificar documento automaticamente (reconhecimento de padrões);
- registrar origem;
- registrar data;
- marcar status;
- adicionar observações;
- exportar.

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

O sistema deve ter modelos fixos, funcionando por conta própria.

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

Criar indicador "Pronto para Domínio".

Checklist exemplo:

- documentos recebidos;
- guias conferidas;
- pendências cobradas;
- comprovantes anexados;
- débitos revisados;
- observações internas preenchidas;
- pronto para lançar/conferir no Domínio.

## 8. Recursos futuros de chat/IA (opcional)

O Assistente Contábil funciona 100% sem nenhum recurso de IA.

Se o produto ganhar futuramente algum chatbox ou recurso de IA, ele entra apenas como um campo simples de configuração: a contabilidade cadastra quantas API keys quiser, de qualquer serviço que já tenha à disposição. Com isso, o sistema poderia ganhar, de forma opcional:

- análise automática de documentos;
- resumo inteligente de PDFs;
- classificação avançada de guias;
- geração de mensagens personalizadas;
- automações de conferência.

Essa camada nunca é pré-requisito para o funcionamento do produto e não fica presa a um fornecedor específico — cada contabilidade decide quais chaves (se alguma) quer cadastrar.

## 9. Segurança obrigatória

Regras:

- não armazenar senhas sensíveis;
- não misturar dados entre contabilidades;
- não hardcodar API keys;
- não salvar chave real em repositório;
- não vender como substituto do Domínio;
- não prometer apuração oficial automática;
- não expor dados fiscais em logs;
- não deixar uma contabilidade acessar dados de outra.

## 10. Stack inicial sugerida

Como o objetivo é custo zero no início, começar simples.

Opções de MVP:

- HTML/CSS/JavaScript;
- IndexedDB para armazenamento local inicial;
- exportações locais;
- GitHub para versionamento;
- Render/Vercel/Netlify Free quando necessário.

Evolução futura:

- backend próprio;
- banco persistente;
- login real;
- multiusuário;
- permissões;
- auditoria;
- planos pagos;
- painel administrativo;
- campo opcional de API keys, caso o produto ganhe recurso de chat/IA.

## 11. Fases recomendadas no Assistente Contábil

### Fase A — Fundação do projeto

- organizar arquivos;
- remover credenciais sensíveis (ex.: campo de senha GOV.br);
- definir estrutura de dados;
- manter o repositório 100% independente de qualquer outro projeto.

### Fase B — Produto funcional

- cadastro de contabilidades;
- cadastro de clientes;
- documentos por cliente, com reconhecimento de padrões;
- pendências;
- guias/débitos;
- checklists;
- mensagens prontas;
- exportações.

### Fase C — Separação multiempresa

- implementar contabilidadeId em todos os registros;
- garantir que uma contabilidade não veja dados de outra;
- criar seletor/ambiente por contabilidade no MVP local.

### Fase D — Recurso opcional de chat/IA

- campo de configuração de API keys por contabilidade (quantas o cliente quiser);
- estrutura de plugin/adaptador simples para o serviço que o cliente escolher plugar;
- garantir que a ausência desse recurso não afete nenhuma função básica.

### Fase E — Comercialização

- polir interface;
- criar página inicial/apresentação;
- criar documentação de uso;
- criar fluxo de onboarding;
- preparar demonstração para escritórios, destacando a adaptação à Reforma Tributária.

## 12. Prompt inicial recomendado para Claude Code

Use este prompt no Claude Code quando o repositório do Assistente Contábil estiver criado e o arquivo base estiver no projeto:

```text
Você é um arquiteto sênior fullstack, especialista em SaaS multiempresa, segurança, automações, contabilidade operacional e UX de sistemas internos.

Contexto:
Este projeto é o Assistente Contábil, um software funcional e independente para escritórios de contabilidade e firmas pequenas. Ele não depende de nenhuma API externa, IA ou serviço de terceiros para funcionar. Futuramente poderá existir um campo opcional onde o cliente cadastra suas próprias API keys, caso o produto ganhe algum recurso de chat/IA, mas isso nunca é pré-requisito.

Objetivo do produto:
Criar uma central operacional para contabilidades organizarem clientes, documentos, pendências, guias, débitos, mensagens, checklists e relatórios — reconhecendo padrões automaticamente — complementando o Domínio sem substituí-lo.

Nesta primeira etapa, NÃO altere arquivos. Apenas analise o projeto atual.

Verifique:
1. Estrutura atual do arquivo/projeto.
2. Funcionalidades existentes.
3. O que pode ser reaproveitado.
4. O que deve ser removido por segurança, especialmente campos de senha GOV.br/e-CAC/prefeitura.
5. Onde falta separação por contabilidadeId.
6. Como transformar o app em produto multiempresa.
7. Onde futuramente incluir um campo opcional de API keys do cliente, sem criar dependência.
8. Quais riscos técnicos existem.
9. Qual é o menor plano seguro de evolução.

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

## 13. Critério de sucesso

O projeto será considerado bem estruturado quando:

- o Assistente Contábil funcionar 100% sozinho, sem nenhuma dependência externa;
- cada contabilidade tiver dados separados;
- clientes/documentos/pendências/guias estiverem organizados;
- exportações funcionarem;
- não houver senhas sensíveis armazenadas;
- o eventual recurso de chat/IA puder ser ativado como plus (via API keys do próprio cliente), sem quebrar o produto básico;
- o produto puder ser demonstrado e vendido para escritórios reais.

## 14. Resumo executivo

O Assistente Contábil será um software operacional vendável para escritórios de contabilidade e firmas pequenas.

Ele organiza clientes, documentos, pendências, guias, débitos, mensagens, checklists e relatórios, reconhecendo padrões automaticamente.

Ele complementa o Domínio, preparando informações antes das rotinas oficiais.

O sistema é 100% independente e funciona sozinho, sem depender de nenhuma API ou IA externa.

Se o produto ganhar futuramente um chatbox ou recurso de IA, ele entra apenas como um campo simples de configuração onde o cliente cadastra quantas API keys quiser, das ferramentas que já tiver à disposição — sem nunca virar dependência.

A arquitetura deve ser multiempresa e segura.

Contexto de oportunidade: 2026 marca o início da Reforma Tributária (IBS/CBS) — escritórios pequenos vão precisar se organizar rápido diante das mudanças, o que reforça a proposta de valor do produto.

Visão final:

```text
Cliente manda bagunça.
Assistente Contábil reconhece padrões e organiza.
Equipe confere.
Domínio recebe informação pronta.
```
