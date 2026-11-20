---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Acuerda un enfoque con Plan, implementa el filtrado desde una incidencia con Autopilot y revisa el resultado en modo Interactive."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Los cambios mayores requieren un proceso más sólido que una modificación pequeña. En estas lecciones seguirás un flujo de desarrollo con agentes: partirás de una incidencia, planificarás, crearás y revisarás el código, validarás el comportamiento y prepararás una solicitud de incorporación de cambios (PR) con la interfaz de línea de comandos (CLI) de Copilot. La inteligencia artificial (IA) no elimina los fundamentos del desarrollo.

> [!NOTE]
> Usarás la misma conversación y rama durante todo el flujo de la funcionalidad. En un proyecto real normalmente se separarían las ramas o las PR por tipo de cambio; aquí se agrupan para centrarse en los conceptos principales.

En esta lección:

- iniciarás una conversación de Copilot desde una incidencia de GitHub.
- definirás los requisitos en el modo Plan.
- implementarás la funcionalidad en modo Autopilot.
- revisarás el código y validarás manualmente la funcionalidad en un navegador reenviado.

Después actualizarás las instrucciones del repositorio, personalizarás la aptitud `quality-checks`, añadirás validación MCP, crearás un agente de QA y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys crece y los visitantes necesitan filtrar juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero algunos detalles, como la combinación de categorías, deben acordarse antes de programar. Usarás Plan para concretar esas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Contexto

Los agentes de programación con IA no cambian los principios del desarrollo. El flujo habitual consiste en partir de una incidencia, planificar, crear y revisar el código, ejecutar pruebas, validar manualmente, abrir una PR y combinarla después de la revisión y de superar la integración continua (CI). Los detalles dependen del equipo, pero mantener este proceso ayuda a comprobar que el código cumple los requisitos.

## Modos de conversación

El **modo de conversación** controla la autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo:

- **Interactive**: trabajas con el agente; este propone cambios y espera tus indicaciones.
- **Plan**: el agente prepara un plan, pero no puede editar archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma, escribe código, ejecuta pruebas e itera hasta considerar que la tarea está terminada.

Empieza en Plan, revisa el plan y, después, usa Autopilot para implementarlo.

## Empieza desde la incidencia

Prepara el repositorio y el terminal antes de empezar el trabajo de filtrado.

1. Vuelve a tu Codespace y reinícialo si está detenido.
2. Confirma que la PR de valoración con estrellas está combinada.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Usa las flechas para seleccionar **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al mensaje y volver a la pestaña **Session**. La referencia, por ejemplo `#7`, añade la incidencia o PR de GitHub al contexto.

## Planifica el filtrado

La planificación permite acordar cómo implementar una funcionalidad antes de encargarla a Copilot.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar a Plan y confirma que el indicador muestre **Plan**.
2. Después de la referencia a la incidencia, escribe:

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. Responde a las preguntas de Copilot sobre el comportamiento que quieres.
4. Cuando termine el plan, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandirlo.
5. Recorre el plan y pide que revise cualquier parte que no refleje tus decisiones.

## Aprueba Autopilot

Cuando hayas revisado el plan, autoriza la implementación.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente de tu versión.
2. Confirma que el indicador muestre **Autopilot**.
3. Observa cómo Copilot sigue el plan, genera código y ejecuta pruebas.

> [!NOTE]
> Al aprobar, la implementación puede empezar inmediatamente; revisa primero el plan. Si Copilot informa de dependencias ausentes o de un conflicto de puerto, resuelve el problema antes de considerar completas las comprobaciones.

## Revisa y verifica la implementación

Revisa el código generado antes de combinarlo y comprueba el sitio.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para volver a Interactive; el indicador ya no debe mostrar Plan ni Autopilot.
2. Escribe `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones del plan.
4. Pulsa <kbd>Esc</kbd> para salir de la vista del diff.
5. Revisa las comprobaciones del proyecto y pide a Copilot que resuelva los fallos.

## Prueba la funcionalidad

Comprueba el sitio en el navegador mediante el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba los filtros por categoría, por editorial y las combinaciones acordadas en el plan.
4. Confirma que el restablecimiento y los resultados vacíos coinciden con la incidencia y tus decisiones.
5. Pide a Copilot que detenga el servidor de desarrollo que inició.

## Resumen y siguientes pasos

Has usado varios modos de conversación para crear y revisar una funcionalidad. En esta lección:

- iniciaste una conversación de Copilot desde una incidencia de GitHub.
- definiste los requisitos en Plan.
- implementaste la funcionalidad en Autopilot.
- revisaste el código.
- validaste manualmente la funcionalidad en un navegador reenviado.

A continuación, [usarás instrucciones personalizadas][next-lesson] para que el código siga las prácticas documentadas.

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
