---
title: "Lección 8 - Crea y combina la PR de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la aptitud, el perfil de QA y las pruebas; después crea una PR y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las instrucciones actualizadas, la aptitud, el perfil de aseguramiento de la calidad (QA) y las pruebas están en una misma rama. Ahora revisarás los cambios y abrirás una solicitud de incorporación de cambios (PR). La PR de las valoraciones con estrellas la combinaste manualmente; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> En condiciones normales, separarías la funcionalidad, las instrucciones, la aptitud y el agente de QA en varias PR. Para simplificar el taller, todo el flujo de filtrado y calidad se mantiene en una conversación y una rama.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de una PR.
- inspeccionarás los cambios completos y las evidencias de verificación.
- crearás la PR del filtrado.
- activarás Agent Merge solo después de revisar los cambios y confirmarás que se han combinado.

## Escenario

Has planificado, implementado y verificado una funcionalidad con Copilot. Tailspin Toys quiere automatizar el trabajo restante de la PR sin quitar al desarrollador el control de autorización de la combinación.

## Agent Merge

**Agent Merge** automatiza el trabajo restante para incorporar una PR. Cuando se activa, Copilot resuelve los bloqueos, como comprobaciones de integración continua (CI) fallidas, comentarios de revisión y necesidad de volver a basar la rama. Después activa la combinación automática de GitHub cuando la configuración del repositorio lo permite.

Antes seleccionabas **Merge pull request** manualmente. Revisa el trabajo y decide si está listo antes de activar Agent Merge.

## Usa Agent Merge para gestionar la PR

Revisa los cambios, crea la PR y permite que Agent Merge gestione el resto.

1. Vuelve a tu Codespace.
2. Escribe `/agent` para abrir el cuadro de diálogo del agente.
3. Selecciona **Default** y pulsa <kbd>Enter</kbd>.
4. Crea una PR con `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará la CI de la PR y la combinará cuando todo se supere.
7. Confirma que Copilot indique algo similar a `PR #14 was squash-merged successfully.`

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, lee el motivo y, cuando el repositorio lo permita, realiza manualmente la combinación revisada.

## Resumen y siguientes pasos

Has automatizado partes del desarrollo, desde la generación y validación del código hasta el proceso de la PR. En esta lección:

- aprendiste qué es Agent Merge y cómo automatiza el ciclo de una PR.
- inspeccionaste los cambios completos y las evidencias de verificación.
- creaste la PR del filtrado.
- activaste Agent Merge después de la revisión y confirmaste que se combinó la PR.

A continuación, [explorarás más comandos de barra de Copilot CLI][next-lesson] para gestionar el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
