---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisa el trabajo

Has pedido a GitHub Copilot que documente el código, añada juegos relacionados y mejore la accesibilidad con modos de alto contraste y claro. Ahora revisarás las solicitudes de incorporación de cambios (PR) y, si hace falta, pedirás mejoras.

### Escenario

Los fundamentos del diseño de software y desarrollo y operaciones (DevOps) no cambian al añadir inteligencia artificial (IA) generativa. Revisa el código generado y sigue el proceso habitual antes de activar la revisión del equipo.

## Seguridad y Copilot cloud agent

El agente trabaja de forma asíncrona y sin supervisión, por lo que existen medidas de seguridad:

- Copilot tiene acceso de lectura al repositorio y acceso de escritura **solo** a la rama que usa para sus cambios.
- El agente se ejecuta en GitHub Actions en un entorno efímero independiente.
- Una persona debe aprobar los flujos de GitHub Actions antes de que se ejecuten.
- [El acceso a recursos externos está limitado de forma predeterminada][agent-firewall], incluidos los servidores de Model Context Protocol (MCP).

## Revisa la documentación generada

Empieza por la primera solicitud de incorporación de cambios (PR) del agente, que añade documentación al código.

> [!NOTE]
> Es posible que la PR muestre un aviso de que Copilot está bloqueado por un firewall. Es lo esperado: el acceso a recursos externos, incluidas las llamadas a servidores MCP, está limitado de forma predeterminada. Si quieres, puedes [personalizar o deshabilitar el firewall][agent-firewall].

1. Vuelve a tu repositorio en github.com y selecciona **Pull Requests**.
2. Abre la PR titulada, por ejemplo, **Add missing documentation**.
3. Si la PR todavía muestra **[WIP]**, espera a que el agente termine.
4. Selecciona la pestaña **Files changed** y revisa los cambios.

   ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Revisa la documentación TSDoc, las convenciones de TypeScript y los encabezados de archivo. Estos cambios siguen las instrucciones personalizadas que revisaste al principio del ejercicio 2.
6. Vuelve a **Conversation** y desplázate hacia abajo. Si hay flujos pendientes de aprobación, selecciona **Approve and run workflows**.

   ![Botón Approve and run workflows](../../../_images/shared-approve-workflows.png)

7. Espera a que se pongan en cola las comprobaciones y verifica que se superen para la aplicación Astro. Puede tardar varios minutos.

## Pide cambios a GitHub Copilot

Puedes mencionar a Copilot en comentarios de la PR o en comentarios en línea para que inicie otra sesión. Por ejemplo, puedes pedir encabezados de archivo, comentarios TSDoc en archivos TypeScript y Astro o un README que explique la estructura de la aplicación Astro.

1. Añade un comentario que mencione a **@copilot** y solicite una mejora de la documentación.
2. Selecciona **View Session** para observar la nueva sesión y sus cambios.
3. Selecciona **Back to pull request** para volver a la PR.
4. Cuando Copilot termine, confirma que haya una nueva confirmación.
5. Selecciona **Files changed** y revisa los cambios.

![Botón Back to pull request](../../../_images/ex7-back-to-pr.png)

Puedes iterar hasta que el resultado sea satisfactorio. Después, puedes marcar la PR como lista para revisión y combinarla.

![Opción para marcar la PR como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Revisa la PR de la incidencia para mostrar juegos relacionados en la página de detalles.

1. Vuelve al repositorio de GitHub y selecciona **Pull Requests**.
2. Abre la PR titulada, por ejemplo, **Show related games on the game details page**.
3. Selecciona **Files changed** y revisa el código generado.
4. Vuelve a **Conversation**. Si hay flujos pendientes, selecciona **Approve and run workflows**.
5. Comprueba que las comprobaciones de la aplicación Astro se superen.
6. **Opcional:** Para probarlo manualmente en Codespace, sustituye `<branch-name>` por la rama del agente, como `copilot/fix-8`, y ejecuta:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Puedes pedir cambios adicionales mediante un comentario en **Conversation**, como ajustar el número de juegos mostrados o añadir encabezados y comentarios TSDoc. Recuerda que esta tarea se asignó antes de actualizar las instrucciones.

## Revisa las funciones de accesibilidad

La PR de accesibilidad debe incluir el modo de alto contraste de este ejercicio y el modo claro que solicitaste desde Mission control.

1. En GitHub, selecciona **Pull Requests** y abre la PR titulada, por ejemplo, **Add high contrast mode to website**.
2. Si la PR aún muestra **[WIP]**, espera a que termine el agente.
3. Selecciona **Files changed** y revisa:
   - los controles para cambiar de modo.
   - el uso del almacenamiento local para guardar las preferencias.
   - los cambios de hojas de estilo en cascada (CSS) para los modos claro y de alto contraste.
   - los atributos de accesibilidad, la navegación con teclado y el código que controla los modos.
4. Vuelve a **Conversation** y, si hay flujos pendientes, selecciona **Approve and run workflows**.
5. Comprueba que las verificaciones de la aplicación Astro se superen.
6. **Opcional:** Para probar manualmente la accesibilidad, cambia a la rama del agente:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

7. Inicia la aplicación y prueba los controles de los modos claro y de alto contraste. Comprueba que funcionen y que la preferencia se conserve al recargar la página.

Si detectas problemas de accesibilidad, menciona a **@copilot** en un comentario y solicita cambios.

## Ejercicio opcional: sigue delegando

El agente en la nube puede trabajar en incidencias reales del backlog mientras te ocupas de otras tareas. Crea incidencias y asígnaselas a Copilot. Por ejemplo:

- crear un formulario de interés para la página de detalles del juego.
- implementar la paginación de la lista de juegos.
- añadir validación de entradas y gestión de errores a los métodos de acceso a datos.

## Resumen

Has completado el itinerario del agente en la nube. En estas lecciones:

- inspeccionaste las instrucciones personalizadas del repositorio para ver su efecto en el agente.
- asignaste incidencias a Copilot cloud agent y observaste cómo preparaba el entorno, planificaba y trabajaba de forma asíncrona.
- creaste y utilizaste un agente personalizado de accesibilidad para los modos de alto contraste y claro.
- usaste la página de agentes para supervisar y dirigir la sesión.
- revisaste e iteraste sobre las PR del agente y aprobaste los flujos de trabajo.

## Revisión y siguientes pasos

Si quieres seguir explorando, los otros itinerarios complementan lo que has practicado:

- [Itinerario de VS Code](../../vscode/): explora el modo agente de Copilot Chat y la integración de MCP desde el entorno de desarrollo integrado (IDE).
- [Itinerario de interfaz de línea de comandos (CLI)](../../cli/): entrega dos cambios revisados desde el terminal con Plan, Autopilot, aptitudes, agente de QA, Playwright MCP, Agent Merge y la delegación opcional `/delegate`.

En tu propio repositorio, puedes asignar al agente una incidencia de refactorización o cobertura de pruebas, crear un agente para otro ámbito o preparar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el entorno del agente en la nube][cloud-agent-best-practices]
- [Configurar el firewall del agente en la nube][agent-firewall]

---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

[previous-lesson]: ../4-managing-agents/
[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
