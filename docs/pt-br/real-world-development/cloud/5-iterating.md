---
title: "Exercício 5: Iterar no trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisar o trabalho

Durante este workshop, você pediu ao GitHub Copilot que documentasse o código, criasse uma seção de jogos relacionados e implementasse recursos de acessibilidade, incluindo modos de alto contraste e claro. Revise as alterações e, se necessário, dê feedback ao Copilot.

### Cenário

Os fundamentos do design de software e do DevOps continuam os mesmos com a inteligência artificial (IA) generativa. Revise o código gerado e siga o processo normal de DevOps. Antes de habilitar a revisão para o restante da equipe, examine as sugestões do GitHub Copilot para a documentação, os jogos relacionados e os recursos de acessibilidade.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente executa tarefas de forma assíncrona e sem supervisão, há restrições de segurança:

- O Copilot tem acesso de leitura ao repositório e acesso de escrita **somente** à branch que usará para o código.
- O agente de nuvem trabalha no GitHub Actions em um ambiente separado e temporário.
- Uma pessoa precisa aprovar os fluxos do GitHub Actions antes da execução.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo servidores MCP.

## Revisar a documentação gerada

Comece pelo primeiro pull request (PR) criado pelo agente: o que adiciona documentação ao código.

> [!NOTE]
> O PR pode mostrar um aviso de que o firewall bloqueou o GitHub Copilot. Isso é esperado, pois o Copilot tem acesso limitado a recursos externos, inclusive chamadas a servidores MCP. Você pode [personalizar ou desabilitar o firewall do agente de nuvem][agent-firewall].

1. Acesse o repositório no github.com.
2. Selecione **Pull Requests** e abra o PR com um título semelhante a **Add missing documentation**.
3. Se o PR ainda estiver marcado como **[WIP]**, aguarde a conclusão do trabalho do Copilot.
4. Selecione **Files changed** e revise as alterações.

   ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Examine o código atualizado. As alterações variam, mas procure comentários TSDoc, convenções de TypeScript e cabeçalhos de arquivo, conforme as instruções personalizadas que você examinou no Exercício 2.
6. Volte à guia **Conversation** e role a página para baixo.
7. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos](../../../_images/shared-approve-workflows.png)

8. Acompanhe os fluxos na seção de verificações do PR. As verificações do aplicativo Astro devem ser aprovadas; isso pode levar alguns minutos.

## Solicitar alterações ao GitHub Copilot

Você também pode mencionar o Copilot em comentários do PR ou em comentários de linha no código. O Copilot poderá iniciar outra sessão para atender ao pedido. Como os resultados são não determinísticos, o texto exato depende do que você deseja alterar. Por exemplo, você pode pedir cabeçalhos de comentário nos arquivos, comentários TSDoc em arquivos TypeScript e Astro ou um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário solicitando uma alteração na documentação gerada e mencione **@copilot**. Use uma das ideias acima ou outro pedido relacionado à documentação.
2. Selecione **View Session** para acompanhar a nova sessão do Copilot. Você também pode selecionar **Back to pull request** para voltar ao PR.

   ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

3. Quando o Copilot concluir as alterações, procure o novo commit no PR.
4. Selecione **Files changed** e revise as alterações.

Continue iterando até que o resultado esteja adequado. Depois, você pode marcar o PR como pronto para revisão e mesclá-lo em `main`.

![Marcar o PR como pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revisar a funcionalidade de jogos relacionados

Agora, revise o PR da issue para mostrar jogos relacionados na página de detalhes.

1. Volte ao repositório no GitHub.com.
2. Selecione **Pull Requests** e abra o PR com título semelhante a **Show related games on the game details page**.
3. Selecione **Files changed** e revise o código.
4. Volte à guia **Conversation**. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos](../../../_images/shared-approve-workflows.png)

5. Acompanhe as verificações até que sejam aprovadas. Isso pode levar alguns minutos.
6. **Opcional:** teste manualmente a funcionalidade no Codespace. No terminal, substitua `<branch-name>` pelo nome da branch criada pelo Copilot, como `copilot/fix-8`, e execute:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Você pode pedir alterações adicionais ao agente por meio de um novo comentário na guia **Conversation**, como ajustar a quantidade de jogos relacionados ou adicionar cabeçalhos de comentário e comentários TSDoc. Observe que essa tarefa foi atribuída antes de atualizar as instruções personalizadas.

## Revisar os recursos de acessibilidade

Por fim, revise o PR do agente personalizado de acessibilidade. Ele deve incluir o modo de alto contraste solicitado no Exercício 3 e o modo claro pedido no centro de controle no Exercício 4.

1. Acesse o repositório no GitHub.com e abra **Pull Requests**.
2. Selecione o PR com título semelhante a **Add high contrast mode to website**. Se ainda estiver marcado como **[WIP]**, aguarde o Copilot concluir.
3. Selecione **Files changed** e revise a implementação, especialmente:
   - os controles de interface para alternar os modos.
   - o uso do armazenamento local para manter as preferências.
   - as alterações de folhas de estilo em cascata (CSS) ou de estilo dos modos de alto contraste e claro.
   - os atributos de acessibilidade, como rótulos de Accessible Rich Internet Applications (ARIA) e navegação por teclado.
   - o código JavaScript/TypeScript que controla a alternância.
4. Volte à guia **Conversation**. Se houver fluxos aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos](../../../_images/shared-approve-workflows.png)

5. Acompanhe as verificações até que sejam aprovadas.
6. **Opcional:** no Codespace, obtenha e selecione a branch do Copilot:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

7. Inicie o aplicativo no navegador e teste os controles de alto contraste e modo claro. Confirme que funcionam e que as preferências persistem após recarregar a página.
8. Se encontrar problemas de acessibilidade ou oportunidades de melhoria, mencione **@copilot** em um comentário para solicitar alterações.

## Exercício opcional — continuar delegando

O agente de nuvem funciona bem quando recebe itens reais do backlog para que você possa trabalhar em outras tarefas. Crie algumas issues e atribua-as ao Copilot. Por exemplo:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo.
- implementar paginação na lista de jogos.
- adicionar validação de entrada e tratamento de erros aos auxiliares de acesso a dados.

## Resumo

Você concluiu o percurso do agente de nuvem. Você:

- examinou os arquivos de instruções personalizados para observar seus efeitos nos resultados.
- atribuiu issues ao agente de nuvem e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- criou e usou um agente personalizado de acessibilidade para adicionar modos de alto contraste e claro.
- usou a página de agentes do Copilot como centro de controle para acompanhar e orientar a sessão.
- revisou e iterou nos pull requests, mencionando `@copilot` e aprovando fluxos.

## Revisão e próximos passos

Os outros percursos complementam o que você praticou:

- **[Percurso do VS Code](../../vscode/)** — explore o modo agente do Copilot Chat e a integração com MCP no IDE.
- **[Percurso de CLI](../../cli/)** — entregue duas alterações revisadas pelo terminal, usando Plan e Autopilot, skills, um agente de QA, Playwright MCP, Agent Merge e a delegação opcional para a nuvem com `/delegate`.

No seu próprio repositório, experimente atribuir ao agente uma issue de refatoração ou cobertura de testes, criar um agente personalizado para outro domínio ou configurar `copilot-setup-steps.yml` para outra pilha tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre os agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
