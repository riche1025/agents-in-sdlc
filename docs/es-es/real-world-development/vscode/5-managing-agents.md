---
title: "Ejercicio 5 - Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

En modo agente, GitHub Copilot explora el código, propone cambios, edita archivos y ejecuta comandos de forma autónoma. Copilot Chat en VS Code muestra las llamadas a herramientas y las ediciones en tiempo real. Puedes revisar cada diff, aceptar o rechazar los cambios y orientar la conversación con nuevos mensajes sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios propuestos.
- orientarás al agente durante la sesión para añadir un control del modo claro.

## Escenario

El agente personalizado está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita también un modo claro. En vez de iniciar otra conversación, ampliarás el trabajo de la sesión actual.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra los archivos explorados, los comandos y las ediciones que propone. Cada diff incluye los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio anterior.
2. Observa las llamadas a herramientas, las lecturas y ediciones de archivos y los comandos del terminal.
3. En cada diff, selecciona **Keep** para aceptar el cambio o **Undo** para revertirlo y pedir otro intento.
4. Abre **Files changed** en la parte superior de Chat para ver todos los archivos modificados durante la sesión.

> [!NOTE]
> Si una llamada a herramienta solicita permiso, por ejemplo, para ejecutar un comando del terminal, Copilot mostrará **Allow**. Autoriza solo los comandos que consideres seguros.

5. Espera a que termine el modo de alto contraste y revisa el resumen de Copilot.

## Pide al agente que añada el modo claro

Continuarás la misma conversación para que el agente conserve el contexto del trabajo, los componentes modificados, los estilos y el uso del almacenamiento local.

1. En la entrada de Copilot Chat, envía este mensaje:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. Revisa las propuestas nuevas para el modo claro y acepta o revierte cada diff con **Keep** o **Undo**.
3. Si el agente toma un rumbo no deseado, detenlo con **Stop** junto a la entrada de Chat y envía una aclaración.

> [!TIP]
> Puedes orientar una sesión activa con mensajes de seguimiento para simplificar el CSS, corregir un enfoque o ampliar el alcance.

## Revisa el conjunto de cambios

Antes de confirmar el trabajo, revisa todos los archivos modificados.

1. Abre **Source Control** en VS Code.
2. Revisa la lista de archivos. Debe incluir componentes Astro, estilos y las pruebas relacionadas.
3. Inspecciona varios diffs y confirma que se aplican los patrones de accesibilidad: atributos de aplicaciones de Internet enriquecidas y accesibles (ARIA), navegación con teclado, HTML semántico y persistencia en el almacenamiento local.
4. Cuando estés satisfecho, prepara y confirma los cambios desde el panel **Source Control**. Publicarás la rama en [la lección siguiente][next-lesson].

## Resumen y siguientes pasos

Has supervisado y guiado una sesión activa de Copilot Chat: revisaste cada cambio, aceptaste o rechazaste ediciones y enviaste mensajes para ampliar el trabajo sin perder el contexto.

En este ejercicio:

- supervisaste el trabajo de un agente en tiempo real.
- aceptaste y rechazaste ediciones individuales.
- orientaste la sesión mediante mensajes de seguimiento.

A continuación, [publicarás el trabajo de accesibilidad en una PR][next-lesson] y revisarás los cambios del agente local.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iteración sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
