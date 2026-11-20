---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo agente →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial (IA) generativa. Se uma tarefa deve ser feita de determinada forma — ou se o Copilot precisa conhecer informações adicionais — disponibilize esse contexto. Os [arquivos de instruções][instruction-files] orientam a geração de código e ajudam o Copilot a entender como realizar o trabalho.

Neste exercício, você vai:

- explorar como o contexto, as diretrizes de código e os padrões de documentação do projeto chegam ao Copilot por meio de instruções personalizadas do repositório e de arquivos com escopo de caminho.
- gerar a primeira parte dos dados para os filtros (um auxiliar de editoras) usando as instruções atuais.
- adicionar um padrão geral ao `.github/copilot-instructions.md`.
- repetir o prompt e observar como o código gerado segue o novo padrão.
- confirmar as instruções e as alterações dos filtros em `main` para usá-las no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir todos os padrões. Como o Copilot é probabilístico, o objetivo é observar a tendência de mudança após atualizar as instruções, não obter resultados idênticos.

## Arquivos de instruções

### Cenário

A Tailspin Toys tem diretrizes de desenvolvimento, como testes unitários para a camada de dados, modo escuro na interface, comentários TSDoc e um bloco de comentários no início de cada arquivo para descrever sua finalidade. Use arquivos de instruções para fornecer esse contexto ao Copilot.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot, como convenções de código, bibliotecas e estilos de comentário. Você pode criar instruções para todo o repositório ou para tipos específicos de arquivos.

Há dois tipos de arquivos:

- `.github/copilot-instructions.md`: um arquivo enviado ao Copilot em todas as solicitações do repositório. Inclua informações gerais sobre a pilha tecnológica, o projeto, as práticas recomendadas e outras orientações globais.
- `.github/instructions/*.instructions.md`: arquivos para tarefas ou tipos de arquivo específicos, como TypeScript, Astro, componentes de interface e testes.

> [!NOTE]
> No ambiente de desenvolvimento integrado (IDE), os arquivos de instruções são usados para gerar código no Copilot Chat, não para sugestões de conclusão de código ou de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam instruções do repositório e arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [aceita outros padrões de arquivos de instruções][custom-instructions-support], como AGENTS.md e CLAUDE.md.

### Práticas recomendadas para instruções

- Mantenha `copilot-instructions.md` focado em informações gerais do projeto, sua estrutura e padrões globais.
- Use `*.instructions.md` para tipos de arquivo ou tarefas específicas.
- Use linguagem natural e orientações claras, com exemplos do que o código deve ou não deve fazer.

Não há uma única maneira certa de criar instruções ou usar IA. Experimente para descobrir o que funciona no seu projeto.

> [!TIP]
> O projeto inclui instruções para tarefas como [alterações na interface][ui-instructions] e [Astro][astro-instructions]. O Copilot também pode ajudar a gerar arquivos de instruções: no VS Code, por exemplo, use **Configure Chat → Generate Agent Instructions**; no Copilot CLI, use `/init`. Para encontrar modelos, explore o [awesome-copilot][awesome-copilot].

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar os arquivos de instruções

