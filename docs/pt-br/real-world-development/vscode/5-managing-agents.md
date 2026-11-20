---
title: "Exercício 5 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

No modo agente, o GitHub Copilot explora o código, propõe alterações, edita arquivos e executa comandos. O Copilot Chat no VS Code mostra essas operações em tempo real. Você pode revisar diffs, aceitar ou rejeitar alterações e orientar a conversa com prompts complementares sem sair do editor.

Neste exercício, você vai:

- acompanhar em tempo real o trabalho do agente de acessibilidade.
- revisar e aceitar as alterações propostas.
- orientar o agente durante a sessão para adicionar um controle de modo claro junto com o modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade do [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho acontece, a equipe de design solicita também um modo claro para pessoas que consideram o tema padrão escuro demais. Em vez de começar uma nova conversa, amplie o trabalho na sessão existente.

## Acompanhar o progresso do Copilot

A exibição Copilot Chat mostra as etapas do agente: arquivos explorados, comandos executados e alterações propostas. Cada edição aparece no chat com um diff e os controles **Keep** e **Undo**.

1. Volte à exibição Copilot Chat do Exercício 4.
2. Role a conversa para acompanhar as chamadas de ferramentas, leituras e edições de arquivos e comandos do terminal solicitados.
3. Quando uma edição aparecer, selecione **Keep** para aceitá-la ou **Undo** para revertê-la e permitir outra tentativa.
4. Abra **Files changed**, na parte superior do chat, para inspecionar todos os arquivos alterados.
5. Aguarde o agente concluir o modo de alto contraste. Ele apresentará um resumo das alterações.

> [!NOTE]
> Se uma chamada de ferramenta pedir permissão, como para executar um comando do terminal, o agente pausará e mostrará **Allow**. Aprove somente os comandos com os quais você concorda.

## Orientar o agente para adicionar o modo claro

Continue na mesma conversa para que o agente mantenha o contexto dos componentes, dos estilos e do padrão de armazenamento local que já criou.

1. Envie este prompt complementar no Copilot Chat:

   ```plaintext
   Bom trabalho! Agora adicione um controle de modo claro junto ao controle de alto contraste. O modo claro deve seguir o mesmo padrão, persistir no armazenamento local e estar disponível na mesma área da interface. As pessoas devem poder ativar o alto contraste e o modo claro de forma independente.
   ```

2. Observe o agente analisar as alterações já feitas e propor as alterações para o modo claro.
3. Revise cada nova edição e use **Keep** ou **Undo**.
4. Se o agente seguir uma abordagem indesejada, como refatorar os controles de modo, interrompa-o com **Stop** ao lado da entrada do chat e envie um esclarecimento.

> [!TIP]
> Orientar uma sessão em andamento é mais rápido do que recomeçar. Use prompts complementares para pedir ajustes, corrigir a abordagem ou ampliar o escopo.

## Revisar o conjunto de alterações

Revise tudo o que o agente alterou antes de confirmar o trabalho.

1. Abra **Source Control** no VS Code.
2. Revise a lista de arquivos alterados, que deve incluir componentes Astro, estilos e testes relacionados.
3. Abra alguns arquivos e examine os diffs. Confirme se a implementação segue padrões de acessibilidade, como atributos de Accessible Rich Internet Applications (ARIA), navegação por teclado, linguagem de marcação de hipertexto (HTML) semântica e persistência no armazenamento local.
4. Quando estiver satisfeito, prepare e confirme as alterações no painel Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximos passos

Você usou o modo agente do Copilot Chat para acompanhar e orientar uma sessão em andamento: revisou edições, aceitou ou rejeitou alterações e enviou prompts complementares sem perder o contexto. Você:

- acompanhou o trabalho do agente em tempo real.
- aceitou ou rejeitou edições individuais.
- orientou a sessão com prompts complementares.

Na [próxima lição][next-lesson], publique seu trabalho de acessibilidade em um pull request e revise as alterações feitas pelo agente personalizado local durante o workshop.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo agente][agent-mode]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar no trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
