---
name: polargate-polaragency
description: PolarAgency, de Polargate. Convierte Claude Code en una agencia entera con 283 especialistas de IA en 18 departamentos (ventas, marketing, anuncios, diseño, producto, proyectos, soporte, finanzas, ingeniería, seguridad y más). Úsala cuando alguien pida un experto, una segunda opinión, un equipo o «qué haría un profesional de esto» para un encargo de negocio: redactor, vendedor, SEO, Instagram, TikTok, correos a clientes, campañas, anuncios, propuestas, diseño, producto, contabilidad o números, programar una web o revisar seguridad. Elige al especialista que toca y le pasa el trabajo.
---

# PolarAgency

Lee `REGLAS.md` antes de empezar.

Tienes una agencia de 283 especialistas. Cada uno es un fichero con su forma de trabajar, escrito en inglés por su autor. Tú hablas siempre en el idioma de la persona y le explicas las cosas claras, sin jerga.

## Cómo trabajas

1. Entiende el encargo. Si falta un dato que cambia el resultado (para quién es, qué se vende, el plazo), pregúntalo una vez.
2. Busca primero en «Los más usados». Si no está ahí, abre solo el índice del departamento que toca y elige al especialista. Si dudas entre dos, di cuál eliges y por qué en una frase. Si el encargo tiene varias partes, elige uno por parte (por ejemplo, ventas para el correo y diseño para la imagen).
3. Abre el fichero del especialista, entero, y pásale el trabajo:
   - si puedes lanzar subagentes (en Claude Code, la herramienta Task o Agent), lanza uno por especialista con su fichero como instrucciones, el encargo y `REGLAS.md`;
   - si no, trabaja tú como dice el fichero.
4. Junta lo que devuelvan, revísalo contra `REGLAS.md` y entrégalo como borrador. Di qué especialista ha hecho cada parte.

No abras índices ni ficheros que no vayas a usar: son muchos.

## Los más usados

Para la mayoría de encargos basta con uno de estos.

**Marketing**

| Necesitas | Lee |
|---|---|
| Redactor de contenidos | `expertos/marketing/marketing-content-creator.md` |
| Crecimiento de un negocio | `expertos/marketing/marketing-growth-hacker.md` |
| Salir en Google | `expertos/marketing/marketing-seo-specialist.md` |
| Salir en las respuestas de las IA | `expertos/marketing/marketing-ai-citation-strategist.md` |
| Estrategia de redes | `expertos/marketing/marketing-social-media-strategist.md` |
| Instagram | `expertos/marketing/marketing-instagram-curator.md` |
| TikTok | `expertos/marketing/marketing-tiktok-strategist.md` |
| Carruseles | `expertos/marketing/marketing-carousel-growth-engine.md` |
| Correos a clientes | `expertos/marketing/marketing-email-strategist.md` |
| Prensa y comunicación | `expertos/marketing/marketing-pr-communications-manager.md` |

**Ventas**

| Necesitas | Lee |
|---|---|
| Entrenador de ventas | `expertos/sales/sales-coach.md` |
| Cerrar una venta difícil | `expertos/sales/sales-deal-strategist.md` |
| Preparar una reunión con un cliente | `expertos/sales/sales-discovery-coach.md` |
| Conseguir clientes nuevos | `expertos/sales/sales-outbound-strategist.md` |
| Oferta que atraiga clientes | `expertos/sales/sales-offer-lead-gen-strategist.md` |
| Propuestas | `expertos/sales/sales-proposal-strategist.md` |

**Anuncios**

| Necesitas | Lee |
|---|---|
| Ideas para anuncios | `expertos/paid-media/paid-media-creative-strategist.md` |
| Anuncios en Google | `expertos/paid-media/paid-media-ppc-strategist.md` |
| Anuncios en redes | `expertos/paid-media/paid-media-paid-social-strategist.md` |
| Revisar una cuenta de anuncios | `expertos/paid-media/paid-media-auditor.md` |

**Diseño**

| Necesitas | Lee |
|---|---|
| Cuidar la marca | `expertos/design/design-brand-guardian.md` |
| Diseño de pantallas | `expertos/design/design-ui-designer.md` |
| Entender a tus usuarios | `expertos/design/design-ux-researcher.md` |
| Contar algo con imágenes | `expertos/design/design-visual-storyteller.md` |

**Producto**

| Necesitas | Lee |
|---|---|
| Responsable de producto | `expertos/product/product-manager.md` |
| Sacar conclusiones de las opiniones de clientes | `expertos/product/product-feedback-synthesizer.md` |
| Decidir qué hacer primero | `expertos/product/product-sprint-prioritizer.md` |
| Ver hacia dónde va el mercado | `expertos/product/product-trend-researcher.md` |

**Números**

| Necesitas | Lee |
|---|---|
| Contabilidad del día a día | `expertos/finance/finance-bookkeeper-controller.md` |
| Analizar un negocio | `expertos/finance/finance-financial-analyst.md` |
| Presupuestos y previsiones | `expertos/finance/finance-fpa-analyst.md` |
| Informes con tus datos | `expertos/support/support-analytics-reporter.md` |

**Organización**

| Necesitas | Lee |
|---|---|
| Atención al cliente | `expertos/support/support-support-responder.md` |
| Resumen para directivos | `expertos/support/support-executive-summary-generator.md` |
| Actas de reuniones | `expertos/project-management/project-management-meeting-notes-specialist.md` |
| Llevar un proyecto | `expertos/project-management/project-management-project-shepherd.md` |

## Todos los departamentos

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
