---
title: "Lição 4 - Orientar o Copilot com instruções personalizadas"
description: "Explore instruções do repositório, adicione um padrão de documentação e aplique-o ao código dos filtros."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O contexto é essencial ao trabalhar com inteligência artificial (IA) generativa. Se uma tarefa precisa ser feita de uma maneira específica, disponibilize essa orientação ao Copilot. [Arquivos de instruções][instruction-files] descrevem não apenas *o que* você quer, mas também *como* o código deve ser estruturado. Agora que você criou os filtros, explore as instruções usadas pelo Copilot, adicione um padrão de documentação e aplique-o ao código.

Nesta lição, você vai:

- explorar como as instruções do repositório e os arquivos de instruções com escopo de caminho chegam ao agente.
- atualizar o arquivo de instruções para que os padrões de codificação sejam seguidos.
- observar o impacto dos arquivos de instruções no código.

## Cenário

A Tailspin Toys tem diretrizes de desenvolvimento. Comentários devem explicar a intenção e decisões não óbvias, e funções exportadas em `db/` e `src/lib/` devem documentar seu propósito, parâmetros e valores de retorno com TSDoc/JSDoc. Componentes Astro reutilizáveis devem documentar seus contratos `Props`, e os comentários devem continuar atualizados. As orientações existentes de formatação e lint também devem ser preservadas.

Com arquivos de instruções, você fornecerá ao Copilot o contexto necessário para seguir essas práticas.

## Arquivos de instruções

As instruções personalizadas oferecem contexto e preferências ao Copilot. Você pode especificar convenções de código, bibliotecas e estilos de comentário para todo o repositório ou para tipos específicos de arquivos.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`: um único arquivo enviado ao Copilot em todas as solicitações do repositório. Inclua nele informações gerais relevantes para a maioria das solicitações.
- `.github/instructions/*.instructions.md`: arquivos com diretrizes para linguagens, tipos de arquivo ou tarefas específicas.

> [!NOTE]
> O suporte a outros formatos de instrução varia conforme o ambiente. Consulte a [referência de suporte a instruções personalizadas][custom-instructions-support] antes de depender de um formato específico.

## Explorar os arquivos de instruções do projeto

O projeto inicial já inclui arquivos de instruções. Explore-os antes de fazer alterações para perceber o efeito deles.

1. Volte ao Codespace.
2. No editor do Codespaces, não no terminal, abra `.github/copilot-instructions.md`.
3. Observe a descrição breve do projeto e as orientações de código. Elas se aplicam a todas as interações com o Copilot neste repositório.
4. Abra `.github/instructions` e examine os arquivos. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
5. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no início: ele define um padrão glob que determina a quais arquivos as instruções se aplicam.
6. Abra `.github/instructions/drizzle.instructions.md` e observe os links para outros arquivos de instruções e arquivos do projeto, que permitem dividir conjuntos maiores de diretrizes em arquivos reutilizáveis e indicar exemplos ao Copilot.

## Atualizar as instruções da equipe

Adicione ao arquivo principal `copilot-instructions.md` uma orientação para documentar o novo código TypeScript com comentários TSDoc.

1. Localize a seção **Code formatting guidance** em `.github/copilot-instructions.md`, perto da linha 35.
2. Adicione este item ao final da lista:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

O arquivo será salvo automaticamente.

## Usar as instruções atualizadas

O Copilot CLI carrega as instruções do repositório quando uma conversa começa. Encerre e retome a conversa de filtros para carregar as novas diretrizes sem perder o contexto da funcionalidade.

1. Se a conversa de filtros ainda estiver aberta, digite `/exit`. O Copilot CLI salva as conversas automaticamente.
2. Na raiz do repositório e na branch `game-filters-cli`, retome a conversa salva:

   ```bash
   copilot --resume
   ```

   Se solicitado, selecione a conversa dos filtros e confirme que a branch ativa é `game-filters-cli`.
3. Peça ao Copilot que aplique as orientações atualizadas:

   ```plaintext
   Atualizamos nossas instruções e as diretrizes de código. Atualize o código que você gerou para seguir essas orientações.
   ```

4. Digite `/diff` e revise os arquivos TypeScript alterados. Observe os comentários TSDoc recém-criados e confirme que descrevem o código corretamente.

## Resumo e próximos passos

Você explorou como o Copilot usa arquivos de instruções e aplicou um novo padrão à funcionalidade. Você:

- explorou como as instruções do repositório e os arquivos com escopo de caminho chegam ao agente.
- atualizou o arquivo de instruções para que os padrões de codificação sejam seguidos.
- observou o impacto dos arquivos de instruções no código.

Em seguida, [personalize e execute a skill reutilizável `quality-checks`][next-lesson] para executar lint e testes de maneira consistente.

## Recursos

- [Adicionar instruções personalizadas ao Copilot CLI][instruction-files]
- [Suporte a instruções personalizadas][custom-instructions-support]
- [Práticas recomendadas para instruções personalizadas][instructions-best-practices]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
