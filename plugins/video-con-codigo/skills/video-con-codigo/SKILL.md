---
name: video-con-codigo
description: Hace vídeos con código usando HyperFrames: HTML y animación que se renderizan a MP4 en local. Usar para reels, TikToks, explicaciones, títulos y animaciones con texto cuando pidan un vídeo sin cámara, con el formato vertical listo para publicar en redes.
---

# Vídeo con código

HyperFrames renderiza una página HTML a vídeo, fotograma a fotograma. El mismo código da siempre el mismo vídeo, y cambiar un texto es editar una línea.

Funciona en tu ordenador con Node 22 o más nuevo y FFmpeg. Render local, sin pagar nada.

## Empezar

```bash
npx hyperframes init mi-video
cd mi-video
```

Para el detalle de cada función, instala sus skills oficiales con `npx hyperframes skills update`, o usa `npx hyperframes docs <tema>`.

## Formato para redes

En `index.html` pon el tamaño en vertical. Hay que cambiarlo en cuatro sitios: el `viewport`, el CSS de `html, body` y los `data-width` y `data-height` de `#root`.

```html
<div id="root" data-composition-id="main" data-start="0" data-duration="8"
     data-width="1080" data-height="1920">
```

Y renderiza con máxima calidad:

```bash
npx hyperframes render --quality delivery --crf 14 -o video.mp4
```

Sale en H.264, 1080x1920, 30 fps. Mientras pruebas, usa `--quality draft`.

## Zona segura

TikTok y Reels tapan parte de la pantalla. Deja fuera de estas zonas todo texto importante:

- El 25 % de abajo: nombre, pie y música.
- El 12 % de arriba.
- El 15 % de la derecha: botones.

En 1080x1920, el texto va entre 230 y 1440 px de alto y no pasa de 918 px de ancho.

## Reglas para que renderice bien

1. Todo lo que aparece lleva `class="clip"`, `data-start` y `data-duration`.
2. La duración del vídeo es la de `data-duration` en `#root`.
3. Una línea de tiempo de GSAP en pausa, guardada en `window.__timelines["main"]`.
4. Nada de `Date.now()`, azar sin semilla, peticiones de red, temporizadores ni bucles infinitos.
5. Anima `transform` y `opacity`, no `left`, `top`, `width` ni `height`.
6. Las rutas de ficheros son `assets/...`, sin barra delante.
7. Las fuentes que no vengan incluidas se cargan desde `assets/fonts/` con `@font-face`.

## Cómo trabajar

1. Escribe el guion: una idea por pantalla, frases cortas.
2. Crea la escena y pasa `npx hyperframes check --json`. Arregla todo lo que diga.
3. Mira fotogramas sueltos con `npx hyperframes snapshot` antes de renderizar.
4. Enséñalo con `npx hyperframes preview` y espera el visto bueno.
5. Renderiza y comprueba el fichero con `ffprobe`.

## Estilos

Si no sabes qué estilo poner, mira los 15 estilos de motion design de [mg-styles-15](https://github.com/Vincentwei1021/mg-styles-15) y escribe tu propia versión con los colores y la letra de tu marca.

## Música y licencias

- Nunca metas una canción comercial dentro del fichero: te pueden silenciar o tumbar el vídeo.
- Usa música propia o con licencia comercial, y fuentes con licencia comercial.

## Lo que cuesta dinero

El render local es gratis. Se paga aparte el render en la nube (`cloud`, `lambda`, `cloudrun`) y lo generado con HeyGen, como avatares o voces. Pregunta antes de usarlo.
