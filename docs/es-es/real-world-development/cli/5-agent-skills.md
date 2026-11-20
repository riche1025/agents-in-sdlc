---
title: "Lección 5 - Personaliza y usa una aptitud de comprobación de calidad"
description: "Explora la aptitud quality-checks existente, personaliza el formato de su informe y úsala para validar el filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Escribir código implica mucho más que programarlo. Ya hemos comprobado manualmente que funciona y hemos usado archivos de instrucciones para asegurarnos de que cumple nuestros estándares. Pero ¿qué hay de las pruebas, el lint y las demás partes de la integración continua (CI)?

Para este tipo de tareas, las **aptitudes de agente** son la opción ideal. Ayudan a Copilot a entender cómo ejecutar operaciones como estas.

En esta lección:

- explorarás la aptitud `quality-checks` existente.
- personalizarás el formato de sus resultados.
- volverás a cargar la aptitud y la ejecutarás.

## Escenario

Tailspin Toys usa la aptitud `quality-checks` para las pruebas unitarias, el lint y las comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las aptitudes de agente agrupan instrucciones reutilizables para tareas, scripts ejecutables y recursos complementarios que el agente carga bajo demanda. En esencia, son una carpeta con el nombre de la aptitud y un archivo Markdown llamado `SKILL.md`. El archivo contiene un frontmatter con el nombre y la descripción de la aptitud, una explicación de lo que hace y orientaciones sobre cuándo debe usarse. La carpeta también puede incluir subcarpetas con scripts y otros recursos que la aptitud utilice al ejecutarse.

> [!NOTE]
> Las carpetas y los archivos adicionales son opcionales. La aptitud `quality-checks` de Tailspin Toys solo contiene `SKILL.md`, ya que utiliza los comandos existentes del proyecto.

Las aptitudes pueden estar en la carpeta `.github/skills` del proyecto para que formen parte del repositorio y el equipo pueda compartirlas y reutilizarlas, o en la carpeta de aptitudes del usuario `~/.copilot/skills`.

## Explora la aptitud

Vamos a explorar la aptitud `quality-checks` que creó el equipo de Tailspin Toys para ejecutar pruebas unitarias, lint y comprobaciones de tipos.

1. Vuelve a tu Codespace. En el editor de Codespaces, abre `.github/skills/quality-checks/SKILL.md`.
2. Lee el `name` y la `description` de la parte superior. La descripción ayuda a Copilot a saber cuándo debe usar la aptitud.
3. Lee las instrucciones y fíjate en cómo guían a Copilot durante las pruebas y el lint.
4. Observa que la aptitud todavía no contiene una sección **Results output formatting**.

## Ejecuta la aptitud antes de hacer cambios

Puedes llamar a las aptitudes directamente desde Copilot CLI o pedirlo en lenguaje natural. Vamos a pedir a Copilot que ejecute las tres comprobaciones de la aptitud.

1. Vuelve a la conversación de filtrado en modo Interactive.
2. Usa este prompt:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Fíjate en el informe final.

## Personaliza el informe

Vamos a mejorar el informe para que indique qué se ejecutó, si se completó correctamente y qué resultados proporcionaron realmente las herramientas. Actualizarás la aptitud para que genere ese informe.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade esta sección al final del archivo:

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la aptitud actualizada

Ahora que has actualizado la aptitud, puedes probarla. Copilot CLI puede volver a cargar las aptitudes editadas sin reiniciar la conversación.

1. Escribe:

   ```plaintext
   /skills reload
   ```

2. Usa exactamente el mismo prompt que antes:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Fíjate en el informe final y compáralo con el primero.

## Resumen y siguientes pasos

Has personalizado y usado una aptitud de agente existente. En esta lección:

- exploraste la aptitud `quality-checks` para las pruebas unitarias, el lint y las comprobaciones de tipos.
- personalizaste el formato de sus resultados.
- volviste a cargar y ejecutaste la aptitud.

Ese cambio acompañará al filtrado en la PR de funcionalidad. A continuación, permitirás que Copilot interactúe directamente con el sitio mediante el [servidor Model Context Protocol (MCP) de Playwright][next-lesson].

## Más ejemplos de aptitudes

Estos ejemplos de la comunidad son referencias, no tareas adicionales:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y script de exportación integrado: `drawio`][drawio-example]
- [Pruebas del navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
