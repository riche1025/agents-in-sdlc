---
title: "Lição 6 - Validar a funcionalidade com Playwright MCP"
description: "Inspecione ou configure o Playwright MCP no Copilot CLI e use-o para explorar os filtros no navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Escrever código envolve mais do que implementar funcionalidades. Também é preciso trabalhar com dados, serviços externos e automações disponíveis ao Copilot. Os servidores MCP estendem os recursos integrados à CLI com outras ferramentas e serviços.

Nesta lição, você vai:

- entender o que é o Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionar o servidor Playwright MCP, se ele ainda não estiver disponível.
- pedir ao agente que controle um navegador e explore os filtros.

## Cenário

Testes unitários e de ponta a ponta são importantes, mas validar alterações na interface exige interagir com ela. Você permitirá que o Copilot use o site como uma pessoa usuária para automatizar a verificação do comportamento.

## O que é o Model Context Protocol (MCP)?

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de inteligência artificial (IA) se comuniquem com ferramentas e serviços externos em tempo real. Um servidor MCP funciona como uma ponte entre o agente e essas ferramentas; cada servidor oferece um conjunto diferente de ferramentas e recursos.

Alguns servidores MCP conhecidos:

- **[GitHub MCP Server][github-mcp]**: fornece acesso a interfaces de programação de aplicações (APIs) para gerenciar repositórios, issues e pull requests do GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: oferece automação de navegadores com o Playwright.

O GitHub mantém um [registro MCP][mcp-registry] para facilitar a descoberta de servidores e contribuições ao ecossistema.

> [!CAUTION]
> Trate servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique o publicador e considere as implicações de segurança.

## Adicionar o servidor Playwright MCP

Se o Playwright MCP ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site.

> [!NOTE]
> Se o Playwright MCP já estiver configurado no Copilot CLI, ignore estas etapas e continue na próxima seção.

1. Volte ao Codespace.
2. No Copilot CLI, digite:

   ```plaintext
   /mcp add
   ```

3. Digite `playwright` como nome e pressione <kbd>Tab</kbd>.
4. Confirme o tipo de servidor **STDIO** pressionando <kbd>Enter</kbd> e, em seguida, pressione <kbd>Tab</kbd>.
5. Cole isto na caixa **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair da caixa de diálogo MCP.

## Pedir ao Copilot que explore a funcionalidade com Playwright

Use o servidor Playwright MCP para repetir a verificação que você fez manualmente.

1. Envie este prompt:

   ```plaintext
   Inicie o aplicativo e use o Playwright MCP para verificar os filtros em relação à issue e ao nosso plano. Informe o que funciona e o que não funciona, sem fazer alterações. Quando terminar, pare o servidor que iniciou.
   ```

> [!NOTE]
> Em geral, não é necessário pedir explicitamente ao Copilot que use o servidor MCP; ele costuma identificá-lo. Mencioná-lo pode ajudar a orientar a tarefa.

2. Observe as etapas que o Copilot executa no navegador.
3. Leia o relatório e confirme que tudo funciona como esperado.

O Copilot iniciará o servidor, usará o Playwright para interagir com o site, interromperá o servidor e apresentará um relatório.

## Resumo e próximos passos

Você usou o servidor Playwright MCP para explorar a funcionalidade em um navegador real a partir do Copilot CLI. Você:

- entendeu o que é o Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionou o servidor Playwright MCP, se ele ainda não estava disponível.
- pediu ao agente que controlasse um navegador e explorasse os filtros.

Em seguida, [crie um agente personalizado de QA][next-lesson] que combine a skill e as ferramentas do navegador.

## Recursos

- [O que é MCP e por que todos estão falando sobre isso?][mcp-blog-post]
- [Servidor Playwright MCP da Microsoft][playwright-mcp-server]
- [Adicionar servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
