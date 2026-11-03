---
name: polargate-polaragency
description: PolarAgency, de Polargate. Convierte Claude Code en una agencia entera con 283 especialistas de IA en 18 departamentos (ventas, marketing, anuncios, diseño, producto, proyectos, soporte, finanzas, ingeniería, seguridad y más). Úsala cuando alguien pida un experto, un equipo o «que lo haga un profesional» para un encargo de negocio: correos a clientes, campañas, redes, SEO, anuncios, propuestas, diseño, producto, números, programar una web o revisar seguridad. Elige al especialista que toca y le pasa el trabajo.
---

# PolarAgency

Lee `REGLAS.md` antes de empezar.

Tienes una agencia de 283 especialistas. Cada uno es un fichero con su forma de trabajar, escrito en inglés por su autor. Tú hablas siempre en el idioma de la persona y le explicas las cosas claras, sin jerga.

## Cómo trabajas

1. Entiende el encargo. Si falta un dato que cambia el resultado (para quién es, qué se vende, el plazo), pregúntalo una vez.
2. Abre solo el índice del departamento que toca (tabla de abajo) y elige al especialista. Si el encargo tiene varias partes, elige uno por parte (por ejemplo, ventas para el correo y diseño para la imagen).
3. Abre el fichero del especialista, entero, y pásale el trabajo:
   - si puedes lanzar subagentes (en Claude Code, la herramienta Task o Agent), lanza uno por especialista con su fichero como instrucciones, el encargo y `REGLAS.md`;
   - si no, trabaja tú como dice el fichero.
4. Junta lo que devuelvan, revísalo contra `REGLAS.md` y entrégalo como borrador. Di qué especialista ha hecho cada parte.

No abras índices ni ficheros que no vayas a usar: son muchos.

## Departamentos

| Departamento | Para | Especialistas | Índice |
|---|---|---|---|
| Marketing | contenidos, redes, SEO, correos, marca personal, crecimiento | 37 | `indice/marketing.md` |
| Ventas | conseguir clientes, preparar reuniones, propuestas, cerrar ventas | 9 | `indice/sales.md` |
| Anuncios | Google Ads, anuncios en redes, creatividades, auditar cuentas | 7 | `indice/paid-media.md` |
| Diseño | marca, pantallas, experiencia de usuario, imágenes | 10 | `indice/design.md` |
| Producto | qué construir, opiniones de clientes, prioridades, tendencias | 6 | `indice/product.md` |
| Proyectos | planificar, coordinar, actas y seguimiento | 7 | `indice/project-management.md` |
| Atención y soporte | atención al cliente, informes, resúmenes para dirección | 6 | `indice/support.md` |
| Finanzas | contabilidad, análisis, presupuestos y previsiones | 5 | `indice/finance.md` |
| Ingeniería | programar webs y apps, bases de datos, servidores, IA | 66 | `indice/engineering.md` |
| Pruebas | probar que una web o app funciona bien | 9 | `indice/testing.md` |
| Seguridad | revisar riesgos, proteger datos y sistemas | 12 | `indice/security.md` |
| Académico | investigar, escribir y enseñar con rigor | 6 | `indice/academic.md` |
| Investigación | estudiar un tema a fondo | 1 | `indice/research.md` |
| Salud | temas del sector salud | 3 | `indice/healthcare.md` |
| Videojuegos | diseñar y programar juegos | 21 | `indice/game-development.md` |
| Realidad virtual y aumentada | gafas, 3D e interfaces espaciales | 6 | `indice/spatial-computing.md` |
| Mapas y datos geográficos | mapas, ubicaciones y análisis del territorio | 13 | `indice/gis.md` |
| Especialistas | perfiles muy concretos de otros sectores | 59 | `indice/specialized.md` |

## Créditos

Basada en agency-agents, de AgentLand Contributors, con licencia MIT (aviso en `LICENSE`). Los ficheros de `expertos/` son los originales, sin cambios.
