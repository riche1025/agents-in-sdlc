---
slug: pt-br/real-world-development/cli
title: "CLI do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O **[GitHub Copilot CLI][about-copilot-cli]** coloca o GitHub Copilot no terminal como um assistente de programação agêntico. Ele explora bases de código, gera código, executa comandos e se conecta a ferramentas externas, tudo pela linha de comando.

O workshop acompanha um fluxo contínuo na Tailspin Toys: preparar o projeto no GitHub Codespaces, instalar o Copilot CLI, adicionar avaliações por estrelas e mesclar manualmente o primeiro pull request (PR); depois, planejar e implementar filtros nos modos Plan e Autopilot e revisar no modo Interactive. Você atualizará as instruções do repositório, personalizará a skill `quality-checks`, usará o Playwright Model Context Protocol (MCP) para explorar os filtros no navegador, criará um agente de garantia da qualidade (QA) e usará o Agent Merge no PR dos filtros. Por fim, explorará comandos de barra para contexto, modelos, compartilhamento e delegação opcional à nuvem.

Para manter o workshop focado, você criará dois PRs: um para avaliações por estrelas e outro para filtros, instruções, atualização da skill, perfil de QA e testes. O fluxo de filtros e qualidade permanece na mesma conversa e branch para que você possa aproveitar o trabalho ao explorar cada ferramenta. Você também pode seguir a [série opcional de três módulos com GitHub Copilot CLI e Foundry][foundry].

## Lições

| Lição | Tópico | Descrição |
| ------ | ----- | ----------- |
| [0. Pré-requisitos][ex0] | Configuração | Crie seu repositório e codespace |
| [1. Instalar o Copilot CLI][ex1] | Instalação | Instale e autentique o Copilot CLI e conheça o ambiente |
| [2. Adicionar avaliações por estrelas: uma vitória rápida][ex2] | Primeira alteração | Exiba avaliações e o estado sem avaliação e mescle seu primeiro PR |
| [3. Modos do agente: Plan e Autopilot][ex3] | Modos do agente | Planeje a funcionalidade a partir da issue, implemente com Autopilot e revise em Interactive |
| [4. Orientar o Copilot com instruções personalizadas][ex4] | Contexto | Explore e atualize as instruções e aplique-as aos filtros |
| [5. Personalizar e usar uma skill de quality-checks][ex5] | Verificações repetíveis | Explore a skill existente, altere o formato do relatório e execute-a |
| [6. Validar a funcionalidade com Playwright MCP][ex6] | Observação no navegador | Configure MCP na CLI e inspecione o comportamento dos filtros |
| [7. Criar e usar um agente de QA][ex7] | Requisitos e cobertura | Crie e selecione um perfil especializado e reúna evidências de verificação |
| [8. Criar e mesclar o PR da funcionalidade][ex8] | Revisão e mesclagem | Revise todas as alterações, crie o PR e use o Agent Merge |
| [9. Comandos de barra no GitHub Copilot CLI][ex9] | Recursos da CLI | Explore contexto, modelos, compartilhamento e delegação opcional |
| [10. Recapitulação e próximos passos][ex10] | Resumo | Revise o fluxo, as personalizações reutilizáveis e outros recursos |
| [Opcional: Incorporar o Foundry][foundry] | Agentes hospedados | Prepare um modelo, implante um agente baseado no catálogo e conecte-o ao site |

## Pré-requisitos

Antes de participar deste workshop, verifique se você tem:

- [ ] Uma conta do GitHub com um plano ativo **Copilot Student, Pro, Pro+, Business ou Enterprise**
- [ ] Permissão para criar um repositório e um Codespace
- [ ] Familiaridade básica com operações de terminal e linha de comando

> [!TIP]
> Não tem um plano pago? Estudantes verificados podem obter o GitHub Copilot gratuitamente por meio do [GitHub Education][callout-student-plan-education]. O plano **Copilot Student** inclui os recursos de agente, MCP, revisão de código e Copilot CLI usados neste workshop. Portanto, você pode concluir todos os percursos com esse plano.

> [!NOTE]
> Se você usa o Copilot Business ou o Copilot Enterprise, verifique se o administrador habilitou o Copilot CLI para uso.

## Começar

[**Comece pela Lição 0: Pré-requisitos →**][ex0]

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[foundry]: 8-foundry-agent/
[ex10]: 10-review/
[callout-student-plan-education]: https://github.com/education/students
