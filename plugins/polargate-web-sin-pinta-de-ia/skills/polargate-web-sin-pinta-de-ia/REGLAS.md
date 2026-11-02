# Reglas en español

Las webs hechas con IA se parecen porque repiten los mismos gestos: degradado morado, tarjetas dentro de tarjetas, cifras inventadas. Estas reglas evitan esos gestos. Se aplican siempre, aunque nadie las recuerde.

## Antes de diseñar

1. Lee el proyecto: colores, letra, componentes y textos que ya existan. Si hay marca, manda la marca.
2. Pregunta una vez, y solo lo que no encuentres: qué se vende, a quién, qué tiene que hacer quien entra y qué tono quieren.
3. Decide una sola idea por pantalla.

## Reglas que no se saltan

**Código**

1. Cada color y cada fuente sale de una variable en `:root`. Ningún valor suelto después.
2. Nunca `transition: all`. Nunca animes `width`, `height`, `top` ni `left`.
3. `overflow-x: clip` en `html` y `body`. Nunca `hidden` ni `100vw`.
4. Las columnas con imágenes usan `minmax(0, 1fr)`, y los títulos grandes `overflow-wrap: break-word` y `min-width: 0`.
5. El contenido va en un contenedor con ancho máximo y centrado: en pantallas grandes crece el margen, no la rejilla.

**Accesibilidad**

6. Todo lo que se pulsa tiene `:focus-visible`, y aparece al instante.
7. Toda animación tiene alternativa con `prefers-reduced-motion: reduce`, y el contenido se ve sin JavaScript.

**Lo que delata a la IA**

8. Nunca cifras, testimonios, logos ni casos inventados. Si no hay datos reales, no se ponen.
9. Nunca una palabra suelta en cursiva dentro de un título.
10. Nunca una etiqueta pequeña en mayúsculas espaciadas sobre el título. Etiquetas y menús van en la letra normal, un punto más pequeña.
11. Nunca textos unidos con puntos medios, flechas pegadas a un enlace ni puntitos de estado decorativos.
12. Nunca degradado de morado a azul, tarjeta dentro de tarjeta, emoji como icono ni una ventana de navegador dibujada a mano.

**Composición**

13. El titular, una frase y el botón principal se ven sin hacer scroll a 1280x800.
14. Unas 80 palabras por pantalla como mucho.

## Al terminar

1. Mira la página en móvil y en ordenador, en claro y en oscuro si los tiene.
2. Repasa las 14 reglas una a una contra el código. Di cuáles has comprobado.
3. Pasa el comprobador y arregla cada `FAIL`: `node <skill-dir>/scripts/sloplint.mjs <fichero>`.
