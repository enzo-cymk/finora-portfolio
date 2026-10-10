# Arquitetura do Finora

O Finora é estruturado para separar interface, regras de negócio, persistência e integrações externas.

## Visão geral

```text
Interface
   ↓
Rotas / APIs
   ↓
Validação
   ↓
Services
   ↓
Domínio financeiro
   ↓
Prisma / PostgreSQL
```

Integrações externas adicionam uma camada de adapter e normalização antes de alcançar o domínio.

## Multibanco

A arquitetura diferencia contas e transações por origem:

```text
AccountSource
├── MANUAL
└── CONNECTED

TransactionSource
├── MANUAL
└── SYNCED
```

O fluxo de ingestão segue:

```text
Provider
   ↓
Provider Adapter
   ↓
Normalização
   ↓
Ingestão
   ↓
Persistência
   ↓
Regras de enriquecimento
   ↓
Domínio financeiro
```

A categorização é tratada como enriquecimento. Ela pode alterar a interpretação da movimentação, mas não o fato financeiro recebido.

## Idempotência

A sincronização bancária foi projetada para reconhecer contas e transações já importadas, evitando duplicidade em reexecuções do mesmo provider.

Entre as identidades externas usadas pelo domínio estão combinações equivalentes a:

```text
provider + externalConnectionId
bankConnectionId + externalAccountId
accountId + externalTransactionId
```

## Ownership

Entidades financeiras são associadas ao usuário autenticado. O `userId` usado por services e APIs é obtido no servidor e não é controlado pelo client.

Quando uma operação referencia categorias ou contas, o ownership dessas relações também é validado.

## Categorização

A categorização manual e automática pode atualizar apenas a categoria da movimentação.

Ela não deve alterar:

- valor;
- natureza financeira;
- conta;
- origem;
- método de pagamento;
- identidade externa;
- saldo.

Regras automáticas determinísticas são aplicadas apenas quando não existe uma decisão de categoria anterior.

## Sandbox

Antes de conectar um provider financeiro real, o projeto utiliza uma sandbox local para validar:

- instituições;
- conexões;
- contas externas;
- movimentações sincronizadas;
- idempotência;
- cálculo de saldo;
- categorização automática.

A sandbox é restrita ao ambiente de desenvolvimento.

## Próximas evoluções arquiteturais

- reconciliação entre contas próprias;
- domínio completo de cartões e faturas;
- provider Open Finance real;
- armazenamento seguro de credenciais e tokens;
- webhooks e jobs de sincronização;
- rate limiting distribuído;
- trilha de auditoria da origem da categorização;
- IA como camada de sugestão, nunca como fonte do fato financeiro.
