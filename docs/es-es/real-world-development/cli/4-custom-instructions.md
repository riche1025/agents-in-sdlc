---
title: "Lección 4 - Guía a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es fundamental al trabajar con inteligencia artificial (IA) generativa. Los archivos de instrucciones explican a Copilot no solo qué código quieres, sino también cómo debe estructurarse. Ahora que ya has creado el filtrado, explorarás las instrucciones que usó, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- explorarás cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- actualizarás las instrucciones para establecer estándares de código.
- observarás su efecto en el código generado.

## Escenario

Tailspin Toys tiene pautas de desarrollo:

- Los comentarios deben explicar la intención y las decisiones que no sean evidentes, no repetir el código.
- Las funciones exportadas en `db/` y `src/lib/` deben documentar su propósito, parámetros y valores devueltos con comentarios de documentación de TypeScript (TSDoc) o JavaScript (JSDoc), incluido el argumento `db` inyectable cuando exista.
- Los componentes reutilizables de Astro deben documentar sus contratos `Props`, y los comentarios deben mantenerse actualizados al cambiar el código relacionado.
- Deben conservarse las pautas de formato y lint existentes.

Las instrucciones ayudarán a Copilot a seguir estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas aportan contexto sobre preferencias, convenciones de código, bibliotecas y comentarios. Se pueden definir para todo el repositorio o para tipos concretos de archivos y tareas:

- `.github/copilot-instructions.md` se envía a Copilot en todas las solicitudes del repositorio.
- `.github/instructions/*.instructions.md` contiene pautas para determinados lenguajes, tipos de archivo o tareas.

> [!NOTE]
> Otros formatos de instrucciones y su compatibilidad dependen del entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de depender de un formato concreto.

### Explora los archivos de instrucciones

El proyecto de ejemplo ya incluye varios archivos. Revísalos antes de modificarlos.

1. Vuelve a tu Codespace.
2. En el editor de Codespaces, abre `.github/copilot-instructions.md` y revisa la descripción del proyecto y sus pautas.
3. Explora los archivos de `.github/instructions`, incluidos los de Astro, la capa de datos Drizzle y las pruebas.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa que `applyTo` define los archivos a los que se aplica.
5. Abre `.github/instructions/drizzle.instructions.md` y revisa los enlaces a otras instrucciones y a archivos de ejemplo.

> [!NOTE]
> Otros formatos y su compatibilidad dependen del entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support].

## Actualiza las instrucciones del proyecto

Añadirás un estándar para los comentarios TSDoc en el archivo principal de instrucciones.

1. En `.github/copilot-instructions.md`, localiza la sección **Code formatting guidance**, aproximadamente en la línea 35.
2. Añade este elemento al final de la sección:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

3. Guarda el archivo.

## Aplica las instrucciones actualizadas

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Cierra y reanuda la conversación de filtrado para que las instrucciones nuevas se apliquen sin perder el contexto.

1. Si la conversación de filtrado sigue abierta, escribe `/exit`.
2. Desde la raíz del repositorio en la rama `game-filters-cli`, reanuda la conversación:

   ```bash
   copilot --resume
   ```

3. Si se te solicita, selecciona la conversación de filtrado y confirma que está activa la rama `game-filters-cli`.
4. Pide a Copilot que aplique las pautas:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

5. Escribe `/diff` y revisa los archivos TypeScript modificados. Comprueba que los comentarios TSDoc nuevos describan el código correctamente.

## Resumen y siguientes pasos

Has explorado cómo Copilot obtiene el contexto de los archivos de instrucciones y has aplicado un estándar nuevo a la funcionalidad. En esta lección:

- exploraste cómo llegan al agente las instrucciones del repositorio y las instrucciones específicas de rutas.
- actualizaste las instrucciones para establecer estándares de código.
- observaste su efecto en el código generado.

A continuación, [personalizarás y ejecutarás la aptitud reutilizable `quality-checks`][next-lesson] para ejecutar las pruebas y el análisis de forma coherente.

## Recursos

- [Añadir instrucciones personalizadas a Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: recursos e instrucciones][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
