# Roadmap do Finora

O Finora está em desenvolvimento ativo. O roadmap abaixo representa a direção técnica atual do projeto e pode evoluir conforme novas decisões de produto forem validadas.

## Próximas etapas

### Transferências

- módulo visual de transferências internas;
- preservação do saldo consolidado;
- criação atômica das movimentações de saída e entrada;
- preparação para futura reconciliação entre contas próprias conectadas.

### Orçamentos e relatórios

- orçamentos por categoria;
- acompanhamento de consumo por período;
- relatórios diário, semanal, mensal e anual;
- comparações entre períodos.

### Cartões e faturas

- domínio completo de cartão de crédito;
- fechamento e vencimento;
- ciclo de fatura;
- pagamento e reconciliação;
- tratamento adequado para compras que não devem debitar conta corrente no momento da compra.

### Integrações financeiras reais

- provider Open Finance ou equivalente;
- consentimento e autenticação;
- armazenamento seguro de credenciais e tokens;
- webhooks e jobs;
- reconciliação e observabilidade da sincronização.

### Categorização

- evolução das regras determinísticas;
- merchant e MCC quando disponíveis;
- histórico da origem da classificação;
- aplicação retroativa controlada;
- sugestões de categoria com IA no futuro.

### Inteligência artificial

A IA é planejada como camada de apoio, não como fonte do fato financeiro.

Possibilidades futuras incluem:

- sugestões de categorização;
- detecção de padrões;
- insights sobre comportamento financeiro;
- alertas personalizados;
- apoio à análise de orçamento e tendências.

### Produção

Antes de uma operação distribuída em produção, ainda serão necessárias evoluções como:

- rate limiting distribuído;
- provider real de e-mail;
- gestão segura de secrets;
- observabilidade;
- estratégia de jobs e retries;
- infraestrutura e deploy;
- auditorias adicionais de segurança.
