---
title: "Exercício 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot são assistentes de inteligência artificial (IA) especializados em tarefas ou domínios do fluxo de desenvolvimento. Arquivos Markdown na pasta `.github/agents` do repositório fornecem instruções, práticas recomendadas, padrões de código e conhecimento específico. As equipes podem registrar seu conhecimento em agentes reutilizáveis, como agentes de acessibilidade que seguem as Diretrizes de Acessibilidade para Conteúdo Web (WCAG), de segurança ou de testes.

Os agentes personalizados são definidos em arquivos Markdown dentro de `.github/agents` ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de instruções Markdown que definem o comportamento e a especialização do agente.

### Agentes personalizados e skills de agente

Agentes personalizados e [skills de agente][agent-skills-concept] se sobrepõem em alguns aspectos: ambos usam principalmente arquivos Markdown para orientar as tarefas de IA. Uma forma simples de distingui-los: o **agente personalizado** executa o trabalho; as **skills** são ferramentas.

Os agentes têm uma janela de contexto própria e podem coordenar skills e outros agentes. Neste exercício, o agente de acessibilidade revisará e atualizará o site seguindo diretrizes de acessibilidade e poderá usar, por exemplo, uma skill de fluxo de pull requests ou de execução de testes.

> [!NOTE]
> Não há uma única maneira certa de criar um agente. Teste e refine o perfil conforme o ambiente e o cenário.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

Com agentes personalizados, você explorará:

- como agentes personalizados são definidos.
- como atribuir uma tarefa a um agente personalizado.

## Cenário

A Tailspin Toys quer que sua plataforma de financiamento coletivo seja acessível a todas as pessoas. Comentários de usuários indicaram que o tema escuro atual é difícil de ler devido ao baixo contraste entre texto e fundo. A equipe de design solicitou um modo de alto contraste que possa ser ativado e desativado. Como a acessibilidade é importante, você usará um agente personalizado para implementar a funcionalidade.

## Revisar o agente personalizado de acessibilidade

Um agente de acessibilidade já foi criado. Examine o perfil para entender como ele orientará o Copilot.

1. Volte ao codespace e abra `.github/agents/accessibility.md`.
2. Observe os campos `name` e `description` no frontmatter YAML.

> [!CAUTION]
> Os campos `name` e `description` no frontmatter são obrigatórios para agentes personalizados.

3. Examine as seções seguintes, que descrevem responsabilidades, práticas recomendadas, exemplos de linguagem de marcação de hipertexto (HTML), folhas de estilo em cascata (CSS) e JavaScript e erros comuns.

## Criar e atribuir uma issue

A página de agentes é um centro de controle para atribuir tarefas ao agente de nuvem, monitorar o trabalho e orientar sessões. Atribua ao Copilot a tarefa de criar um modo de alto contraste.

1. Acesse seu repositório.
2. Abra a guia de issues e selecione **New issue**.
3. Selecione **Blank issue**.
4. Defina **Title** como `Add high contrast mode to website`.
5. Defina **Description** como:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

6. Selecione **Create**.
7. À direita, selecione **Assign to Copilot**.
8. Selecione **Accessibility agent** na lista de agentes personalizados.

   ![Atribuição ao agente de nuvem, com o agente personalizado Accessibility selecionado](../../../_images/ex5-select-custom-agent.png)

9. Selecione **Assign**. O Copilot começará a trabalhar em segundo plano.

## Resumo e próximos passos

Você explorou [agentes personalizados][custom-agents] do GitHub Copilot, assistentes especializados que registram o conhecimento e os padrões da equipe. Você:

- examinou como agentes personalizados são definidos.
- atribuiu uma tarefa a um agente personalizado.

Enquanto o Copilot implementa o modo de alto contraste, [acompanhe e oriente a sessão do agente][next-lesson] no centro de controle.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Preparar sua organização para usar agentes personalizados][org-custom-agents]
- [Preparar sua empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Lição anterior: Agente de nuvem do GitHub Copilot][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
