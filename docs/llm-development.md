# Desenvolvimento com LLMs

O Finora também é utilizado como um ambiente de experimentação com **Large Language Models (LLMs)** dentro de um processo real de engenharia de software.

## Modelos e ecossistemas utilizados

Ao longo do desenvolvimento foram experimentados:

- OpenAI GPT / ChatGPT
- Anthropic Claude
- NVIDIA Nemotron
- MiMo

## Ferramentas de apoio

Ferramentas usadas para interação, execução ou orquestração dos modelos incluem:

- OpenAI Codex CLI
- Claude Code
- OpenCode
- OmniRoute
- Model Context Protocol (MCP)

Essas ferramentas não são tratadas como LLMs. Elas fazem parte da infraestrutura utilizada para trabalhar com os modelos.

## Ciclo de trabalho

O processo adotado segue:

```text
planejar
   ↓
implementar
   ↓
auditar
   ↓
corrigir
   ↓
validar
```

Código produzido ou sugerido por uma LLM não é considerado concluído apenas porque foi gerado.

Dependendo da alteração, as validações incluem:

- TypeScript typecheck;
- ESLint;
- Prisma validate;
- revisão de migrations;
- testes de regras de negócio;
- idempotência;
- ownership;
- invariantes financeiras;
- auditorias de segurança;
- inspeção visual;
- testes manuais no navegador.

## Abordagem multi-modelo

O objetivo não é assumir que exista um único modelo melhor para todas as tarefas. Modelos diferentes são avaliados em atividades diferentes, como planejamento, implementação, debugging, revisão e auditoria.

Em algumas situações, uma tarefa pode ser iniciada com um modelo e posteriormente revisada por outro.

## Responsabilidade técnica

As LLMs são utilizadas como ferramentas dentro do processo de engenharia. Decisões de produto, arquitetura, segurança e regras financeiras são analisadas e validadas durante o desenvolvimento.

No domínio financeiro, automações e futuras funcionalidades de IA não devem alterar fatos como valor, natureza, saldo ou identidade bancária da movimentação.
