---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes especializados en tareas o ámbitos concretos del desarrollo. Sus archivos Markdown, en `.github/agents`, proporcionan instrucciones, prácticas recomendadas, patrones de código y conocimientos específicos. Los equipos pueden convertir sus conocimientos en agentes reutilizables: por ejemplo, un agente de accesibilidad que aplique las [pautas de accesibilidad para el contenido web (WCAG, por sus siglas en inglés)][wcag], uno de seguridad o uno de pruebas.

Los agentes se definen en archivos de `.github/agents` o globalmente en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, al menos, `name` y `description`, seguido de instrucciones Markdown que describen el comportamiento, la experiencia y las pautas del agente.

### Agentes personalizados y aptitudes

Los agentes y las [aptitudes][agent-skills-concept] tienen puntos en común, pero cumplen funciones distintas: un **agente personalizado** es el trabajador y las **aptitudes** son herramientas. Un agente tiene su propia ventana de contexto y puede coordinar aptitudes y otros agentes. En este taller, el agente de accesibilidad revisará y actualizará el sitio; podría usar una aptitud para gestionar PR o ejecutar pruebas.

> [!NOTE]
> No hay una única forma correcta de escribir un agente personalizado. Pruébalo e itera para encontrar lo que funcione en tu entorno y tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En este ejercicio:

- revisarás cómo se definen los agentes personalizados.
- asignarás una tarea a un agente personalizado.

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible a personas con distintas capacidades y preferencias visuales. Algunos usuarios encuentran difícil leer el tema oscuro por el bajo contraste. El equipo de diseño solicita un modo de alto contraste que se pueda activar y desactivar. Utilizarás un agente personalizado para implementar la funcionalidad.

## Revisa el agente de accesibilidad

Ya hay un agente personalizado de accesibilidad en el proyecto. Revisa sus instrucciones para comprender cómo guiarán a Copilot.

1. Vuelve a tu Codespace y abre `.github/agents/accessibility.md`.
2. Revisa los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

3. Revisa las responsabilidades, las prácticas de accesibilidad, los ejemplos de HTML, CSS y JavaScript, y los errores habituales.

## Crea y asigna una incidencia

Mission control permite asignar tareas, supervisar el trabajo y orientar al agente.

1. Abre tu repositorio en GitHub.
2. Selecciona **Issues** > **New issue** y, después, **Blank issue**.
3. Escribe `Add high contrast mode to website` en **Title**.
4. En **Description**, escribe:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

5. Selecciona **Create**.
6. En el panel derecho, selecciona **Assign to Copilot**.
7. Selecciona **Accessibility agent** y, después, **Assign**.

![Captura de pantalla de la asignación del agente en la nube, con las opciones de agente personalizado y de accesibilidad resaltadas](../../../_images/ex5-select-custom-agent.png)

Copilot empezará a trabajar en segundo plano.

## Resumen y siguientes pasos

Has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes especializados que permiten codificar y reutilizar las prácticas del equipo. En este ejercicio:

- revisaste cómo se definen los agentes personalizados.
- asignaste una tarea a un agente personalizado.

A continuación, [supervisarás y guiarás la sesión del agente desde Mission control][next-lesson]. El agente en la nube también puede usar [servidores de Model Context Protocol (MCP)][cloud-agent-mcp] e instrucciones personalizadas.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para usar agentes personalizados][org-custom-agents]
- [Preparar la empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
