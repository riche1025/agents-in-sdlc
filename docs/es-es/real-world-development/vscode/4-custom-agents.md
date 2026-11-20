---
title: "Ejercicio 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes especializados en tareas o ámbitos concretos del desarrollo. Sus archivos Markdown, en `.github/agents`, proporcionan instrucciones, prácticas recomendadas, patrones de código y conocimientos específicos. Los equipos pueden convertir sus conocimientos en agentes reutilizables, como un agente de accesibilidad que aplique las [pautas de accesibilidad para el contenido web (WCAG, por sus siglas en inglés)][wcag], uno de seguridad o uno de pruebas.

Los agentes se definen en archivos de `.github/agents` o globalmente en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, al menos, los campos `name` y `description`, seguido de instrucciones que definen el comportamiento y los conocimientos del agente.

### Agentes personalizados y aptitudes

Los agentes y las [aptitudes][agent-skills-concept] tienen puntos en común, pero cumplen funciones distintas: un **agente personalizado** es el trabajador y las **aptitudes** son herramientas. Un agente tiene su propia ventana de contexto y puede coordinar aptitudes y otros agentes. En este ejercicio, el agente de accesibilidad revisará el sitio y puede utilizar aptitudes para gestionar solicitudes de incorporación de cambios o pruebas.

> [!NOTE]
> No hay una única forma correcta de escribir un agente personalizado. Pruébalo e itera para encontrar lo que funcione en tu entorno y tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma sea accesible a personas con distintas capacidades y preferencias visuales. Algunos usuarios encuentran difícil leer el tema oscuro por el bajo contraste. El equipo de diseño solicita un modo de alto contraste que pueda activarse y desactivarse. Utilizarás un agente personalizado para implementar la funcionalidad.

En este ejercicio:

- revisarás el agente personalizado de accesibilidad existente.
- usarás el agente en Copilot Chat para implementar el modo de alto contraste.

## Revisa el agente de accesibilidad

El proyecto ya incluye un agente de accesibilidad. Primero crea una rama independiente para esta tarea.

1. Vuelve al Codespace y abre un terminal.
2. Crea una rama desde `main`:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. Abre `.github/agents/accessibility.md` y revisa los campos `name` y `description` del frontmatter.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios para los agentes personalizados.

4. Revisa las responsabilidades, las prácticas de accesibilidad, los ejemplos de lenguaje de marcado de hipertexto (HTML), hojas de estilo en cascada (CSS) y JavaScript, y los errores habituales.

## Usa el agente personalizado en Copilot Chat

VS Code muestra los agentes personalizados definidos en `.github/agents` en el selector de agentes de Copilot Chat.

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, abre Copilot Chat en el Codespace y selecciona **New Chat** para iniciar una conversación limpia. El modo y el modelo pueden variar según el ejercicio.

1. En el selector de agentes de Chat, selecciona **Agent**, si aún no está seleccionado.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Abre el selector de agentes en la parte inferior de la vista Chat, que muestra el agente activo; de forma predeterminada, es **default**.
3. Selecciona **Accessibility agent**.
4. Envía este prompt:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Revisa las modificaciones que Copilot propone y aplica en los archivos del proyecto.
6. Observa el indicador **Files changed** para revisar el conjunto de archivos modificados.

El proceso puede tardar varios minutos. Copilot modifica componentes Astro, CSS y pruebas relacionadas. Revisarás y orientarás el trabajo en el ejercicio siguiente.

## Resumen y siguientes pasos

Has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes especializados que permiten reutilizar las prácticas y los estándares del equipo. En este ejercicio:

- revisaste cómo se definen los agentes personalizados.
- usaste un agente personalizado en el modo agente de Copilot Chat.

A continuación, [supervisarás y guiarás el trabajo del agente][next-lesson], revisarás los cambios y añadirás un control para el modo claro en la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados en awesome-copilot][awesome-copilot-agents]

---

| [← Lección anterior: Prueba la funcionalidad con Playwright de Model Context Protocol (MCP)][previous-lesson] | [Siguiente lección: Supervisión y gestión de agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
