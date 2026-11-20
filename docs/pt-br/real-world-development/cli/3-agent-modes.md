---
title: "Lição 3 - Modos do agente: Plan e Autopilot"
description: "Use Plan para combinar uma abordagem, Autopilot para implementar filtros a partir de uma issue e Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando uma pequena funcionalidade ao projeto, mas alterações maiores exigem um processo mais robusto. O GitHub Copilot CLI foi criado para trabalhar com o fluxo existente da organização e ajudar a construir o que é necessário da maneira adequada. Nesta lição, você iniciará um fluxo de desenvolvimento orientado por agente: usará uma issue para criar uma funcionalidade, verificará o código e o comportamento e, por fim, preparará a mesclagem.

> [!NOTE]
> Você continuará o fluxo da funcionalidade na mesma conversa e branch. Em geral, tarefas diferentes usariam branches ou PRs separados; aqui, faremos um atalho para focar nos conceitos principais.

Nesta lição, você vai:

- iniciar uma conversa do Copilot a partir de uma issue do GitHub.
- definir requisitos no modo Plan.
- implementar a funcionalidade no modo Autopilot.
- revisar o código.
- validar manualmente a funcionalidade no navegador encaminhado.

Ao continuar o trabalho, você atualizará as instruções do repositório, personalizará a skill `quality-checks`, adicionará validação MCP, criará um agente de QA e abrirá o PR da funcionalidade.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve a funcionalidade, mas detalhes como combinar categorias precisam ser acordados antes da implementação. Use Plan para definir essas decisões e, depois, autorize uma implementação com escopo limitado no Autopilot.

## Contexto

Usar agentes de codificação com inteligência artificial (IA) não muda os fundamentos do desenvolvimento de software; na verdade, torna-os ainda mais importantes. Um fluxo comum é:

1. Começar por uma issue que descreve o trabalho.
2. Planejar o que será criado.
3. Implementar e revisar o código.
4. Executar testes para validar o código.
5. Validar manualmente a funcionalidade.
6. Criar um pull request (PR).
7. Mesclar o código depois da revisão e da aprovação da integração contínua.

> [!NOTE]
> Os detalhes variam de acordo com a equipe e a organização, mas muitos fluxos seguem uma abordagem semelhante.

Esse processo ajuda a garantir que o código gerado por IA atenda aos requisitos e passe pelas mesmas verificações que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere alterações e aguarda sua resposta antes de continuar.
- **Plan**: o agente cria um plano e não pode editar os arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma, escrevendo código, executando testes e iterando até considerar a tarefa concluída.

Comece no modo Plan, revise o plano e só então use o Autopilot para implementá-lo.

## Começar pela issue

Antes de trabalhar nos filtros, prepare o Codespace, o repositório e o terminal.

1. Volte ao Codespace. Se estiver parado, reinicie-o.
2. Confirme que o PR das avaliações por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Atualize `main` e crie uma branch para os filtros:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para exibir todas as issues.
8. Use as setas para selecionar a issue **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

Observe que o prompt agora começa com `#7` (ou um número semelhante). O caractere `#` adiciona o contexto de uma issue ou de um pull request do GitHub.

## Planejar os filtros

O planejamento permite definir a abordagem antes de delegar a implementação ou outras tarefas ao Copilot. Para trabalhos complexos, vale a pena planejar.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para mudar para Plan. Confirme que o indicador abaixo do prompt mostra **Plan**.
2. Depois da referência à issue, digite:

   ```plaintext
   Crie um plano para implementar esta funcionalidade.
   ```

O Copilot explorará o projeto e determinará uma abordagem.

3. Responda às perguntas que o Copilot fizer sobre os filtros, de acordo com suas preferências.
4. Quando o plano estiver pronto, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Percorra o plano e revise-o.
6. Peça ao Copilot que revise qualquer parte que não corresponda às decisões tomadas.

## Aprovar o Autopilot

Depois de revisar o plano, autorize a implementação no Autopilot.

1. Selecione **Accept plan and build on autopilot (recommended)** ou a opção equivalente na versão instalada.
2. Confirme que o indicador abaixo do prompt mostra **Autopilot**.
3. Acompanhe o Copilot enquanto ele segue o plano, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, portanto revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revisar e verificar a implementação

Revise o código gerado antes de mesclá-lo, como faria com qualquer outro código.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme que o indicador não mostra **Plan** nem **Autopilot**.
2. Digite `/diff` e inspecione a implementação dos filtros e os testes.
3. Compare o resultado com a issue e as decisões de planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da exibição de diff.
5. Revise os resultados das verificações do projeto e peça ao Copilot que resolva as falhas.

## Explorar a funcionalidade

Inicie o aplicativo e abra o site pela porta encaminhada do Codespaces para verificar se tudo funciona.

1. Peça ao Copilot para iniciar o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa testar os filtros no navegador. Informe a URL e mantenha o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Teste os filtros por categoria, por editora e as combinações acordadas no plano.
4. Confirme que a redefinição e o comportamento sem resultados correspondem à issue e às decisões tomadas.
5. Volte ao Codespace e peça ao Copilot que pare o servidor de desenvolvimento iniciado.

## Resumo e próximos passos

Você usou diferentes modos de conversa para criar e revisar uma funcionalidade. Você:

- iniciou uma conversa do Copilot a partir de uma issue do GitHub.
- definiu requisitos no modo Plan.
- implementou a funcionalidade no modo Autopilot.
- revisou o código.
- validou manualmente a funcionalidade no navegador encaminhado.

Em seguida, [use instruções personalizadas][next-lesson] para orientar melhor a geração de código.

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
