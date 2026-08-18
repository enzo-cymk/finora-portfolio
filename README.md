# Finora

**Controle. Planeje. Evolua.**

O **Finora** é uma aplicação de controle financeiro pessoal em desenvolvimento, criada para centralizar contas, movimentações, categorias e informações financeiras em uma única experiência.

Este repositório é o **portfólio técnico público do projeto**. O código-fonte principal permanece em repositório privado, enquanto aqui são apresentados arquitetura, decisões de engenharia, funcionalidades implementadas, evolução do produto e o uso de LLMs durante o desenvolvimento.

> 🚧 Projeto em desenvolvimento ativo. O Finora ainda não deve ser considerado pronto para produção.

## Visão geral

A proposta do Finora é permitir que o usuário tenha uma visão centralizada da própria vida financeira, combinando dados cadastrados manualmente com uma arquitetura preparada para movimentações provenientes de contas financeiras conectadas.

Atualmente, o projeto já cobre autenticação, Dashboard, contas, transações, categorização manual, regras automáticas determinísticas e uma fundação multibanco com sandbox de sincronização.

## Funcionalidades implementadas

### Autenticação e segurança

- Cadastro de usuários
- Login com Auth.js
- Hash de senha com bcrypt
- Verificação de e-mail por código de 6 dígitos
- Expiração e limite de tentativas do código
- Reenvio com cooldown
- Rate limiting
- Proteção contra enumeração no fluxo de verificação
- Sessão autenticada e proteção de rotas
- Isolamento de dados por usuário

### Interface

- Light Mode e Dark Mode
- Layout responsivo para desktop, tablet e mobile
- App Shell autenticado
- Sidebar, topbar e drawer mobile
- Sistema próprio de iconografia
- Microinterações e animações
- Suporte a `prefers-reduced-motion`

### Dashboard

O Dashboard utiliza dados financeiros reais do usuário autenticado e apresenta:

- saldo total consolidado;
- receitas e despesas do período;
- resultado financeiro;
- gastos por categoria;
- gastos por conta;
- transações recentes;
- seleção de período.

### Contas

- Cadastro e visualização de contas
- Saldo individual e consolidado
- Contas `MANUAL` e `CONNECTED`
- Diferentes tipos de conta
- Saldo derivado das movimentações financeiras

### Transações

- Transações `MANUAL` e `SYNCED`
- Receitas e despesas
- Filtros, busca, ordenação e paginação
- Agrupamento por data
- Conta, categoria, método de pagamento, instituição e origem
- Criação de transações manuais

### Categorização

O Finora possui categorização manual e uma primeira camada de automação baseada em regras determinísticas.

Exemplo:

```text
Descrição contém "UBER"
        ↓
Categoria Transporte
```

As regras pertencem ao usuário, possuem prioridade determinística e não alteram valor, natureza, conta ou identidade bancária da movimentação. Uma categoria já definida pelo usuário não é sobrescrita automaticamente.

## Arquitetura multibanco

A fundação multibanco diferencia:

```text
Contas:      MANUAL | CONNECTED
Transações:  MANUAL | SYNCED
```

O pipeline atual segue a ideia:

```text
Provider
   ↓
Adapter
   ↓
Normalização
   ↓
Ingestão
   ↓
Prisma
   ↓
Domínio financeiro
   ↓
Dashboard / Contas / Transações
```

Uma sandbox bancária foi criada para validar instituições, conexões, contas externas, movimentações e reexecução de sincronizações sem duplicidade.

> Nenhum banco real ou integração Open Finance está conectado atualmente.

Mais detalhes em [`docs/architecture.md`](docs/architecture.md).

## Stack

### Frontend

- Next.js 15
- React 19
- TypeScript
- Tailwind CSS 3
- React Hook Form
- Zod
- Radix UI

### Backend e dados

- Next.js App Router
- Auth.js / NextAuth 5
- Prisma 6
- PostgreSQL
- bcryptjs
- Resend

### Qualidade

- TypeScript strict
- ESLint
- Prisma validation
- migrations versionadas
- validações de domínio
- testes de idempotência
- auditorias de segurança
- inspeção visual e testes manuais de fluxo

## Desenvolvimento com LLMs

O Finora também funciona como um ambiente de experimentação com **Large Language Models (LLMs)** aplicados a um processo real de engenharia de software.

Ao longo do desenvolvimento foram utilizados modelos e ecossistemas como:

- OpenAI GPT / ChatGPT
- Anthropic Claude
- NVIDIA Nemotron
- MiMo

Ferramentas utilizadas para interação e orquestração incluem:

- OpenAI Codex CLI
- Claude Code
- OpenCode
- OmniRoute
- Model Context Protocol (MCP)

Essas ferramentas não são tratadas como LLMs; elas fazem parte da infraestrutura utilizada para trabalhar com os modelos.

O ciclo adotado é:

```text
planejar → implementar → auditar → corrigir → validar
```

Código sugerido por uma LLM não é considerado concluído apenas porque foi gerado. Dependendo da alteração, o processo inclui typecheck, lint, validação do Prisma, revisão de migrations, testes de regras de negócio, idempotência, ownership, segurança e validação manual no navegador.

Leia mais em [`docs/llm-development.md`](docs/llm-development.md).

## Princípios de engenharia

Algumas invariantes importantes do projeto:

- categorização não altera o fato financeiro;
- sincronização repetida não deve duplicar movimentações;
- ownership é validado no servidor;
- o cliente não controla `userId` nem campos de integração bancária;
- decisões manuais do usuário prevalecem sobre automações;
- dados de sandbox e fixtures são restritos ao desenvolvimento;
- integrações externas passam por normalização antes de chegar ao domínio.

## Interface

Screenshots reais das principais telas serão adicionados a este repositório:

- Cadastro
- Login
- Dashboard
- Contas
- Transações
- Light Mode
- Dark Mode

## Roadmap

Próximos passos incluem:

- módulo de transferências;
- orçamentos;
- relatórios financeiros;
- cartões e ciclo de faturas;
- reconciliação entre contas próprias;
- integração com provider financeiro real / Open Finance;
- sincronização automática via jobs e webhooks;
- categorização avançada;
- futuras funcionalidades de IA para sugestões e insights;
- hardening para produção distribuída.

Mais detalhes em [`docs/roadmap.md`](docs/roadmap.md).

## Código-fonte

O código-fonte principal do Finora é mantido em **repositório privado**. Este repositório público existe para demonstração técnica, documentação e avaliação em contexto de portfólio e recrutamento.

Isso permite apresentar as decisões de produto e engenharia sem publicar integralmente a implementação de um produto com potencial de exploração comercial.

## Status atual

O checkpoint público atual cobre:

**autenticação → Dashboard → contas → transações → fundação multibanco → sandbox bancária → categorização manual → regras automáticas determinísticas**

O desenvolvimento funcional está pausado imediatamente antes do módulo de **Transferências**.

## Licença

Este repositório é disponibilizado apenas para fins de portfólio, demonstração e avaliação. Consulte [`LICENSE`](LICENSE) para os termos de uso.
