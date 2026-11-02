---
name: polargate-usa-ia-gratis
description: Busca dónde usar modelos de IA sin pagar, con sus límites y lo que hacen con tus datos, y ayuda a montarlo. Trae 15 servicios con plan gratis, como Google Gemini, Groq, Mistral, Cloudflare u OpenRouter. Usar cuando alguien quiera probar una idea con IA sin gastar, abaratar una tarea, elegir un modelo gratis o pregunte «¿hay alguna IA gratis para esto?».
---

# Usa IA gratis

Lee `REGLAS.md` antes de empezar.

La lista está en `proveedores.json`: cada servicio con su web, sus modelos, sus límites y sus notas. El campo `lastUpdated` dice cuándo se revisó y `footnotes` trae la letra pequeña.

## Cómo se hace

1. **Pregunta para qué es,** si no lo ha dicho: qué tarea, cuántas veces al día y si lleva datos privados.
2. **Elige dos opciones como mucho.** Mira límites, idioma y qué hace cada servicio con lo que le envías. Explica la elección con una frase.
3. **Comprueba que sigue igual.** Estos planes cambian sin avisar. Abre la web del servicio y mira que el plan y el modelo siguen ahí. Si la lista tiene más de un mes, dilo.
4. **Ayúdale a montarlo.** Dile dónde se crea la cuenta y la clave de acceso. La cuenta la crea la persona. Prueba una llamada corta antes de construir nada encima.
5. **Guarda la clave bien.** En un fichero `.env` que no se suba a ningún sitio, nunca dentro del código.

## Cómo se lee la lista

- `RPM` son peticiones por minuto, `RPD` por día, `TPD` palabras aproximadas (tókenes) por día.
- `context` es cuánto texto admite de una vez.
- `country` es el país del servicio. `CN` es China.

Basada en awesome-free-llm-apis, de mnfst, con licencia CC0.
