---
title: "Exercício 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot são assistentes de inteligência artificial (IA) especializados em tarefas ou domínios do fluxo de desenvolvimento. Arquivos Markdown na pasta `.github/agents` fornecem instruções, práticas recomendadas, padrões de código e conhecimento específico. As equipes podem registrar seu conhecimento em agentes reutilizáveis, como agentes de acessibilidade que seguem as Diretrizes de Acessibilidade para Conteúdo Web (WCAG), de segurança ou de testes.

Os agentes são definidos em arquivos Markdown dentro de `.github/agents` ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de instruções que definem o comportamento e a especialização do agente.

### Agentes personalizados e skills de agente

Agentes personalizados e [skills de agente][agent-skills-concept] têm algumas semelhanças: ambos usam principalmente arquivos Markdown para orientar tarefas de IA. Uma forma simples de distingui-los: o **agente personalizado** executa o trabalho; as **skills** são ferramentas.

Os agentes têm uma janela de contexto própria e podem coordenar skills e outros agentes. Neste exercício, o agente de acessibilidade revisará e atualizará o site conforme as diretrizes de acessibilidade e poderá usar, por exemplo, uma skill para o fluxo de pull requests ou para executar testes.

> [!NOTE]
> Não há uma única maneira certa de criar um agente. Teste e refine o perfil conforme o ambiente e o cenário.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Cenário

A Tailspin Toys quer que sua plataforma seja acessível a pessoas com diferentes necessidades visuais e preferências. Comentários de usuários indicaram que o tema escuro atual é difícil de ler devido ao baixo contraste entre texto e fundo. A equipe de design pediu um modo de alto contraste que possa ser ativado e desativado. Use um agente personalizado para implementar a funcionalidade.

Neste exercício, você vai:

- revisar um agente personalizado de acessibilidade existente.
- usar o agente de acessibilidade no Copilot Chat para implementar o modo de alto contraste.

## Revisar o agente personalizado de acessibilidade

Um agente de acessibilidade já foi criado. Primeiro, crie uma branch separada do trabalho dos filtros.

1. Volte ao codespace e abra um terminal.
2. Crie uma branch nova a partir de `main`:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. Abra `.github/agents/accessibility.md`.
4. Observe os campos `name` e `description` no frontmatter YAML.

> [!CAUTION]
> Os campos `name` e `description` no frontmatter são obrigatórios para agentes personalizados.

5. Examine as seções de responsabilidades, práticas recomendadas de acessibilidade, exemplos de linguagem de marcação de hipertexto (HTML), folhas de estilo em cascata (CSS) e JavaScript e erros comuns.

## Usar o agente personalizado no Copilot Chat

O VS Code mostra os agentes personalizados definidos em `.github/agents` na lista de agentes na parte inferior da exibição Copilot Chat. Selecione um agente para aplicar suas instruções e ferramentas à conversa.

> [!TIP]
> **Abrir o Copilot Chat**
>
> No codespace, abra o painel Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo podem variar entre exercícios; cada etapa informa o que selecionar.

1. Na lista de agentes da exibição Chat, selecione **Agent**, caso ainda não esteja selecionado.
2. Abra a lista de agentes na parte inferior do chat, onde aparece o agente ativo, normalmente **default**.
3. Selecione **Accessibility agent**.
4. Envie ao agente este prompt:

   ```plaintext
   Adicione um modo de alto contraste ao site. Deve haver um controle que as pessoas possam usar para ativar o alto contraste, e a preferência deve persistir após recarregar a página usando o armazenamento local do navegador.
   ```

5. O Copilot Chat explorará o código, proporá alterações e editará os arquivos do projeto. Cada edição aparecerá no chat com o caminho e um diff para revisão.
6. Observe o indicador **Files changed**, que mostra os arquivos alterados pelo agente.

> [!NOTE]
> O agente pode levar alguns minutos para editar componentes Astro, folhas de estilo em cascata (CSS) e testes. Você revisará e orientará o trabalho em andamento no próximo exercício.

## Resumo e próximos passos

Você explorou [agentes personalizados][custom-agents], assistentes especializados que registram conhecimento e padrões da equipe. Você:

- examinou como agentes personalizados são definidos.
- usou um agente personalizado no modo agente do Copilot Chat.

Em seguida, [acompanhe e oriente o trabalho do agente][next-lesson], revise as alterações enquanto são feitas e peça que ele adicione um controle de modo claro à mesma sessão.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Criar agentes personalizados no IDE][creating-custom-agents-ide]
- [Agentes personalizados no VS Code][custom-agents-vscode]
- [Configuração de agentes personalizados][custom-agents-config]
- [Agentes personalizados no awesome-copilot][awesome-copilot-agents]

---

| [← Lição anterior: Testar a funcionalidade com o servidor Playwright MCP][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
