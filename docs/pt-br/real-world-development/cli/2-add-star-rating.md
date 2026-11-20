---
title: "Lição 2 - Adicionar avaliações por estrelas: uma vitória rápida"
description: "Use o Copilot CLI para atualizar os cards de jogos, revisar a alteração no navegador encaminhado e mesclá-la como seu primeiro pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e experimentou uma conversa, faça sua primeira alteração no projeto. Os dados dos jogos já incluem uma avaliação por estrelas, mas ela ainda não aparece nos cards da página inicial. Peça ao agente que a mostre, revise a alteração e mescle-a no seu primeiro pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em uma branch de funcionalidade.
- pedir ao agente uma pequena alteração no projeto.
- revisar a alteração com `/diff`.
- executar o aplicativo e verificar a alteração no navegador encaminhado.
- abrir e mesclar seu primeiro pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação por estrelas, já exibida na página de detalhes. Os cards da página inicial mostram apenas o título, a categoria, a editora e a descrição. Como primeiro exercício, peça ao agente para mostrar a avaliação existente em cada card: uma alteração pequena e independente, ideal para sua primeira sessão.

## Estrutura de uma conversa

Uma **conversa** é o espaço em que você trabalha com o Copilot CLI em uma tarefa. Diferentemente do aplicativo Copilot, uma conversa normal da CLI usa o repositório e a branch atualmente selecionados no terminal, em vez de criar uma worktree dedicada. As conversas salvas permitem retomar a discussão; os arquivos e a branch continuam sendo o estado normal do Git no disco.

Em uma conversa, você verá seus prompts e as respostas do agente, as ferramentas usadas pelo agente para explorar e editar arquivos e as alterações que pode inspecionar com `/diff`.

## Iniciar uma conversa e solicitar a alteração

Comece uma nova conversa para implementar a funcionalidade.

1. Volte ao Codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Se o Copilot ainda não estiver em execução, use este comando:

   ```bash
   copilot --yolo
   ```

4. Inicie uma nova sessão com o comando de barra `/new` e pressione <kbd>Enter</kbd>.
5. Use este prompt:

   ```plaintext
   Mostre nos cards da lista de jogos a avaliação starRating de cada jogo, de 5. Se a avaliação for null, mostre "No rating yet". Mantenha o layout dos cards, adicione testes e execute as verificações relevantes.
   ```

O Copilot explorará o projeto, localizará os arquivos que exibem os detalhes dos jogos e fará as alterações necessárias.

## Revisar o diff

Revise todas as alterações geradas por inteligência artificial (IA) antes de mesclá-las, mesmo quando forem pequenas.

1. Digite `/diff` e inspecione cada arquivo alterado.
2. Confirme que o card mostra a avaliação numérica quando ela existe e `No rating yet` quando `starRating` é `null`.
3. Confirme que os testes cobrem os dois casos.
4. Revise os resultados das verificações executadas pelo Copilot e peça que corrija eventuais falhas.
5. Ao terminar a revisão, pressione <kbd>Esc</kbd> para sair da tela de diff.

> [!NOTE]
> Como toda ferramenta de IA generativa, o Copilot é probabilístico, não determinístico. O código exato pode variar. Revise o comportamento, sem esperar uma implementação idêntica a um exemplo.

## Verificar as alterações

Não presuma que o código funciona apenas por tê-lo lido. Peça ao Copilot para iniciar o site e examine a interface no navegador encaminhado pelo Codespaces.

1. Peça ao Copilot para iniciar o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa inspecionar a alteração das avaliações por estrelas no navegador. Informe a URL e mantenha o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme que os cards mostram as avaliações de 5.
4. Volte ao Copilot e peça que pare o servidor iniciado:

   ```plaintext
   Pare o servidor de desenvolvimento que você iniciou.
   ```

## Abrir e mesclar seu primeiro pull request

Agora que você criou a funcionalidade, abra um pull request (PR) para mesclar o código no projeto.

1. Peça ao agente padrão para confirmar a alteração:

   ```plaintext
   Confirme as alterações revisadas das avaliações por estrelas com uma mensagem de commit apropriada.
   ```

2. Digite `/pr create`. O Copilot CLI enviará o commit existente ao criar o PR e exibirá a URL.
3. Abra o PR mantendo pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e as verificações.
5. Quando estiver tudo pronto, selecione **Merge pull request** e confirme a mesclagem.
6. Volte ao Codespace e saia do Copilot CLI com `/exit`.
7. Atualize sua cópia local de `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Você entregou sua primeira alteração com o GitHub Copilot CLI. Você:

- iniciou uma conversa focada do Copilot em uma branch de funcionalidade.
- orientou o agente a alterar os cards de jogos.
- revisou a alteração com `/diff`.
- executou o aplicativo e verificou as avaliações no navegador encaminhado.
- abriu e mesclou seu primeiro pull request.

Em seguida, [comece pela issue de filtros e use os modos Plan e Autopilot][next-lesson] para criar uma funcionalidade maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