Leia os arquivos incluídos no repositório no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Examine a descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Observe também as orientações aninhadas de **GitHub Actions Workflows**.
3. Examine a pasta `.github/instructions`, que contém instruções para Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md`. O campo `applyTo` define um padrão glob relativo à raiz do repositório; arquivos de teste TypeScript, como `**/*.test.ts`, correspondem a ele.
5. Observe as instruções específicas para testes unitários.
6. Abra `.github/instructions/drizzle.instructions.md` e examine os links para outros arquivos de instruções e exemplos do projeto. Esses caminhos são relativos ao arquivo de instruções.

> [!NOTE]
> A seção **Code formatting requirements** ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de arquivo.

## Criar uma branch

Crie uma branch para as alterações.

1. Volte ao codespace e abra um terminal com <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Crie e selecione uma branch:

   ```bash
   git checkout -b custom-instructions
   ```

## Usar o Copilot Chat antes de atualizar as instruções

Para observar o efeito das instruções, envie o prompt antes da alteração e repita-o depois.

> [!TIP]
> **Abrir o Copilot Chat**
>
> Volte ao codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa informa o que selecionar.

1. Feche as guias abertas de exercícios anteriores para limitar o contexto disponível ao Copilot.
2. Abra `src/lib/publishers.ts` para indicar onde o auxiliar deve ficar.
3. Na lista de agentes da exibição Chat, selecione **Agent** para que o Copilot possa aplicar alterações.

   ![Seletor de agente na exibição Chat](../../../_images/shared-chat-mode-selector.png)

4. Envie o prompt:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um auxiliar de acesso a dados que retorne todas as editoras, incluindo nome e id de cada uma. Aplique as alterações nos arquivos.
   ```

5. O Copilot explorará o projeto e aplicará alterações, normalmente ao arquivo do auxiliar e aos testes.
6. Observe que a função proposta usa tipos, recebe um cliente `db` como primeiro argumento e retorna uma matriz tipada de editoras. Essas convenções vêm de `.github/instructions/drizzle.instructions.md`, aplicável a `src/lib/*.ts`.
7. Observe se o código proposto não inclui comentários TSDoc nem cabeçalho de arquivo.

> [!CAUTION]
> Como o Copilot é probabilístico, ele pode incluir comentários mesmo sem a instrução. Tudo bem: o objetivo é observar a consistência após a atualização.

## Adicionar um padrão ao repositório

Adicione orientações de documentação no código ao arquivo `.github/copilot-instructions.md`.

1. Reabra `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, perto da linha 27.
3. Logo abaixo dos padrões existentes, adicione estas linhas:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve o arquivo.

> [!TIP]
> Use `.github/copilot-instructions.md` para orientações gerais do projeto e arquivos `*.instructions.md` para linguagens, tipos de arquivo ou tarefas específicas.

## Repetir o prompt e observar a diferença

Repita o mesmo prompt para ver como o Copilot aplica o novo padrão.

1. Volte ao Copilot Chat e selecione **New Chat**.
2. Selecione novamente `src/lib/publishers.ts`.
3. Envie o mesmo prompt:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um auxiliar de acesso a dados que retorne todas as editoras, incluindo nome e id de cada uma. Aplique as alterações nos arquivos.
   ```

4. Observe que o arquivo proposto começa com um bloco de comentários semelhante a:

   ```typescript
   /**
    * Auxiliares de acesso a dados de editoras da plataforma de financiamento coletivo da Tailspin Toys.
    * Fornece funções para recuperar informações de editoras do banco de dados.
    */
   ```

5. Observe que a função inclui um comentário TSDoc semelhante a:

   ```typescript
   /**
    * Retorna uma lista de todas as editoras com seus IDs e nomes.
    *
    * @param db - Cliente do banco de dados Drizzle.
    * @returns Uma promessa que é resolvida com uma matriz de objetos de editora.
    */
   ```

Você orientou o Copilot a seguir um novo padrão e aplicá-lo ao código que servirá de base para o próximo exercício.

## Confirmar as instruções e enviar a branch

Os arquivos de instruções são controlados pelo Git como os demais arquivos do repositório.

1. Abra um terminal com <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Confirme que as instruções e o auxiliar foram alterados:

   ```bash
   git status
   ```

3. Adicione e confirme as instruções e os arquivos alterados pelo Copilot para o auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Se git status mostrar outras alterações relacionadas (por exemplo, testes), adicione esses arquivos também.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie a branch:

   ```bash
   git push -u origin custom-instructions
   ```

## Criar e mesclar um pull request

Peça ao Copilot que encontre a issue relacionada ao padrão de documentação, crie um pull request (PR) vinculado a ela e faça a mesclagem.

> [!NOTE]
> Este é o primeiro exercício em que o Copilot executa ações no GitHub. O modelo do projeto já conecta as ferramentas do GitHub ao workspace. Na primeira utilização, o VS Code pode pedir que você entre no GitHub. Siga as instruções. Você conhecerá o Model Context Protocol (MCP) em outro exercício.

1. Abra o Copilot Chat no codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) e confirme que **Agent** está selecionado.
3. Peça ao Copilot para localizar a issue e criar um PR da branch atual, descrevendo as instruções e o auxiliar de editoras:

   ```plaintext
   Encontre a issue relacionada à atualização do arquivo de instruções. Crie um pull request a partir da branch atual, informe que ele fecha essa issue e mencione também a base do auxiliar de editoras para o próximo trabalho com filtros.
   ```

4. Aguarde o Copilot localizar a issue e criar o PR.
5. Quando solicitado a permitir ações do GitHub, revise o comando e selecione **Allow** se estiver de acordo.
6. Depois da criação do PR, peça ao Copilot que faça a mesclagem e atualize a branch local:

   ```plaintext
   Mescle o PR em main. Depois, volte para main localmente e obtenha o código mais recente.
   ```

7. Revise os comandos e selecione **Allow** quando o Copilot solicitar autorização para ações do GitHub ou comandos do shell.

Você criou e mesclou um pull request com a ajuda do GitHub Copilot.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções e usou o Copilot Chat no VS Code para:

- examinar como as instruções personalizadas do repositório e as instruções com escopo de caminho chegam ao Copilot.
- enviar um prompt de geração de código e observar os resultados com as instruções existentes.
- adicionar um padrão geral a `.github/copilot-instructions.md`.
- repetir o prompt e observar o código seguir o novo padrão.
- confirmar as instruções e a base do auxiliar de editoras em `main`.

Em seguida, use essas instruções no [modo agente][next-lesson] para implementar uma funcionalidade em várias partes do código.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
