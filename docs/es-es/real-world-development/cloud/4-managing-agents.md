---
title: "Ejercicio 4 - Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has asignado al agente en la nube tres tareas relacionadas con la experiencia de usuario y nuevas funcionalidades. Aunque trabaja de forma asíncrona y autónoma, es importante supervisar las tareas.

Puedes usar varias herramientas para gestionar el trabajo, incluida la [página de agentes][agents-page] de GitHub.com. En este centro de control puedes ver las tareas de agentes con solicitudes de incorporación de cambios (PR) abiertas, revisar sus operaciones y orientar las sesiones en curso.

En este ejercicio:

- explorarás la página de agentes para supervisar las tareas.
- dirigirás una sesión activa para solicitar otra funcionalidad.

## Escenario

Después de asignar el modo de alto contraste, el equipo también quiere un modo claro. Como el agente ya está actualizando los estilos e incorporando controles, pedirás que añada el modo claro además del de alto contraste.

## Revisa las tareas del agente en la nube

Comprueba el estado de las tareas asignadas a Copilot.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa la lista de tareas en los paneles principal e izquierdo. Deben aparecer las tareas que asignaste, como documentar el código, crear interfaces de programación de aplicaciones (API) para modificar juegos y añadir un modo de alto contraste.
3. Selecciona una tarea activa y revisa las acciones que ha realizado Copilot, como obtener el código, preparar el entorno, configurar servidores de Model Context Protocol (MCP) y completar el trabajo.

> [!NOTE]
> Los pasos concretos varían según el estado de la tarea y el enfoque del agente.

4. Revisa también el panel de PR, que muestra la solicitud y los archivos modificados.

## Dirige al agente en la nube

Pide que el agente añada el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión de alto contraste. El título puede variar según el nombre y el estado de la tarea.
2. Espera unos minutos a que termine la configuración y empiece el trabajo.
3. En el cuadro **Steer active session while Copilot is working**, escribe:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

4. Pulsa <kbd>Enter</kbd> para enviar el mensaje.
5. Comprueba que Copilot lo reconoce y lo incorpora al flujo de trabajo.

![Sesión de accesibilidad en Mission control](../../../_images/ex6-accessibility-session.png)

![Tarea del agente en la nube en la página de agentes, con el cuadro para dirigir la sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

## Deja que Copilot trabaje

Copilot incorporará la nueva solicitud cuando termine el paso que estaba ejecutando. La tarea puede tardar varios minutos; puedes aprovechar ese tiempo para repasar lo aprendido.

## Resumen y siguientes pasos

Has explorado la página de agentes, el centro de control para supervisar y orientar las tareas de Copilot cloud agent. En este ejercicio:

- exploraste Mission control y la página de agentes para supervisar las tareas.
- redirigiste una sesión activa para solicitar otra funcionalidad.

Cuando Copilot termine el trabajo de accesibilidad, [revisarás e iterarás sobre las PR que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
