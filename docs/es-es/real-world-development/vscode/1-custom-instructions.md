---
title: "Ejercicio 1 - Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo agente →][next-lesson]

El contexto es clave al trabajar con inteligencia artificial (IA) generativa. Los archivos de instrucciones permiten proporcionar a Copilot el contexto necesario sobre cómo generar código. En este ejercicio explorarás las instrucciones del repositorio, generarás un primer método auxiliar para editoriales con las pautas actuales, añadirás un estándar general y repetirás el prompt para observar el efecto.

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto, las pautas de código y los estándares de documentación.
- generarás un método auxiliar de editoriales con las instrucciones actuales.
- añadirás un estándar general a `.github/copilot-instructions.md` y repetirás el prompt.
- confirmarás los cambios en `main` para que Copilot use las nuevas pautas en el ejercicio siguiente.

> [!CAUTION]
> El código generado puede no seguir todos los estándares: Copilot no es determinista. El objetivo es observar la tendencia tras actualizar las instrucciones, no obtener siempre el mismo resultado.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene estándares para el desarrollo: la capa de datos necesita pruebas unitarias, la interfaz debe tener un modo oscuro y un aspecto moderno, el código debe incluir comentarios de documentación de TypeScript (TSDoc) y cada archivo debe empezar con un bloque de comentarios que explique su función.

### Instrucciones personalizadas

Las instrucciones proporcionan a Copilot contexto sobre preferencias, convenciones, bibliotecas y comentarios. Se pueden definir para todo el repositorio o para tareas y tipos de archivo concretos:

- `.github/copilot-instructions.md` se aplica a todas las solicitudes del repositorio.
- `.github/instructions/*.instructions.md` contiene pautas para tareas o tipos de archivo concretos.

Copilot Chat, la interfaz de línea de comandos (CLI) de Copilot y Copilot cloud agent utilizan ambos tipos. Copilot también admite formatos como `AGENTS.md` y `CLAUDE.md`; consulta la [referencia de compatibilidad][custom-instructions-support].

> [!NOTE]
> En el IDE, los archivos de instrucciones se utilizan para generar código en Copilot Chat, pero no para completar código ni para sugerir la siguiente edición.

Mantén el archivo principal enfocado en el contexto del proyecto y los estándares globales. Usa los archivos específicos para lenguajes, pruebas, componentes y tareas. Escribe instrucciones claras en lenguaje natural y añade ejemplos cuando ayuden. El proyecto incluye instrucciones para [cambios de interfaz][ui-instructions] y [Astro][astro-instructions]. Para explorar recursos, consulta [awesome-copilot][awesome-copilot].

> [!TIP]
> Todos los proyectos que usan GitHub Copilot deberían tener una colección sólida de archivos de instrucciones. Copilot también puede generarlos: en VS Code, por ejemplo, puedes usar **Configure Chat → Generate Agent Instructions**; en Copilot CLI, `/init`. Cada ejercicio indica la opción pertinente para ese entorno.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

### Explora los archivos de instrucciones del proyecto

1. Abre `.github/copilot-instructions.md`.
2. Revisa la descripción y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**, incluida la guía de flujos de GitHub Actions dentro de **Code standards**.
3. Explora `.github/instructions`, donde hay instrucciones para Astro, Drizzle, pruebas y otras tareas.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa que `applyTo` define un patrón relativo a la raíz del repositorio, como `**/*.test.ts`.
5. Revisa las pautas específicas para las pruebas unitarias.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otras instrucciones y a ejemplos. Las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> **Code formatting requirements** documenta las convenciones del proyecto, pero aún no exige documentación dentro del código. Añadirás comentarios TSDoc y encabezados de archivo.

## Crea una rama

Prepara una rama para los cambios.

1. Vuelve al Codespace del ejercicio anterior.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea y activa una rama:

   ```bash
   git checkout -b custom-instructions
   ```

## Usa Copilot Chat antes de actualizar las instrucciones

