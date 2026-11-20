---
title: "Ejercicio 3 - Prueba la funcionalidad con el servidor Playwright MCP"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Ya has creado el filtrado con el modo agente. Antes de abrir una solicitud de incorporación de cambios (PR), comprobarás que funciona en el navegador. Conectarás el servidor Playwright de Model Context Protocol (MCP) para que Copilot controle un navegador real, pruebe la funcionalidad y, después, publique la rama y abra la PR.

En este ejercicio:

- aprenderás qué es Model Context Protocol (MCP) y cómo amplía Copilot con herramientas.
- añadirás Playwright MCP al espacio de trabajo.
- pedirás a Copilot que pruebe manualmente el filtrado en un navegador.
- publicarás la rama y abrirás una PR.

## ¿Qué es Model Context Protocol?

Model Context Protocol (MCP) proporciona a Copilot una forma estándar de comunicarse con herramientas y servicios externos. Los servidores MCP proporcionan acceso a recursos y permiten realizar acciones.

![Diagrama del modo agente y su interacción con el contexto, el modelo de lenguaje y las herramientas, incluidas las herramientas de servidores MCP y extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

Algunos servidores MCP conocidos:

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)** permite gestionar repositorios, incidencias y solicitudes de incorporación de cambios mediante interfaces de programación de aplicaciones (API).
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)** permite automatizar un navegador, navegar por páginas, rellenar formularios y seleccionar botones.

GitHub aloja un [registro MCP](https://github.com/mcp) para facilitar la búsqueda de servidores y las contribuciones.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Revisa el código fuente, comprueba quién lo publica y valora las implicaciones de seguridad. Usa solo servidores de confianza y ten cuidado al conceder acceso a recursos u operaciones sensibles.

## Revisa la configuración MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en el espacio de trabajo de VS Code. El proyecto ya contiene el servidor remoto `github`:

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

Esta entrada permite a Copilot consultar el backlog. VS Code se conecta al servidor GitHub MCP remoto mediante el protocolo de transferencia de hipertexto (HTTP) y te pide autenticarte la primera vez que se usa una herramienta.

## Añade Playwright MCP

Playwright MCP proporciona a Copilot un navegador controlable para probar la funcionalidad.

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

`playwright` es un servidor local que VS Code inicia con `npx @playwright/mcp@latest`. La opción `--headless` ejecuta el navegador sin ventana visible, necesaria en Codespaces, que no dispone de escritorio.

> [!NOTE]
> Tailspin Toys ya utiliza Playwright para las pruebas de extremo a extremo, por lo que normalmente el navegador ya está instalado. Si Copilot informa de que falta, pídele que ejecute `npx playwright install chromium`.

## Inicia y autoriza el servidor

VS Code inicia los servidores MCP cuando se necesitan y pide confirmación de confianza.

1. En `.vscode/mcp.json`, selecciona **Start** sobre la entrada `playwright` para comprobar la configuración.
2. Si VS Code pregunta si confías en el servidor, revisa la configuración y autorízala.

Iniciarlo manualmente es opcional; si no lo haces, VS Code lo iniciará y solicitará autorización cuando Copilot necesite sus herramientas.

## Prueba el filtrado

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe la funcionalidad. Playwright MCP se basa en el árbol de accesibilidad de la página, no en capturas de pantalla; así, el agente trabaja con elementos etiquetados como botones, enlaces y listas.

1. Envía este prompt:

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

2. Compara el informe con los criterios de aceptación de la incidencia. Si algo no funciona, pide aclaraciones o correcciones antes de abrir la PR.

> [!NOTE]
> La aplicación debe estar en ejecución en `http://localhost:4321`. Si detuviste el servidor de desarrollo, vuelve a iniciarlo. La primera vez que se usa Playwright MCP puede ser necesario descargar un navegador; si falta, ejecuta `npx playwright install chromium`.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publica la rama y crea una PR

Después de confirmar que la funcionalidad funciona, publica la rama `filtering-vscode`.

1. En el panel **Source Control** del Codespace, revisa los cambios de Copilot.
2. Selecciona el icono **+** para preparar los cambios.
3. Usa el botón **Sparkle** para generar un mensaje de confirmación.
4. Selecciona **Publish** para enviar la rama.

![Panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

## Crea la solicitud de incorporación de cambios

Copilot puede localizar la incidencia asociada y crear la PR.

1. En Copilot Chat, selecciona **New Chat** y confirma que **Agent** está seleccionado.
2. Envía este prompt:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

3. Cuando corresponda, selecciona **Continue** para autorizar las operaciones necesarias. La primera vez que se utilice una herramienta de GitHub, puede que tengas que autenticarte.
4. Abre el enlace de Copilot y revisa la PR; **no la combines todavía**.

## Resumen y siguientes pasos

En este ejercicio:

- aprendiste qué es MCP y cómo amplía Copilot con herramientas.
- añadiste Playwright MCP al espacio de trabajo.
- lo usaste para probar el filtrado en un navegador antes de publicarlo.
- publicaste la rama y abriste una PR.

MCP es una forma de ampliar Copilot. A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas concretas, como las revisiones de accesibilidad.

## Recursos

- [Qué es MCP y por qué se habla tanto de ello][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [Registro MCP de GitHub][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
