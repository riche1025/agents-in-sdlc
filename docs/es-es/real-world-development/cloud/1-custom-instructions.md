---
title: "Ejercicio 1 - Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental al trabajar con inteligencia artificial (IA) generativa. Los archivos de instrucciones permiten proporcionar pautas para que Copilot entienda no solo qué debe hacer, sino también cómo. En este ejercicio explorarás cómo llegan a Copilot el contexto del proyecto, las pautas de código y los estándares de documentación mediante las instrucciones del repositorio y las instrucciones específicas de rutas.

En este ejercicio:

- explorarás cómo las instrucciones personalizadas proporcionan contexto al agente.
- añadirás un estándar general al archivo `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los itinerarios de VS Code y de la interfaz de línea de comandos (CLI), aquí no compararás prompts antes y después. Copilot cloud agent trabaja de forma asíncrona con incidencias de GitHub, por lo que la diferencia no se ve en tiempo real. Observarás el efecto más adelante al revisar las solicitudes de incorporación de cambios (PR).

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene pautas de desarrollo: las pruebas unitarias deben cubrir siempre la capa de datos; la interfaz debe tener un modo oscuro y un aspecto moderno; el código debe incluir comentarios de documentación de TypeScript (TSDoc); y cada archivo debe empezar con un bloque de comentarios que describa su función.

### Instrucciones personalizadas

Las instrucciones permiten compartir contexto, preferencias de código, convenciones y pautas de comentarios. Se pueden definir para todo el repositorio o para tareas y tipos de archivo concretos:

- `.github/copilot-instructions.md` se aplica a todas las solicitudes del repositorio y debe contener contexto general, como la pila tecnológica, el proyecto y las prácticas globales.
- `.github/instructions/*.instructions.md` contiene instrucciones para tareas o tipos de archivo, como TypeScript, Astro, componentes de interfaz o pruebas.

En el entorno de desarrollo integrado (IDE), los archivos de instrucciones se utilizan para generar código en Copilot Chat, pero no para completar código ni para sugerir la siguiente edición. Copilot Chat, Copilot CLI y Copilot cloud agent utilizan las instrucciones del repositorio y los archivos `*.instructions.md` con frontmatter `applyTo`. Copilot también admite formatos como `AGENTS.md` y `CLAUDE.md`; consulta la [referencia de compatibilidad][custom-instructions-support].

Mantén el archivo principal enfocado en el contexto del proyecto, su estructura y los estándares globales. Usa `*.instructions.md` para pautas de tipos de archivo, como pruebas unitarias, componentes Astro y la capa de datos, o para tareas concretas. Escribe instrucciones claras en lenguaje natural y añade ejemplos de código correcto e incorrecto cuando ayuden. No hay una única forma de crear instrucciones: prueba distintas opciones para descubrir qué funciona en el proyecto.

> [!TIP]
> Todo proyecto que utilice GitHub Copilot debería tener una colección sólida de archivos de instrucciones. Copilot puede ayudar a generarlos: en VS Code, por ejemplo, puedes usar **Configure Chat → Generate Agent Instructions**; en Copilot CLI, `/init`. El ejercicio correspondiente describe las opciones de cada entorno. Para consultar plantillas, explora [awesome-copilot][awesome-copilot].

El proyecto también incluye pautas para [cambios de interfaz][ui-instructions] y [Astro][astro-instructions].

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

### Explora los archivos de instrucciones

Revisa los archivos que incluye el repositorio desde el editor o la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Explora la descripción del proyecto y las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, revisa también las pautas anidadas para los flujos de GitHub Actions.
3. Explora `.github/instructions`, donde hay pautas para Astro, la capa de datos Drizzle, pruebas y más.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa que el campo `applyTo` define un patrón relativo a la raíz del repositorio. Por ejemplo, coincide con archivos de prueba TypeScript como `**/*.test.ts`.
5. Revisa las pautas para crear pruebas unitarias.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otras instrucciones y a ejemplos existentes. Las rutas son relativas al archivo de instrucciones.

> [!NOTE]
> La sección **Code formatting requirements** aún no exige documentación dentro del código. Añadirás reglas para comentarios TSDoc y encabezados de archivo.

## Añade un estándar del repositorio

Añadirás reglas globales de comentarios para que el agente las aplique a las incidencias posteriores.

1. Desde el terminal del Codespace, crea una rama:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Vuelve a abrir `.github/copilot-instructions.md`.
3. Localiza **Code formatting requirements**, cerca de la línea 27.
4. Añade estas líneas Markdown después de las pautas existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. Guarda el archivo.

> [!TIP]
> Las instrucciones del repositorio son adecuadas para estándares generales; los archivos `*.instructions.md` sirven para lenguajes, tipos de archivo y tareas concretas.

## Confirma, envía y combina la actualización

El agente en la nube lee las instrucciones de la rama a la que se dirige la incidencia. Para que las use en el siguiente ejercicio, los cambios deben llegar a `main`.

1. Añade y confirma el archivo:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una PR desde `custom-instructions-cloud` a `main` y combínala. Si prefieres trabajar directamente en `main` durante el taller, puedes omitir la rama y confirmar allí los cambios.

## Resumen y siguientes pasos

Has explorado cómo Copilot utiliza los archivos de instrucciones y has añadido un estándar general a `.github/copilot-instructions.md`. En este ejercicio:

- exploraste cómo las instrucciones personalizadas proporcionan contexto al agente.
- añadiste un estándar general al archivo `.github/copilot-instructions.md`.

Verás el efecto en las PR que cree el agente.

A continuación, [asignarás tu primera incidencia a Copilot cloud agent][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para mejorar las instrucciones personalizadas][copilot-instructions-five-tips]
- [Awesome Copilot: recursos e instrucciones][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
