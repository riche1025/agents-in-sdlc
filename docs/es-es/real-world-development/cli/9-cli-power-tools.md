---
title: "Lección 9 - Comandos de barra de GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, elegir modelos, compartir sesiones y delegar tareas opcionalmente al agente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La interfaz de línea de comandos (CLI) de GitHub Copilot incluye comandos de barra para acceder a funciones avanzadas e información de configuración. Ya has usado `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora probarás otros comandos útiles.

En esta lección:

- usarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto.
- usarás `/model` para explorar los modelos disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar árboles de trabajo y delegar tareas al agente en la nube.

## Escenario

Ya has terminado el flujo principal de CLI. Ahora explorarás la gestión del contexto, el cambio de modelos, el uso compartido de sesiones y la delegación opcional a [Copilot cloud agent][about-cloud-agent].

## Explora el contexto de Copilot CLI

En tareas grandes o complejas puedes acercarte al límite de contexto del modelo. Copilot CLI lo compacta automáticamente cuando hace falta, y también puedes inspeccionarlo o compactarlo con comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y la distribución del contexto entre instrucciones del sistema, herramientas, mensajes y espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a ejecutar `/context` y compara el resultado. Si la conversación ya es corta, puede que apenas cambie.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto cuando se llena. Usa `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` para empezar una tarea distinta con una conversación nueva.

## Elige el modelo

Los modelos tienen distintas capacidades y preferencias. Copilot CLI permite mostrar y seleccionar los modelos disponibles.

1. Escribe `/model`.
2. Explora los modelos y la información de uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

El comando `/share` puede exportar una sesión a un archivo Markdown o en lenguaje de marcado de hipertexto (HTML), crear un enlace para compartir o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` de tu versión.
2. Si quieres compartir la sesión, elige el destino adecuado; por ejemplo, `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo o publicarlo. Las exportaciones pueden incluir mensajes, respuestas y detalles del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de una conversación que el equipo no tenga previsto compartir.

## Opcional: amplía el trabajo o delégalo

El flujo principal del taller ha terminado. Copilot CLI también ofrece comandos para tareas mayores:

- `/fleet` divide tareas independientes entre subagentes y las ejecuta en paralelo.
- `/worktree` crea un árbol de trabajo de Git aislado para otra tarea.
- `/delegate` envía una tarea a Copilot cloud agent, que trabaja de forma asíncrona y puede abrir una PR.

Estos comandos son opcionales: pueden crear árboles de trabajo adicionales o trabajo remoto. Empieza con una tarea nueva y acotada, y revisa el resultado con el flujo habitual. Para obtener más información sobre el trabajo asíncrono, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y siguientes pasos

Has usado comandos de barra para configurar Copilot CLI, compartir sesiones y consultar información interna. En esta lección:

- usaste `/context` y `/compact` para explorar la gestión del contexto.
- usaste `/model` para explorar los modelos disponibles.
- aprendiste cómo `/share` puede exportar o compartir una sesión.
- exploraste comandos opcionales para tareas en paralelo, árboles de trabajo y delegación al agente en la nube.

Hay más comandos que explorar. Para cerrar el recorrido, [repasarás lo aprendido y los siguientes pasos][next-lesson].

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca de Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
