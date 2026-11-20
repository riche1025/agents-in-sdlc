---
title: "Ejercicio 2 - Añade funcionalidad con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso un cambio sencillo puede afectar a varios archivos y requerir pruebas. El modo agente de Copilot puede explorar el proyecto, actualizar archivos, ejecutar tareas como las pruebas y corregir errores detectados. En este ejercicio lo usarás para añadir una funcionalidad.

> [!NOTE]
> Aunque los nombres se parecen, el modo agente y el agente en la nube ofrecen experiencias distintas. El modo agente trabaja en el entorno de desarrollo integrado (IDE) con ciclos rápidos de comentarios; el agente en la nube trabaja de forma asíncrona con incidencias y solicitudes de incorporación de cambios.

En este ejercicio:

- Copilot explorará el proyecto, identificará los archivos pertinentes y coordinará los cambios.
- Copilot implementará funcionalidades en la interfaz y la capa de datos.
- revisarás los cambios y las pruebas antes de combinarlos.

## Escenario

El catálogo de juegos crece y quieres permitir el filtrado por categoría y editorial. Ya añadiste el método auxiliar de editoriales en el ejercicio anterior; ahora completarás la capa de datos, la interfaz y las pruebas con el modo agente.

## Ejecuta el sitio de Tailspin Toys

Antes de cambiar el código, explora el sitio. Tailspin Toys es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Es una única aplicación Astro que genera páginas en lenguaje de marcado de hipertexto (HTML) estáticas. Las páginas consultan una base SQLite local con Drizzle, un mapeador objeto-relacional (ORM); no hay una interfaz de programación de aplicaciones (API) de backend independiente ni un marco de interfaz del lado del cliente. Los métodos auxiliares reutilizables están en `src/lib/`, y la interactividad se implementa con pequeños elementos `<script>` de Astro y las API del modelo de objetos del documento (DOM).

### Inicia el sitio

1. Vuelve a tu Codespace; deberías estar en `main`.
2. Abre un terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

5. Cuando el servidor Astro esté listo, comprueba el mensaje de que Tailspin Toys está listo y abre `http://localhost:4321` en el navegador. Si aparece un cuadro que te ofrece abrir esa dirección, ciérralo con **x**. En Codespaces, el enlace se reenvía a una dirección privada `https://<your-codespace-name>-4321.app.github.dev/`.

### Explora el sitio

La página principal muestra juegos con sus títulos, imágenes y descripciones. Al seleccionar un juego, se abre la página de detalles con el título, la descripción, la editorial y la categoría.

## Explora el backlog con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, abre Copilot Chat en el Codespace y selecciona **New Chat** para iniciar una conversación limpia. El modo y el modelo pueden variar según el ejercicio.

Pide a GitHub Copilot que muestre las incidencias creadas automáticamente a partir de la plantilla.

1. En el selector de agentes de Chat, selecciona **Agent**.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.
3. Envía este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para permitir que se enumeren las incidencias.
5. Revisa la lista generada.

> [!CAUTION]
> Los autores no expresan preferencia por un modelo concreto. Este taller se preparó con Claude Sonnet 4.5 para que las sugerencias fueran relativamente coherentes, pero los resultados pueden variar porque los modelos son probabilísticos.

> [!NOTE]
> Copilot puede utilizar un comando de Model Context Protocol (MCP) diferente y aun así completar la tarea.

## Revisa los archivos de instrucciones

Revisa las instrucciones de interfaz que guiarán los cambios del agente.

1. En el Codespace, abre `.github/instructions/ui.instructions.md`.
2. Revisa la arquitectura, los principios de diseño de componentes, las pruebas y la accesibilidad, y los enlaces a las instrucciones de Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y del proyecto. Las rutas son relativas al archivo que contiene el enlace.

## Implementa el filtrado

La funcionalidad necesita lógica de filtrado en `src/lib/`, pruebas y cambios en la página de listado de juegos. Antes de combinar los cambios, las pruebas deben superarse.

1. Continúa la conversación actual o selecciona **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Ejemplo de selección del archivo de instrucciones de interfaz](../../../_images/ex3-select-instructions-file.png)

3. Confirma que el agente **Agent** sigue seleccionado.

   ![Selector de agentes en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirma que sigue seleccionado el modelo **Claude Sonnet 4.5**.
5. Envía este prompt:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora y modifica los archivos de la capa de datos, la interfaz y las pruebas.

   ![Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Cuadro de Copilot Chat que solicita permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Revisa el código generado. Puede haber pausas o fallos de pruebas durante las iteraciones.

   ![Sesión completa de Copilot Chat en modo agente](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Vuelve al navegador, explora el filtrado y revisa los cambios. Cuando todo esté correcto, selecciona **Keep** en Copilot Chat.

> [!CAUTION]
> Revisa siempre el código generado por Copilot u otras herramientas de IA.

## Resumen y siguientes pasos

Has usado el modo agente para añadir funcionalidad al sitio de Tailspin Toys. En este ejercicio:

- observaste cómo Copilot exploró el proyecto, identificó los archivos pertinentes y coordinó los cambios.
- usaste Copilot para implementar funcionalidades en la interfaz y la capa de datos.
- revisaste los cambios y las pruebas generadas antes de conservarlos.

A continuación, [probarás la funcionalidad con Playwright MCP][next-lesson] y abrirás una solicitud de incorporación de cambios (PR).

### Ejercicio de exploración adicional: implementa la paginación

La lista de juegos puede necesitar paginación. Usa las instrucciones existentes y decide si el tamaño de página debe ser configurable o fijo. Proporciona a Copilot el contexto necesario e itera sobre sus propuestas.

## Recursos

- [Modos ask, edit y agent de Copilot: diferencias y usos][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
