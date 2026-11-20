---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios de VS Code, prepara el entorno. Crearás una copia propia del repositorio Tailspin Toys, iniciarás un [Codespace][codespaces] y confirmarás que GitHub Copilot Chat funciona en el editor.

## Configura el repositorio del taller

Crearás una instancia propia desde la [plantilla][template-repository], que contiene los archivos necesarios para el taller.

1. En una ventana nueva del navegador, abre la [plantilla de Tailspin Toys][tailspin-template].
2. Selecciona **Use this template** y, después, **Create a new repository**.

   ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si participas en un evento organizado por GitHub o Microsoft, sigue las instrucciones de los mentores. En caso contrario, crea el repositorio en una organización donde tengas acceso a GitHub Copilot.

   ![Configuración del repositorio de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio (**organization-or-user-name/repository-name**); la necesitarás más adelante.

> [!NOTE]
> **El backlog está preparado**
>
> Al crear el repositorio a partir de la plantilla, se crea automáticamente un backlog de incidencias de GitHub. Trabajarás con esas incidencias durante el taller; no tienes que crear otras.

## Crea un Codespace

GitHub Codespaces es un entorno de desarrollo en la nube con un entorno de desarrollo integrado (IDE) completo para escribir, ejecutar y depurar código desde el navegador, compatible con varios lenguajes de programación, extensiones y herramientas.

1. Abre el repositorio recién creado.
2. Selecciona el botón verde **Code**.

   ![Botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, **+** para crear un Codespace.

   ![Creación de un Codespace](../../../_images/ex0-create-codespace.png)

La creación puede tardar varios minutos. Mientras esperas, puedes explorar otras funciones de GitHub Copilot.

> [!CAUTION]
> Volverás al Codespace en un ejercicio posterior. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller funciona en Codespaces o en un [contenedor de desarrollo local][dev-containers]. Para trabajar localmente, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando aparezca el aviso; VS Code creará el mismo contenedor de desarrollo que Codespaces.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Usa GitHub Copilot Chat y el modo agente

Para usar el modo agente de GitHub Copilot Chat, necesitas la extensión GitHub Copilot Chat, que ya debería estar instalada en Codespaces.

> [!TIP]
> Si no tienes la extensión, [instálala desde Visual Studio Code Marketplace][copilot-chat-extension] o búscala en la vista Extensions de Visual Studio Code y selecciona **Install**.

Después de instalarla, puede que tengas que autenticarte con tu cuenta de GitHub.

1. Vuelve a tu Codespace.
2. Si Copilot Chat no aparece a la derecha del editor, selecciona el icono **Copilot Chat** en la parte superior del Codespace.
3. Escribe `Hello world` en la ventana de Copilot Chat y pulsa <kbd>Enter</kbd>.
4. Si se te solicita, sigue las instrucciones para iniciar sesión en GitHub.

   ![Ejemplo de un aviso de autenticación de Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Comprueba que se muestra la ventana de Copilot Chat.

## Resumen

Has creado una copia del repositorio y comenzado a preparar el Codespace que usarás para escribir código.

## Siguiente paso

A continuación, enseñarás a Copilot las convenciones del proyecto. Continúa con [el ejercicio 1: Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Guía de inicio rápido de Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
