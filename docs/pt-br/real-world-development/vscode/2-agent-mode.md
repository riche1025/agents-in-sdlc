---
title: "Exercício 2 - Adicionar funcionalidade com o modo agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo alterações simples em um aplicativo podem exigir mudanças em vários arquivos e a execução de testes. O modo agente do Copilot pode explorar a estrutura do projeto, atualizar arquivos, executar tarefas e corrigir problemas encontrados. Use-o para adicionar uma funcionalidade ao site.

> [!NOTE]
> O modo agente e o agente de nuvem oferecem experiências diferentes. O modo agente trabalha no ambiente de desenvolvimento integrado (IDE), permite interação e feedback rápido. O agente de nuvem trabalha de forma assíncrona, como parte da equipe, usando issues e pull requests.

Neste exercício, você vai:

- explorar como o modo agente examina o projeto, identifica arquivos e coordena alterações.
- implementar uma funcionalidade na interface e na camada de dados.
- revisar alterações e testes antes de mesclar o código.

## Cenário

À medida que a lista de jogos cresce, as pessoas precisam filtrar por categoria e editora. Você já criou um auxiliar de editoras no exercício anterior. Agora concluirá as alterações restantes na camada de dados, na interface e nos testes com o modo agente.

## Executar o site Tailspin Toys

Antes de alterar o código, explore o site para conhecer o comportamento atual. A Tailspin Toys é uma plataforma de financiamento coletivo para jogos de tabuleiro com tema de desenvolvimento. O aplicativo é um único projeto Astro, que gera páginas estáticas em HTML (HyperText Markup Language). As páginas consultam diretamente um banco de dados SQLite local com Drizzle ORM; não há uma interface de programação de aplicações (API) de backend separada nem framework de interface no cliente. Os auxiliares de acesso a dados ficam em `src/lib/`, e a interatividade usa pequenos elementos `<script>` do Astro com APIs padrão do Document Object Model (DOM).

### Iniciar o site

O comando `npm run dev` inicia o servidor de desenvolvimento Astro.

1. Volte ao codespace. Você deve estar na branch `main` após o exercício anterior.
2. Abra um terminal com <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crie uma branch para os filtros:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

   Quando o servidor Astro estiver pronto, o terminal mostrará uma mensagem semelhante a:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Se uma caixa de diálogo pedir para abrir `http://localhost:4321` em um navegador, feche-a selecionando **x**.

5. No terminal, mantenha pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecione o endereço `http://localhost:4321`.
6. Explore a lista de jogos e abra uma página de detalhes para conhecer o comportamento existente.

> [!NOTE]
> Em um codespace, o link local será encaminhado para `https://<your-codespace-name>-4321.app.github.dev/`, um túnel privado para o servidor do codespace.

### Explorar o site

A página inicial lista jogos de tabuleiro, títulos, imagens e descrições. Ao selecionar um jogo, a página de detalhes mostra mais informações, incluindo título, descrição, editora e categoria.

## Explorar o backlog com o Copilot

O modelo do projeto cria automaticamente um backlog de issues. Peça ao GitHub Copilot para exibi-lo.

> [!TIP]
> **Abrir o Copilot Chat**
>
> No codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo podem variar entre exercícios; cada etapa informa o que selecionar.

1. Na lista de agentes da exibição Chat, selecione **Agent** para que o agente planeje e implemente alterações em arquivos, execute comandos do terminal e use ferramentas.
2. Selecione **Claude Sonnet 4.5** na lista de modelos.

   ![Seletor de agente na exibição Chat](../../../_images/shared-chat-mode-selector.png)

> [!CAUTION]
> A menção a Claude Sonnet 4.5 não expressa preferência por um modelo. Ele foi usado ao criar o workshop para que as sugestões fossem relativamente consistentes. Modelos de linguagem são probabilísticos, então os resultados podem variar.

> [!NOTE]
> O Copilot pode usar um comando MCP diferente, mas ainda deve concluir a tarefa.

