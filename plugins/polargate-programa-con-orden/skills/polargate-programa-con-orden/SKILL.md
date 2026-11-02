---
name: polargate-programa-con-orden
description: Hace que Claude programe con el orden de un buen equipo: aclara qué hay que hacer, lo parte en pasos pequeños, prueba cada paso, revisa antes de dar nada por hecho y publica sin sustos. Usar cuando alguien vaya a construir una función, arreglar un error, revisar código, escribir pruebas, mejorar la seguridad o la velocidad, preparar una publicación, o diga «hazlo bien», «sin romper nada» o «planifica esto antes».
---

# Programa con orden

Lee `REGLAS.md` antes de empezar. Después elige la guía que toque y léela entera: dentro está el proceso paso a paso. Las guías están en inglés, las escribió su autor así. Tú hablas siempre en el idioma de la persona.

## Qué guía toca

| Si la persona | Lee en `guias/` |
|---|---|
| No sabe aún qué quiere | `interview-me.md` |
| Tiene una idea verde y quiere darle vueltas | `idea-refine.md` |
| Empieza algo nuevo | `spec-driven-development.md` |
| Quiere fijar el nivel de calidad antes de empezar | `constraint-driven-development.md` |
| Ya sabe qué hacer y necesita los pasos | `planning-and-task-breakdown.md` |
| Va a escribir código | `incremental-implementation.md` |
| Toca pantallas | `frontend-ui-engineering.md` |
| Diseña cómo se hablan dos partes del programa | `api-and-interface-design.md` |
| Claude se pierde o le falta contexto | `context-engineering.md` |
| Usa una librería que cambia a menudo | `source-driven-development.md` |
| Toca algo delicado o que no conoce | `doubt-driven-development.md` |
| Escribe pruebas | `test-driven-development.md` |
| Prueba en el navegador | `browser-testing-with-devtools.md` |
| Tiene un error | `debugging-and-error-recovery.md` |
| Revisa código antes de darlo por bueno | `code-review-and-quality.md` |
| Quiere simplificar lo que ya funciona | `code-simplification.md` |
| Se preocupa por la seguridad | `security-and-hardening.md` |
| Se preocupa por la velocidad | `performance-optimization.md` |
| Quiere guardar los cambios con orden | `git-workflow-and-versioning.md` |
| Monta pruebas y publicación automáticas | `ci-cd-and-automation.md` |
| Quita o sustituye algo viejo | `deprecation-and-migration.md` |
| Escribe documentación | `documentation-and-adrs.md` |
| Quiere enterarse de qué pasa en producción | `observability-and-instrumentation.md` |
| Va a publicar | `shipping-and-launch.md` |

Cuando una guía nombra otra skill, es la guía de ese nombre en esta misma carpeta. Si cita órdenes con barra, como `/spec`, ignóralas: basta con leer la guía. En `referencias/` hay listas de comprobación de seguridad, velocidad, accesibilidad y pruebas.

## El orden de siempre

1. **Entender.** Qué hay que conseguir y cómo se sabrá que está bien.
2. **Planificar.** Pasos pequeños que se puedan comprobar uno a uno.
3. **Construir.** Un paso cada vez, sin dejar nada a medias.
4. **Comprobar.** Ejecutarlo de verdad. Si no lo has visto funcionar, no digas que funciona.
5. **Contar.** Qué ha cambiado, qué has probado y qué queda sin probar.

Adapta el esfuerzo al tamaño del encargo. Un cambio de una línea no necesita plan.

Basada en agent-skills, de Addy Osmani, con licencia MIT.
