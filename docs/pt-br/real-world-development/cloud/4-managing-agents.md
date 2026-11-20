---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nos exercícios anteriores, você pediu ao agente de nuvem do Copilot que executasse três tarefas para melhorar a experiência e adicionar funcionalidades. Embora o agente trabalhe de forma assíncrona e autônoma, é importante acompanhar o trabalho.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse centro de controle, você vê as tarefas com pull requests abertos, inspeciona as operações e orienta sessões em andamento.

Nesta lição, você vai:

- explorar a página de agentes para acompanhar as tarefas do agente de nuvem.
- orientar uma sessão em andamento e solicitar uma funcionalidade adicional.

## Cenário

Depois de atribuir o modo de alto contraste ao agente, a equipe decidiu adicionar também um modo claro. Como o agente já estava atualizando o estilo do site e adicionando controles de alternância, você vai orientá-lo para incluir o novo modo.

## Revisar as tarefas do agente de nuvem

Confira o status das tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Examine as tarefas nas áreas principal e lateral. Você deve encontrar, entre outras, a documentação do código, as APIs de jogos e o modo de alto contraste.
3. Selecione uma tarefa em andamento e revise as operações já realizadas, que podem incluir obter o código, configurar o ambiente, configurar servidores MCP e executar as etapas da tarefa.

> [!NOTE]
> As etapas exibidas variam de acordo com o estado do trabalho e a abordagem do Copilot.

4. Examine o painel do pull request (PR) à direita para acompanhar o PR e os arquivos alterados.

## Orientar o agente de nuvem

Peça ao Copilot que adicione também o controle do modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão relacionada ao modo de alto contraste. O título exato depende do nome escolhido pelo Copilot e do estado do trabalho.

   ![Sessão de acessibilidade no centro de controle](../../../_images/ex6-accessibility-session.png)

2. Aguarde até que a configuração termine e o agente comece a trabalhar.
3. Na caixa de diálogo **Steer active session while Copilot is working**, envie:

   ```plaintext
   Enquanto trabalhamos no modo de alto contraste, vamos adicionar também um modo claro. Deve haver um controle para que as pessoas selecionem o modo de exibição desejado.
   ```

   ![Tarefa do agente de nuvem na página de agentes, com a caixa de diálogo de orientação destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe o Copilot confirmar o pedido e incluí-lo no fluxo de trabalho.

## Deixar o Copilot trabalhar

O Copilot incorporará a solicitação adicional depois de concluir a etapa em andamento. Isso pode levar alguns minutos; aproveite a pausa para refletir sobre o que aprendeu.

## Resumo e próximos passos

Você explorou a página de agentes do Copilot, o centro para acompanhar e orientar tarefas do agente de nuvem. Você:

- usou a página de agentes para monitorar as tarefas.
- redirecionou uma sessão em andamento para solicitar outra funcionalidade.

Enquanto o Copilot conclui as alterações de acessibilidade, [itere nos pull requests que ele criou][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
