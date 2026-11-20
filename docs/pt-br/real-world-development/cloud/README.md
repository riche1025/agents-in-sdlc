---
slug: pt-br/real-world-development/cloud
title: "Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

O **[agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** trabalha de forma assíncrona na nuvem. Você atribui o trabalho no GitHub, e o agente explora o repositório, faz alterações e abre um pull request em segundo plano enquanto você cuida de outras tarefas.

Nestes exercícios, você adicionará instruções personalizadas para o agente, atribuirá uma issue e deixará que ele implemente o trabalho. Você revisará os resultados, usará agentes personalizados para orientar a abordagem, acompanhará e direcionará sessões pelo painel de agentes e, por fim, revisará os pull requests e iterará sobre as alterações.

## Exercícios

| Exercício | Tópico | Descrição |
|----------|-------|-----------|
| [0. Pré-requisitos][ex0] | Configuração | Crie seu repositório e um codespace |
| [1. Instruções personalizadas][ex1] | Contexto | Adicione instruções personalizadas para o agente de nuvem |
| [2. Agente de nuvem][ex2] | Agente assíncrono | Atribua issues ao agente de nuvem do Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revise e use agentes personalizados |
| [4. Gerenciar agentes][ex4] | Monitoramento | Acompanhe e direcione sessões de agentes |
| [5. Iterar][ex5] | Revisão | Revise pull requests, itere no trabalho do Copilot e escolha os próximos passos |

## Pré-requisitos

Antes de participar deste workshop, verifique se você tem:

- [ ] Uma conta do GitHub com um plano ativo **Copilot Student, Pro, Pro+, Business ou Enterprise**
- [ ] O agente de nuvem do Copilot habilitado para sua conta ou organização

> [!TIP]
> Não tem um plano pago? Estudantes com status verificado podem usar o GitHub Copilot gratuitamente pelo [GitHub Education][callout-student-plan-education]. O plano **Copilot Student** inclui o agente, o Model Context Protocol (MCP), revisão de código e os recursos do Copilot CLI usados neste workshop.

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> O agente de nuvem está disponível nos planos **Copilot Student, Pro, Pro+, Business e Enterprise** — em todos, exceto no Copilot Free. No Copilot Business ou Enterprise, um administrador precisa habilitá-lo para a organização.

> [!NOTE]
> Este percurso não aborda o Model Context Protocol (MCP). Para explorar servidores MCP com o Copilot, consulte o [percurso de CLI][cli-workshop] ou o [percurso do VS Code][vscode-workshop].

[cli-workshop]: ../cli/
[vscode-workshop]: ../vscode/

## Comece

**[Comece pelos pré-requisitos do Exercício 0 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
