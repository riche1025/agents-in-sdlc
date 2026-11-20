---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

Muitas organizações enfrentam dívida técnica, como problemas de segurança não resolvidos, código legado que precisa de atualização e funcionalidades paradas no backlog. O agente de nuvem do GitHub Copilot pode atualizar código e adicionar funcionalidades de forma autônoma. Ao concluir, ele abre um pull request de rascunho para revisão. Assim, você pode delegar tarefas repetitivas e se concentrar em trabalhos mais amplos.

Neste exercício, você vai explorar:

- a personalização do ambiente de geração de código.
- como garantir que as operações sejam realizadas com segurança.
- a importância de issues com escopo claro.
- como atribuir issues ao Copilot.

## Cenários

A Tailspin Toys quer resolver algumas pendências. Primeiro, o código não tem documentação: a equipe quer comentários TSDoc em todas as funções exportadas. Além disso, a equipe de design quer mostrar jogos relacionados na página de detalhes de cada jogo para testar a experiência. São tarefas que podem perder prioridade, mas que o agente de nuvem pode executar de forma assíncrona enquanto você trabalha em outras atividades.

## Conhecer o agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) executa tarefas em segundo plano de maneira semelhante a uma pessoa desenvolvedora. Você pode, por exemplo, [atribuir uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). O Copilot abre um pull request de rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar. Você pode acompanhar a sessão durante a execução ou depois que ela terminar. Quando a solução estiver pronta para revisão, o agente marcará você no pull request.

## A importância de instruções com escopo claro

O GitHub Copilot não elimina a necessidade de pensar. Mesmo tarefas aparentemente simples podem ter complexidades. [Defina cuidadosamente o escopo do trabalho para o agente de nuvem][cloud-agent-best-practices]. Trate-o como um parceiro de programação com inteligência artificial (IA): trabalhe em etapas, aprenda, experimente e adapte o processo. Os fundamentos do desenvolvimento não mudam com a IA generativa.

## Instruções personalizadas neste repositório

Antes de atribuir trabalho, examine os arquivos de instruções incluídos no repositório. Eles ajudam a entender os resultados que você revisará.

- `.github/copilot-instructions.md`: examine **Code standards**, especialmente as convenções de TypeScript e os comentários TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observe o frontmatter `applyTo`, que aplica as instruções a arquivos `**/*.test.ts`.

Ao atribuir a issue `Code lacks documentation`, observe nos resultados os comentários TSDoc, as convenções de TypeScript e os cabeçalhos de arquivo descritos nas instruções.

## Configurar o ambiente do agente de nuvem

O agente de nuvem usa o [GitHub Actions][github-actions] para configurar o ambiente de trabalho. Você pode personalizá-lo com um fluxo de configuração especial em `.github/workflows/copilot-setup-steps.yml`, executado antes de o agente começar. O projeto já inclui esse fluxo, que instala Node.js e dependências, navegadores para testes de ponta a ponta e configura o banco de dados SQLite da aplicação Astro:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões mínimas necessárias para *suas etapas*. O Copilot receberá seu próprio token para as operações dele.
    permissions:
      # Para clonar o repositório durante as etapas de configuração, por exemplo, para instalar dependências, você precisará da permissão `contents: read`. Se não clonar o repositório nessas etapas, o Copilot fará isso automaticamente depois que elas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend/aplicativo - Node.js (todo o aplicativo agora usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migre e popule o banco de dados SQLite local para que builds e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

Esse arquivo se parece com outros fluxos do GitHub, mas tem alguns detalhes importantes:

- Ele contém um único trabalho chamado `copilot-setup-steps`, executado no GitHub Actions antes de o Copilot começar a trabalhar no pull request.
- O gatilho `workflow_dispatch` permite executar o fluxo manualmente na guia **Actions** do repositório para verificar se ele funciona.

## Atribuir uma tarefa de documentação

Documentação desatualizada ou ausente é uma forma comum de dívida técnica. A criação de documentação é uma tarefa adequada para o agente de nuvem, que pode trabalhar em segundo plano.

1. Em uma nova guia do navegador, acesse o repositório no github.com.
2. Selecione a guia **Issues** e, em seguida, **New issue**.
3. Selecione **Blank issue**.
4. Defina **Title** como `Code lacks documentation`.
5. Defina **Description** como:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

6. Selecione **Create** para criar a issue.
7. À direita, selecione **Assign to Copilot** e, em seguida, **Assign**.

   ![Atribuir uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

8. Selecione a guia **Pull Requests** e abra o novo pull request (PR), com título semelhante a `[WIP]: Code lacks documentation`. Se ele ainda não aparecer, aguarde um pouco e atualize a página.
9. Aguarde a lista de tarefas criada pelo Copilot. Isso pode levar alguns minutos enquanto o agente configura o ambiente, analisa o projeto e define uma abordagem.
10. Revise a lista de tarefas e a linha do tempo do pull request para verificar se o agente começou a trabalhar.
11. Selecione **View session** para acompanhar a sessão.

   ![Exibição da sessão do Copilot](../../../_images/ex4-view-session.png)

12. Se necessário, atualize a página para ver o status. Observe o agente explorar o código, analisar o estado do projeto, planejar e criar código.

O agente trabalha de forma assíncrona, então você pode atribuir outra tarefa enquanto ele continua.

## Atribuir a tarefa de jogos relacionados

Delegue também a tarefa da equipe de design para que o agente trabalhe nela em segundo plano.

1. Volte ao repositório no github.com.
2. Abra **Issues**, selecione **New issue** e, em seguida, **Blank issue**.
3. Defina **Title** como `Show related games on the game details page`.
4. Defina **Description** como:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

5. Selecione **Create** para criar a issue.
6. Selecione **Assign to Copilot** e, depois, **Assign**.

   ![Atribuir uma issue ao Copilot](../../../_images/shared-assign-copilot.png)

O indicador 👀 no primeiro comentário da issue significa que o Copilot começou a trabalhar.

![O Copilot usa o emoji de olhos para indicar que está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

O agente está trabalhando na segunda tarefa. Ele funciona de forma semelhante a uma pessoa desenvolvedora: você não precisa acompanhá-lo continuamente, mas deve revisar o resultado quando estiver pronto.

## Resumo e próximos passos

Você explorou o [agente de nuvem do GitHub Copilot][copilot-agents], que executa tarefas de forma assíncrona. Você pode usá-lo para resolver dívida técnica, criar funcionalidades ou ajudar a migrar código entre frameworks. Você:

- personalizou o ambiente de geração de código.
- examinou a execução segura das operações.
- viu a importância de definir claramente o escopo das issues.
- atribuiu issues ao Copilot.

Enquanto o agente trabalha, passe a criar e usar agentes personalizados. O [agente de nuvem também pode usar servidores MCP][cloud-agent-mcp] e instruções personalizadas.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente de nuvem][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