3. Envie:

   ```plaintext
   Mostre o backlog de itens do meu repositório do GitHub e ajude a priorizá-los de acordo com o que será mais útil para as pessoas usuárias.
   ```

4. Selecione **Continue** para permitir que o comando liste as issues.
5. Revise a lista e a priorização propostas.

## Revisar os arquivos de instruções

Antes de pedir ao agente que gere código, examine `.github/instructions/ui.instructions.md`, que fornece contexto sobre como implementar funcionalidades no site.

1. No codespace, abra `.github/instructions/ui.instructions.md`.
2. Examine a arquitetura, os princípios de design de componentes, testabilidade e acessibilidade, e os links para instruções de Astro, Tailwind CSS e Drizzle.

> [!TIP]
> Arquivos de instruções podem referenciar outros arquivos e exemplos do projeto. Os caminhos são relativos ao arquivo de instruções; isso permite reutilizar conteúdo e dividir instruções complexas.

## Implementar os filtros

A funcionalidade exige alterações na lógica de filtros da camada de dados (`src/lib/`), nos testes e na página de listagem de jogos. Execute e aprove os testes antes da mesclagem.

1. Continue a conversa atual ou selecione **New Chat**.
2. Selecione **Add Context**, **Instructions** e **ui** para adicionar o arquivo de instruções.

   ![Exemplo de seleção do arquivo de instruções da interface](../../../_images/ex3-select-instructions-file.png)

3. Confirme que **Agent** está selecionado na lista de agentes.
4. Confirme que **Claude Sonnet 4.5** continua selecionado.
5. Peça ao Copilot que implemente a funcionalidade da issue:

   ```plaintext
   Atualize o site para incluir filtros por editora e categoria de acordo com os requisitos da issue relacionada no backlog do GitHub. Já existe um auxiliar de editoras do exercício anterior; preserve e refine esse trabalho conforme necessário e conclua o restante da camada de dados, da interface e dos testes. Confirme que todos os testes passam. O servidor já está em execução, não o inicie novamente.
   ```

6. Observe o Copilot explorar o projeto, localizar auxiliares de dados, interface e testes e, em seguida, modificar arquivos e executar testes.

   ![Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> O Copilot pode levar alguns minutos para explorar o projeto, editar arquivos e executar testes. Os controles **Keep** e **Undo** podem aparecer enquanto o agente trabalha; aguarde até que ele termine antes de aceitar ou desfazer todas as alterações.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.

   ![Solicitação para confirmar a execução dos testes no painel Copilot Chat](../../../_images/ex3-agent-mode-run-tests.png)

8. É normal haver pausas ou falhas de teste durante a tarefa. O Copilot itera entre geração de código e testes até concluir o trabalho.
9. Revise o código gerado para identificar possíveis problemas.

   ![Sessão concluída do modo agente do Copilot Chat](../../../_images/ex3-agent-mode-proposed-changes.png)

> [!CAUTION]
> Revise sempre o código gerado pelo Copilot ou por outras ferramentas de inteligência artificial (IA).

10. Volte ao navegador em que o site está em execução e explore a funcionalidade.
11. Depois de confirmar o funcionamento e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximos passos

Você usou o modo agente do GitHub Copilot para adicionar funcionalidades ao site da Tailspin Toys. Você:

- implementou alterações na interface e na camada de dados.
- permitiu que o Copilot explorasse o projeto e coordenasse alterações em arquivos relacionados.
- revisou as alterações e os testes antes da mesclagem.

Em seguida, [teste a funcionalidade com o servidor Playwright MCP][next-lesson] e abra um pull request.

### Exercício extra — implementar paginação

À medida que a lista de jogos cresce, pode ser necessário adicionar paginação. Use as habilidades deste exercício e peça ao Copilot que implemente a paginação. Siga os arquivos de instruções, decida se o tamanho da página será configurável ou fixo e forneça contexto suficiente. Iterar e pedir ajustes ao Copilot faz parte do fluxo normal.

## Recursos

- [Modos ask, edit e agent do Copilot: o que fazem e quando usar cada um][choose-mode]
- [Modo agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