Primero usarás las instrucciones actuales para observar el resultado inicial.

1. Vuelve al Codespace, abre Copilot Chat y selecciona **New Chat**.
2. Cierra las pestañas de editor anteriores y abre `src/lib/publishers.ts` para dar contexto a Copilot.
3. En el selector de agentes de Chat, selecciona **Agent**.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Revisa los cambios propuestos. El método auxiliar suele ser una función tipada con un cliente `db` como primer argumento y una matriz tipada de editoriales como resultado; esto sigue las convenciones de `.github/instructions/drizzle.instructions.md`, aplicable a `src/lib/*.ts`.
6. Observa si faltan los comentarios TSDoc y el encabezado del archivo. Debido a la naturaleza probabilística de Copilot, puede que los añada incluso antes de actualizar las instrucciones.

## Añade un estándar del repositorio

Añadirás reglas generales para mejorar las sugerencias de código.

1. Abre de nuevo `.github/copilot-instructions.md`.
2. Localiza **Code formatting requirements**, cerca de la línea 27.
3. Añade debajo de las normas existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

## Repite el prompt y observa el cambio

Copilot debe recibir contexto nuevo para repetir la operación.

1. En Copilot Chat, selecciona **New Chat**.
2. Vuelve a abrir `src/lib/publishers.ts`.
3. Envía exactamente el mismo prompt:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Comprueba que el archivo propuesto empiece con un comentario sobre su función y que la función incluya un comentario TSDoc con su propósito, el parámetro `db` y el valor devuelto.

   ```typescript
   /**
    * Métodos auxiliares de acceso a los datos de editoriales de la plataforma de financiación colectiva de Tailspin Toys.
    * Proporciona funciones para recuperar información de editoriales de la base de datos.
    */
   ```

   El comentario de la función puede tener esta forma:

   ```typescript
   /**
    * Devuelve una lista de todas las editoriales con sus identificadores y nombres.
    *
    * @param db - Cliente de base de datos Drizzle.
    * @returns Una promesa que se resuelve en una matriz de objetos de editorial.
    */
   ```

Copilot ya sigue el nuevo estándar en código real que utilizarás en el ejercicio siguiente.

## Confirma las instrucciones y envía la rama

Confirma que los cambios están presentes y envía la rama.

1. Abre un terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
2. Ejecuta `git status` y comprueba que aparecen las instrucciones y el método auxiliar.
3. Añade los archivos y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Si git status muestra cambios de apoyo (por ejemplo, pruebas), añade también esos archivos.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envía la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Crearás una PR vinculada a la incidencia del backlog sobre la actualización de las instrucciones.

1. Abre Copilot Chat en el Codespace, pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) y confirma que está seleccionado **Agent**.
2. Pide a Copilot que encuentre la incidencia relacionada y cree una PR desde la rama actual, indicando que incluye las instrucciones y la base del método auxiliar de editoriales:

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

3. Revisa cada solicitud de permiso de GitHub y selecciona **Allow** cuando corresponda.
4. Cuando se cree la PR, pide a Copilot que la combine en `main` y actualice la rama local:

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

5. Revisa los comandos y acciones de GitHub antes de seleccionar **Allow**.

## Resumen y siguientes pasos

Has explorado cómo Copilot utiliza las instrucciones del proyecto y has usado Copilot Chat en VS Code para:

- enviar un prompt de generación de código y observar el resultado con las instrucciones iniciales.
- añadir un estándar general a `.github/copilot-instructions.md`.
- repetir el prompt y observar cómo el código propuesto aplica el nuevo estándar.
- confirmar las instrucciones y la base del método auxiliar en `main`.

A continuación, aplicarás esas instrucciones en [modo agente][next-lesson] para añadir una funcionalidad.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para mejorar las instrucciones de Copilot][copilot-instructions-five-tips]
- [Instrucciones personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: recursos e instrucciones][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
