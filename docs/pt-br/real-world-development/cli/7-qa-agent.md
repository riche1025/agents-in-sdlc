---
title: "Lição 7 - Criar e usar um agente de QA"
description: "Crie um agente personalizado de QA que combine requisitos da issue, a skill quality-checks e o Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você usou a skill `quality-checks` para executar verificações automatizadas e o Playwright MCP para observar os filtros no navegador. Agora, combine esses recursos em um agente personalizado com um processo claro de garantia da qualidade (QA).

Nesta lição, você vai:

- explorar como um agente personalizado usa instruções, skills e ferramentas MCP.
- criar e inspecionar um perfil reutilizável de QA.
- selecionar o agente de QA e revisar as descobertas em relação à issue dos filtros.

## Cenário

A Tailspin Toys quer revisar requisitos, qualidade do código, verificações automatizadas, cobertura de testes e comportamento no navegador antes de abrir um pull request (PR). Um agente personalizado pode coordenar esse processo e gerar um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot, definida em um perfil Markdown. O perfil descreve a finalidade, as instruções e as ferramentas disponíveis. Neste workshop, você definirá a função de QA em `.github/agents/qa.agent.md` e a selecionará no Copilot CLI.

As personalizações usadas até aqui têm funções diferentes: as instruções do repositório descrevem os padrões da equipe; a skill `quality-checks` reúne verificações repetíveis; o Playwright MCP fornece ferramentas de navegador; e o perfil de QA orienta o Copilot a usar esses recursos para avaliar requisitos e relatar descobertas.

## Criar o perfil de QA

Peça ao Copilot para criar um perfil reutilizável que defina as verificações e os limites do trabalho de QA.

1. Volte ao Codespace e confirme que a conversa dos filtros está no modo Interactive.
2. Peça ao agente padrão que crie o agente:

   ```plaintext
   Crie um agente personalizado chamado QA em .github/agents/qa.agent.md. Ele deve verificar funcionalidades em relação às issues e aos requisitos acordados, seguir as instruções do repositório, executar a skill quality-checks, usar o Playwright MCP para verificar o comportamento e adicionar testes quando faltar cobertura.

   Para cada requisito, informe aprovado, reprovado ou bloqueado, com evidências. Peça autorização antes de alterar o código de implementação e não faça commits nem abra pull requests.

   Apenas crie o perfil para que eu possa revisá-lo.
   ```

## Inspecionar o perfil

Revise o perfil para confirmar que o agente seguirá o fluxo e os limites pretendidos.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. `description` é obrigatório; `name` é opcional, mas fornece um nome de exibição claro.
3. Leia as instruções e confirme que o agente começa pelos requisitos, segue as instruções do repositório, executa a skill `quality-checks` e usa o Playwright MCP.
4. Confirme que o agente apresenta evidências, pede autorização antes de alterar a implementação e não faz commits nem abre PRs.
5. Se o perfil não incluir alguma responsabilidade ou limite, peça ao agente padrão que o revise antes de continuar.

## Executar o QA para a issue

O Copilot CLI carrega agentes do projeto quando uma conversa começa. Retome a conversa dos filtros e selecione QA para que o agente use a issue e as decisões de planejamento já disponíveis.

1. Ative o agente com:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como você acabou de criar o agente, talvez ele não apareça na lista. O comando acima ainda o ativará.

2. Peça ao agente de QA que revise a funcionalidade:

   ```plaintext
   Revise a funcionalidade de filtros em relação à issue e às decisões do nosso plano. Ela está pronta para um PR?
   ```

3. Aguarde o agente concluir o trabalho.
4. Leia o relatório.

## Resumo e próximos passos

Você adicionou uma função especializada reutilizável ao fluxo e revisou o trabalho do agente. Você:

- explorou como um agente personalizado usa instruções, skills e ferramentas MCP.
- criou e inspecionou um perfil reutilizável de QA.
- selecionou o agente de QA e revisou as descobertas em relação à issue dos filtros.

Em seguida, [reúna as alterações em um PR de funcionalidade e use o Agent Merge][next-lesson].

## Recursos

- [Criar agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
