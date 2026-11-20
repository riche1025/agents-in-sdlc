---
title: "Lección 12 - Publicar el sitio con GitHub Pages"
description: "Configura con la aplicación GitHub Copilot un flujo de trabajo de Pages, revisa su solicitud de incorporación de cambios y comprueba el cuestionario espacial publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Publica el cuestionario espacial en GitHub Pages para que cualquiera pueda probarlo. Copilot puede preparar el flujo de trabajo y guiar la publicación, pero debes revisar los cambios y confirmar que el sitio está disponible en una dirección web (URL) pública.

En esta lección:

- pedirás a Copilot que configure una publicación en GitHub Pages.
- revisarás el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarla.
- seguirás la publicación y comprobarás el sitio.

## Escenario

El cuestionario espacial ya está en un repositorio de GitHub, pero hace falta una forma sencilla de probarlo. GitHub Pages publica el sitio de un solo archivo en una URL pública sin añadir un servidor ni dependencias de ejecución.

## Pide a Copilot que prepare la publicación

> [!WARNING]
> Crear una solicitud de incorporación de cambios puede confirmar y enviar código. Revisa la configuración de aprobación y el repositorio de destino antes de enviar este mensaje. Si está activada la opción **Approve all**, no esperes una confirmación aparte.

En la sesión de la aplicación Copilot para `space-quiz`, envía este mensaje:

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## Revisa el flujo de trabajo y la solicitud de incorporación de cambios

1. Confirma que el archivo README solo se añade si el repositorio aún no tiene uno.
2. Revisa los cambios de la solicitud de incorporación de cambios (PR), incluidos los pasos de compilación y publicación del flujo, sus desencadenadores y permisos.
3. Confirma que el flujo publica desde la rama predeterminada, no desde una solicitud de incorporación de cambios aún sin combinar.
4. Pide las correcciones necesarias y revisa el diff actualizado. Espera a que se superen las comprobaciones obligatorias antes de autorizar la combinación.

## Autoriza la combinación y la publicación

> [!WARNING]
> El mensaje siguiente autoriza al agente a combinar la solicitud revisada, cambiar la configuración de Pages del repositorio y publicar el sitio. Envíalo solo después de revisar los cambios y confirmar el repositorio y la solicitud. La configuración de aprobación podría permitir estas acciones sin otra confirmación.

Sustituye `<PR_NUMBER>` por el número de la solicitud revisada y envía este mensaje por separado:

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![Diagrama en tres etapas: una solicitud de incorporación de cambios de space-quiz combinada; una ejecución correcta de Deploy website en GitHub Actions con los pasos Build website, Upload artifact y Deploy to Pages; y el cuestionario espacial publicado en yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Comprueba la publicación

1. Sigue la ejecución de publicación de GitHub Actions hasta que termine correctamente.
2. Abre la URL indicada y confirma que se carga el cuestionario espacial.

Si el agente no puede habilitar Pages o combinar la solicitud, sigue las instrucciones concretas que te proporcione. No des la tarea por terminada hasta que la publicación se complete y el sitio esté disponible.

## Resumen y siguientes pasos

El cuestionario espacial ya está publicado y has comprobado el sitio en lugar de confiar solo en el informe del agente. En esta lección:

- pediste a Copilot que configurara la publicación en GitHub Pages.
- revisaste el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarla.
- seguiste la publicación y comprobaste el sitio.

Continúa con [la lección 13: Revisión y siguientes pasos][next-lesson].

[next-lesson]: ../13-review/
