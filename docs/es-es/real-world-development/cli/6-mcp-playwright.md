---
title: "Lección 6 - Valida la funcionalidad con Playwright MCP"
description: "Comprueba la configuración de Playwright MCP en Copilot CLI y úsala para explorar el filtrado en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Además de escribir código, hay que trabajar con datos, servicios externos y automatizaciones. Los servidores de Model Context Protocol (MCP) amplían la interfaz de línea de comandos (CLI) de Copilot con herramientas y servicios adicionales.

En esta lección:

- aprenderás qué es Model Context Protocol (MCP) y cómo lo usa Copilot CLI.
- añadirás el servidor Playwright MCP si aún no está disponible.
- pedirás al agente que controle un navegador para explorar el filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar cambios en la interfaz también hay que interactuar con ella. Usarás Playwright MCP para que Copilot explore el sitio como lo haría una persona y automatice parte de las comprobaciones.

## ¿Qué es Model Context Protocol?

[Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de inteligencia artificial (IA) se comuniquen con herramientas y servicios externos en tiempo real. Los agentes acceden a estas herramientas y recursos a través de servidores MCP, que actúan como puente. Cada servidor ofrece un conjunto distinto de herramientas y recursos.

Algunos servidores MCP conocidos:

- **[GitHub MCP Server][github-mcp]**: acceso a interfaces de programación de aplicaciones (API) para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: automatización de navegadores con Playwright.

GitHub mantiene un [registro MCP][mcp-registry] para facilitar la búsqueda y las contribuciones.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de usar uno, revisa su código fuente, comprueba quién lo publica y valora las implicaciones de seguridad.

## Añade el servidor Playwright MCP

Si Playwright MCP aún no está disponible, añádelo para que Copilot pueda interactuar con el sitio.

> [!NOTE]
> Si Copilot CLI ya tiene configurado Playwright MCP, omite estos pasos.

1. Vuelve a tu Codespace.
2. En Copilot CLI, escribe `/mcp add` para abrir el cuadro de diálogo para añadir un servidor MCP.
3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** con <kbd>Enter</kbd> y pulsa <kbd>Tab</kbd>.
5. Introduce este comando en el cuadro **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor.
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de diálogo MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Ya has comprobado manualmente el comportamiento. Ahora pide a Copilot que haga lo mismo con el servidor Playwright MCP.

1. Envía este mensaje:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> Normalmente Copilot identifica por sí mismo el servidor MCP que debe usar. Indicarlo puede orientar la tarea y hacer los resultados más coherentes.

2. Observa los pasos que Copilot ejecuta en el navegador.
3. Lee el informe y comprueba que todo funciona como esperabas.

Copilot iniciará el servidor, usará Playwright, detendrá el servidor y te entregará un informe.

## Resumen y siguientes pasos

Has usado Playwright MCP para explorar la funcionalidad en un navegador real. En esta lección:

- aprendiste qué es MCP y cómo lo usa Copilot CLI.
- añadiste Playwright MCP si aún no estaba disponible.
- pediste al agente que controlara un navegador para explorar el filtrado.

A continuación, [crearás un agente personalizado de QA][next-lesson] que combine la aptitud y las herramientas del navegador.

## Recursos

- [Qué es MCP y por qué se habla tanto de ello][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
