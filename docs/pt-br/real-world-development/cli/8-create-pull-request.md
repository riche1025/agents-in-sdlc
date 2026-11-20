---
title: "Lição 8 - Criar e mesclar o PR da funcionalidade"
description: "Revise filtros, instruções, a skill, o perfil de QA e os testes; depois crie um PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação dos filtros, as atualizações das instruções, da skill e do perfil de garantia da qualidade (QA), além dos testes, estão salvos em uma branch. Revise tudo em conjunto e abra um pull request. Você mesclou manualmente o primeiro pull request (PR); desta vez, deixe o **Agent Merge** gerenciar o processo.

> [!NOTE]
> Em condições normais, dividiríamos a funcionalidade, as atualizações das instruções, a skill e o agente de QA em alguns PRs. Para agilizar o workshop, mantivemos todo o fluxo de filtros e qualidade em uma única conversa e branch.

Nesta lição, você vai:

- entender o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionar todas as alterações da funcionalidade e as evidências de verificação.
- criar o PR dos filtros.
- habilitar o Agent Merge somente depois da revisão e confirmar a mesclagem.

## Cenário

Durante o fluxo dos filtros, você usou o Copilot para planejar, implementar e verificar uma funcionalidade. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização da mesclagem sob o controle de quem desenvolve.

## Conhecer o Agent Merge

O **Agent Merge** automatiza o trabalho necessário para integrar um pull request. Quando habilitado, o Copilot resolve o que estiver bloqueando o PR — como verificações de integração contínua (CI) com falha, comentários de revisão e necessidade de rebase — e habilita a mesclagem automática do GitHub quando o repositório permite.

Até agora, você selecionou **Merge pull request** manualmente. Revise o trabalho e só habilite o Agent Merge quando considerar que está pronto.

## Usar o Agent Merge para gerenciar o PR

Revise o código, crie o PR e permita que o Agent Merge cuide das etapas seguintes.

1. Volte ao Codespace.
2. Abra a caixa de diálogo do agente com `/agent`.
3. Selecione **Default** e pressione <kbd>Enter</kbd>.
4. Crie um PR com `/pr create`.
5. Ative a mesclagem do agente com `/pr agentmerge`.
6. O Copilot acompanhará a integração contínua do PR e fará a mesclagem quando tudo for aprovado.
7. Confirme que o Copilot informa algo semelhante a `PR #14 was squash-merged successfully`.

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de mesclagem, configurações do repositório ou permissões ausentes. Se houver bloqueio, leia o motivo informado e conclua manualmente a mesclagem revisada quando o repositório permitir.

## Resumo e próximos passos

Você automatizou várias etapas do desenvolvimento: geração de código, testes e validação, além do processo do pull request. Você:

- conheceu o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionou as alterações completas da funcionalidade e as evidências de verificação.
- criou o PR dos filtros.
- habilitou o Agent Merge somente após a revisão e confirmou a mesclagem.

Em seguida, [explore outros comandos de barra do Copilot CLI][next-lesson] para gerenciar contexto, modelos, compartilhamento e delegação opcional à nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
