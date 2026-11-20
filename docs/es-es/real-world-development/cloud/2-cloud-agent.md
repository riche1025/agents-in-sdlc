---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Muchas organizaciones acumulan deuda técnica: incidencias de seguridad pendientes, código heredado que necesita actualizaciones o funcionalidades que no se han implementado por falta de tiempo. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidades de forma autónoma. Al terminar, crea una solicitud de incorporación de cambios (PR) en borrador para que la revise un desarrollador. Así puedes delegar tareas tediosas y centrarte en otras prioridades.

En este ejercicio explorarás cómo:

- personalizar el entorno en el que se genera el código.
- garantizar que las operaciones se realicen de forma segura.
- definir incidencias con un alcance claro.
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica. El equipo quiere añadir comentarios de documentación de TypeScript (TSDoc) a las funciones exportadas de la aplicación. Además, el equipo de diseño quiere mostrar juegos relacionados —otros títulos de la misma categoría— en la página de detalles. La implementación puede ser inicial y servir para probar la experiencia de usuario (UX). Actualmente, esto supone un bloqueo, aunque hay otras incidencias de mayor prioridad.

Son tareas que suelen aplazarse y que se pueden asignar a Copilot cloud agent. El agente trabaja de forma asíncrona mientras tú te ocupas de otras tareas; después revisas su trabajo.

## Presentación de Copilot cloud agent

[GitHub Copilot cloud agent][copilot-agents] puede trabajar en segundo plano de forma parecida a un desarrollador. Puedes, por ejemplo, [asignarle una incidencia de GitHub][assign-issue]. El agente crea una PR en borrador, prepara un entorno y empieza a trabajar. Puedes consultar la sesión mientras sigue activa o después de terminar; cuando la solución esté lista, te etiquetará en la PR.

## Define bien el alcance de las instrucciones

Copilot no elimina la necesidad de pensar. Incluso las tareas aparentemente sencillas pueden ser complejas; define cuidadosamente el alcance de las tareas para el agente en la nube y trabaja por etapas, como con un programador colaborativo. Los principios del desarrollo no cambian al añadir inteligencia artificial (IA) generativa. Consulta las [prácticas recomendadas para Copilot cloud agent][cloud-agent-best-practices].

## Instrucciones personalizadas del repositorio

Antes de asignar trabajo, revisa las instrucciones que incluye el repositorio para reconocer su efecto en las PR:

1. Abre `.github/copilot-instructions.md` y revisa **Code standards**, en especial las convenciones de TypeScript y los comentarios TSDoc.
2. Abre `.github/instructions/unit-tests.instructions.md` y observa que `applyTo` aplica estas pautas a los archivos `**/*.test.ts`.

En la siguiente sección asignarás a Copilot la incidencia `Code lacks documentation`. Cuando revises la PR, fíjate en los comentarios TSDoc, las convenciones de TypeScript y los encabezados de archivo.

## Prepara el entorno de desarrollo

El agente usa [GitHub Actions][github-actions] para preparar el entorno. Puedes configurarlo con el flujo especial `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece. El proyecto ya incluye un flujo que instala Node.js y dependencias, prepara los navegadores para pruebas de extremo a extremo y configura la base de datos SQLite de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio.
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos mínimos necesarios para *tus pasos*. Copilot recibirá su propio token para las operaciones.
    permissions:
      # Para clonar el repositorio durante la configuración (por ejemplo, para instalar dependencias), necesitarás el permiso `contents: read`. Si no lo clonas aquí, Copilot lo hará automáticamente al terminar estos pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración del frontend y la aplicación: Node.js (ahora toda la aplicación utiliza Astro + Drizzle/libSQL).
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga datos iniciales en SQLite local para que la compilación y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El flujo tiene un único trabajo llamado `copilot-setup-steps`, que se ejecuta en GitHub Actions antes de que Copilot trabaje en la solicitud de incorporación de cambios (PR). El desencadenador `workflow_dispatch` permite probarlo manualmente desde la pestaña **Actions**.

## Añade documentación al código

Crear documentación es una buena tarea para delegar. Más adelante volverás para revisar los resultados.

1. En una pestaña nueva, abre tu repositorio en github.com.
2. Selecciona **Issues** y, después, **New issue**.
3. Selecciona **Blank issue**.
4. Escribe `Code lacks documentation` en **Title**.
5. Escribe esta descripción:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

6. Selecciona **Create**.
7. En el panel derecho, selecciona **Assign to Copilot** y, después, **Assign**.

   ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

8. Selecciona **Pull Requests** y abre la solicitud de incorporación de cambios (PR) que ha creado el agente, con un título similar a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la página.

   ![Detalles de la asignación de Copilot](../../../_images/ex4-assign-copilot-details.png)

9. Cuando Copilot añada la lista de tareas a la PR, revísala. Puede tardar varios minutos mientras prepara el entorno, analiza el proyecto y decide cómo resolver la incidencia.
10. En la cronología de la PR, observa que Copilot ha empezado a trabajar y selecciona **View session**.

    ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

11. Si el indicador no se actualiza, actualiza la página. Explora la sesión para ver cómo Copilot revisa el código, analiza el estado y crea los cambios.

La tarea puede tardar varios minutos. Mientras Copilot trabaja, asignarás otra incidencia y avanzarás con otras tareas.

## Añade una sección de juegos relacionados

Asigna la siguiente tarea al agente para que trabaje en ella en segundo plano.

1. Vuelve a tu repositorio en github.com y selecciona **Issues** > **New issue**.
2. Selecciona **Blank issue**.
3. Escribe `Show related games on the game details page` en **Title**.
4. Escribe esta descripción:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

5. Selecciona **Create**. En el panel derecho, selecciona **Assign to Copilot** y, después, **Assign**.
6. Observa el comentario inicial de la incidencia: el emoji 👀 indica que Copilot ha empezado a trabajar.

   ![El emoji de ojos indica que Copilot está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

No hace falta supervisar activamente al agente; revisarás su trabajo cuando termine. Ahora puedes crear y utilizar agentes personalizados.

## Resumen y siguientes pasos

Has explorado [GitHub Copilot cloud agent][copilot-agents]. Puedes asignarle incidencias para que resuelva deuda técnica, cree funcionalidades o migre código de un marco de trabajo a otro. En este ejercicio:

- personalizaste el entorno de generación de código.
- revisaste cómo se protegen las operaciones.
- exploraste la importancia de definir el alcance de las incidencias.
- asignaste incidencias a Copilot.

Mientras el agente trabaja, puedes crear y utilizar agentes personalizados. El agente en la nube también puede usar [servidores de Model Context Protocol (MCP)][cloud-agent-mcp] e instrucciones personalizadas.

## Recursos

- [Acerca de Copilot cloud agent][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de preparación del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
