---
title: "Exercício 3 - Testar a funcionalidade com o servidor Playwright MCP"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Modo agente][previous-lesson] · [Próxima lição: Agentes personalizados →][next-lesson]

Você acabou de criar filtros com o modo agente. Antes de abrir um pull request (PR), confirme que a funcionalidade funciona no navegador. Conecte o **servidor Playwright do Model Context Protocol (MCP)** para que o Copilot controle um navegador real, teste a funcionalidade e, em seguida, publique sua branch e abra o PR.

Neste exercício, você vai:

- entender o Model Context Protocol (MCP) e como servidores MCP ampliam as ferramentas do Copilot.
- adicionar o servidor Playwright MCP ao workspace.
- pedir ao Copilot que teste manualmente os filtros no navegador.
- publicar a branch e abrir um pull request.

## O que é o Model Context Protocol (MCP)?

O modo agente ganha recursos quando acessa ferramentas fora do editor. O Model Context Protocol (MCP) é um padrão para conectar o Copilot a ferramentas e serviços externos.

![Diagrama da estrutura interna do modo agente e de sua interação com contexto, modelo de linguagem grande (LLM) e ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

O [MCP](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que agentes de inteligência artificial (IA) acessem informações atualizadas e executem ações em nome de quem os usa. Um servidor MCP faz a ponte entre o agente e ferramentas externas, como interfaces de programação de aplicações (APIs) ou pacotes locais.

Alguns servidores conhecidos:

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: permite gerenciar repositórios, issues e pull requests.
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: permite automatizar o navegador, navegar em páginas, preencher formulários e selecionar botões.

O GitHub mantém um [registro MCP](https://github.com/mcp) para facilitar a descoberta de servidores e as contribuições ao ecossistema.

> [!CAUTION]
> Trate servidores MCP como qualquer outra dependência. Revise o código-fonte, verifique o publicador e considere os riscos de segurança. Use somente servidores confiáveis e tenha cuidado ao conceder acesso a recursos ou operações sensíveis.

## Revisar a configuração MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste workspace do VS Code.

1. Abra `.vscode/mcp.json` no codespace.
2. Observe o servidor `github` já configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

Essa entrada veio do modelo do projeto e permitiu que o Copilot acessasse o backlog. O servidor remoto do GitHub conecta-se por HTTP, sem instalação local. Na primeira utilização das ferramentas, você precisa autenticar no GitHub.

## Adicionar o servidor Playwright MCP

O [servidor Playwright MCP][playwright-mcp-server] fornece ao Copilot um navegador controlável.

1. Em `.vscode/mcp.json`, adicione uma entrada `playwright` junto com `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Salve o arquivo.

O servidor `playwright` é local: o VS Code inicia `npx @playwright/mcp@latest`. A opção `--headless` executa o navegador sem uma janela visível, o que é necessário no codespace.

> [!NOTE]
> O projeto já usa o Playwright para testes de ponta a ponta, portanto o navegador geralmente já está instalado. Se o Copilot informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Iniciar e confiar no servidor

O VS Code inicia servidores MCP sob demanda e pode pedir que você confirme que confia neles.

1. Em `.vscode/mcp.json`, selecione **Start** acima da entrada `playwright` para iniciar o servidor e verificar a configuração.
2. Se o VS Code pedir confirmação de confiança, revise a configuração e selecione a opção para confiar no servidor.

Iniciar o servidor manualmente é opcional. Se você ignorar esta etapa, o VS Code iniciará o servidor e solicitará confiança quando o Copilot precisar das ferramentas.

## Testar a funcionalidade de filtros

Com o servidor conectado e o aplicativo em execução, peça ao Copilot para testar os filtros:

1. Envie este prompt:

   ```text
   Usando o servidor Playwright MCP, abra um navegador para o aplicativo em execução em http://localhost:4321 e verifique a nova funcionalidade de filtros de jogos:

   1. Acesse a página de jogos e observe quantos jogos aparecem.
   2. Aplique um filtro de categoria e confirme que a lista mostra somente jogos dessa categoria.
   3. Limpe o filtro e aplique um filtro de editora. Confirme que a lista é atualizada.
   4. Combine um filtro de categoria e um de editora e confirme que os resultados correspondem a ambos.

   Relate o que observou em cada etapa e indique qualquer comportamento inesperado.
   ```

O Copilot abrirá um navegador pelo servidor Playwright MCP, executará as etapas e apresentará um relatório. Compare-o com os critérios de aceitação da issue e peça correções antes de abrir o PR, se necessário.

> [!NOTE]
> O aplicativo precisa estar em execução em `http://localhost:4321`. Se o servidor de desenvolvimento tiver sido parado, inicie-o antes de enviar o prompt. Na primeira utilização, o Playwright MCP talvez precise baixar um navegador. Se estiver faltando, peça ao Copilot que execute `npx playwright install chromium` e tente novamente.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publicar a branch e criar um pull request

Depois de confirmar que a funcionalidade funciona, publique a branch `filtering-vscode`.

1. Abra **Source Control** no codespace e revise as alterações feitas pelo Copilot.
2. Selecione o ícone **+** para preparar as alterações.
3. Use o botão **Sparkle** para gerar uma mensagem de commit.
4. Selecione **Publish** para enviar a branch ao repositório.

   ![Painel Source Control mostrando as alterações](../../../_images/ex3-source-control-changes.png)

Peça ao Copilot que encontre a issue relacionada e crie um PR vinculado a ela.

1. No Copilot Chat, selecione **New Chat**.
2. Confirme que **Agent** está selecionado para permitir o uso das ferramentas do GitHub.
3. Envie:

   ```plaintext
   Encontre no repositório a issue sobre filtros por categoria e editora. Crie um pull request para a branch atual e associe-o à issue correta.
   ```

4. Selecione **Continue** quando necessário para permitir que o Copilot obtenha informações e execute operações. Na primeira utilização de uma ferramenta do GitHub, talvez seja necessário autenticar.
5. Observe o Copilot pesquisar as issues, localizar a correta e criar o PR.
6. Abra o link do PR e revise-o, mas **não o mescle ainda**.

## Resumo e próximos passos

Você aprendeu o que é MCP, adicionou o Playwright MCP ao workspace, usou-o para testar filtros no navegador e publicou a branch em um pull request. Você:

- entendeu o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionou o servidor Playwright MCP ao workspace.
- pediu ao Copilot que o usasse para testar manualmente os filtros no navegador.
- publicou a branch e abriu um pull request para o trabalho dos filtros.

Em seguida, [crie um agente personalizado][next-lesson] para tarefas focadas, como revisões de acessibilidade.

## Recursos

- [O que é MCP e por que todos estão falando sobre isso?][mcp-blog-post]
- [Servidor Playwright MCP da Microsoft][playwright-mcp-server]
- [Servidor GitHub MCP][github-mcp-server]
- [Registro GitHub MCP][mcp-registry]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
