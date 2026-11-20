---
title: "Lección 7 - Crea y utiliza un agente de QA"
description: "Crea un agente de QA personalizado que combine los requisitos de la incidencia, la aptitud quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has usado la aptitud `quality-checks` para ejecutar comprobaciones automatizadas y el servidor de Model Context Protocol (MCP) de Playwright para observar el filtrado en un navegador. Ahora integrarás ambas capacidades en un agente personalizado con un proceso de control de calidad (QA) definido. Trabajarás con la interfaz de línea de comandos (CLI) de Copilot.

En esta lección:

- explorarás cómo un agente personalizado utiliza instrucciones, aptitudes y herramientas MCP.
- crearás y revisarás un perfil reutilizable de aseguramiento de la calidad.
- seleccionarás el agente de QA y revisarás sus conclusiones respecto a la incidencia de filtrado.

## Escenario

Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de pruebas y el comportamiento en el navegador antes de abrir una solicitud de incorporación de cambios (PR). Un agente personalizado puede coordinar este proceso y generar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe el propósito, las instrucciones y las herramientas disponibles. En este taller definirás el rol de QA en `.github/agents/qa.agent.md`.

Las personalizaciones tienen funciones distintas: las instrucciones del repositorio describen los estándares del equipo; la aptitud `quality-checks` agrupa comprobaciones repetibles; Playwright MCP proporciona herramientas de navegador; y el perfil de QA indica cómo utilizar esas capacidades para evaluar los requisitos e informar de los resultados.

## Crea el perfil de QA

Pide a Copilot que cree un perfil reutilizable antes de abrir la PR de la funcionalidad.

1. Vuelve a tu Codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el perfil:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Inspecciona el perfil

Revisa el perfil para comprobar que Copilot ha incluido el flujo de QA y sus límites antes de usarlo.

1. Escribe `/diff` y abre `.github/agents/qa.agent.md`.
2. Revisa el frontmatter. `description` es obligatorio; `name` es opcional, pero proporciona un nombre visible al agente.
3. Confirma que las instrucciones empiezan por los requisitos y que indican seguir las instrucciones del repositorio, ejecutar `quality-checks` y utilizar Playwright MCP.
4. Confirma que el perfil exige evidencias, pide permiso antes de modificar código de implementación y prohíbe confirmar cambios o abrir PR.
5. Si falta alguna responsabilidad o límite, pide al agente predeterminado que corrija el perfil.

## Ejecuta QA respecto a la incidencia

Copilot CLI carga los agentes del proyecto al iniciar una conversación. Reanuda la conversación de filtrado para conservar el contexto de la incidencia y el plan.

1. Activa el agente con:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, quizá no aparezca en la lista. El comando anterior lo activará.

2. Pide al agente que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. Lee el informe cuando termine.

## Resumen y siguientes pasos

Has añadido un rol especializado reutilizable y revisado su trabajo. En esta lección:

- exploraste cómo se relaciona un agente personalizado con instrucciones, aptitudes y herramientas MCP.
- creaste e inspeccionaste un perfil reutilizable de QA.
- seleccionaste el agente y revisaste sus conclusiones sobre la incidencia.

Ya tienes la implementación, la actualización de la aptitud, el perfil de QA, las pruebas y el informe de verificación. A continuación, [reunirás los cambios en una PR de funcionalidad y usarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
