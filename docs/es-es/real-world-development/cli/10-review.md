---
title: "Lección 10 - Recapitulación y siguientes pasos"
description: "Recapitula el flujo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado la interfaz de línea de comandos (CLI) de GitHub Copilot durante un flujo de trabajo continuo en Tailspin Toys. En concreto:

- preparaste un Codespace, instalaste Copilot CLI, exploraste el proyecto y encontraste la incidencia de filtrado.
- añadiste valoraciones con estrellas, revisaste el resultado en un navegador reenviado y combinaste manualmente tu primera solicitud de incorporación de cambios (PR).
- partiste de la incidencia de filtrado, definiste el enfoque en Plan, creaste la funcionalidad en Autopilot y revisaste el resultado en Interactive.
- guiaste al agente con instrucciones personalizadas, personalizaste la aptitud `quality-checks` y la utilizaste para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- añadiste el servidor Model Context Protocol (MCP) de Playwright y lo usaste para explorar el filtrado en un navegador real.
- creaste y seleccionaste un agente personalizado de aseguramiento de la calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la aptitud y las evidencias del navegador.
- revisaste el cambio completo de filtrado y autorizaste Agent Merge para combinar su PR.
- exploraste comandos de barra para el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

## Lo que entregaste

El taller tiene dos hitos de PR, cada uno en su propia rama basada en `main` actualizado:

1. **Valoraciones con estrellas:** muestra `starRating` y un estado explícito sin valoración en las tarjetas de juegos.
2. **Filtrado y flujo de calidad:** implementa el filtrado, actualiza las instrucciones y aplícalas a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de QA e incluye las pruebas correspondientes.

Desde la planificación del filtrado hasta la apertura de su PR, trabajaste en la misma conversación y rama. Se agrupó el trabajo en una PR para simplificar el taller.

## Distintas formas de verificación

Comprobaste el código con pruebas automatizadas, una inspección manual en el navegador y la exploración del navegador mediante MCP. La aptitud `quality-checks` ejecutó pruebas unitarias, lint y comprobaciones de tipos, e informó de los resultados en el formato actualizado. Antes de abrir la PR, QA reunió esos resultados con una revisión de los requisitos y de la cobertura.

Las pruebas nuevas deben cubrir carencias reales; una ejecución de QA que no necesite pruebas nuevas también puede ser correcta. Revisa el código y las evidencias antes de autorizar la combinación y actualiza las evidencias afectadas después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas influyen en el trabajo de Copilot. En este taller actualizaste instrucciones, personalizaste una aptitud, creaste un perfil de QA y configuraste un servidor MCP. Reutiliza estas personalizaciones entre conversaciones y ajústalas a las necesidades del equipo. Las instrucciones establecen estándares, las aptitudes describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y resultados reales, no solo el resumen del agente.

Elige el **modo y el modelo** según la tarea. Usa **Plan** para definir un enfoque antes de construir, **Interactive** para colaborar en cambios concretos y **Autopilot** para tareas bien acotadas. Elige un modelo rápido para ediciones rutinarias y otro más capaz para tareas complejas.

El contexto importa tanto como la infraestructura. Explicar claramente *qué* quieres crear, *por qué* y *cómo* puede cambiar el resultado.

## Más ideas para explorar

Algunos comandos de CLI que puedes probar:

- `/review` pide al agente de revisión de código que analice los cambios.
- `/rubber-duck` permite razonar sobre un problema desde otra perspectiva.
- `/fleet` coordina subtareas independientes en paralelo.
- `/worktree` aísla una tarea en otro árbol de trabajo.
- `/delegate` envía una tarea a Copilot cloud agent.

## Siguientes pasos

La mejor forma de mejorar con cualquier herramienta es seguir utilizándola: en código de producción, proyectos personales o esa aplicación que llevas años queriendo crear. Comparte lo que aprendas con el equipo y sigue consultando la documentación.

Para ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. También puedes comparar otros entornos: el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller del agente en la nube][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
