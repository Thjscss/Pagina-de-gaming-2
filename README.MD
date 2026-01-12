# PASOS PARA LEVANTAR LA WEB
Para testing con sass 
`sass --watch scss:css`
Para levantar la web a git
`git add . , git commit -m "Arreglo botones y colores estilo Maximus", git push`

---

## Optimización de imágenes (recomendado)
Para mejorar tiempos de carga y rendimiento se recomienda generar versiones WebP y comprimir las imágenes originales.

Opciones rápidas:

- Con libwebp (cwebp):
  - `cwebp img/wallpapers/wallpaper1.jpeg -q 80 -o img/wallpapers/webp/wallpaper1.webp`

- Con imagemin (npm):
  - `npm i -D imagemin-cli imagemin-webp imagemin-mozjpeg imagemin-pngquant`
  - `npx imagemin img/wallpapers/* --out-dir=img/wallpapers/webp --plugin=webp`

Notas:
- Guarda siempre versiones originales de alta resolución en caso de necesitar impresiones o descargas.
- Si querés, puedo agregar un `package.json` y scripts para automatizar la conversión/compresión.

---

## Scripts npm añadidos
- `npm i` — instala dependencias de desarrollo (`sass`, `imagemin-cli`, `imagemin-webp`, `imagemin-mozjpeg`, `imagemin-pngquant`).
- `npm run build:sass` — compila todos los archivos SASS a `css/style.css`.
- `npm run watch:sass` — compila en modo watch mientras editas.
- `npm run optimize:images` — genera versiones WebP optimizadas en `img/wallpapers/webp/`.
- `npm run build` — ejecuta `build:sass` + `optimize:images`.

> Nota: También añadí un GitHub Action (`.github/workflows/build-optimize.yml`) que ejecuta la compilación y optimización en cada push a `main`. Los archivos WebP resultantes se almacenan en `img/wallpapers/webp/` y se intentará commitearlos en el repo si hay cambios.


---

## Uso de Mixins SASS (rápido)
- Creé `scss/utils/_mixins.scss` con `@mixin gallery-image()` y `@mixin button-variant()`.
- Para reutilizar estilos: `@use "../utils/mixins" as mixins;` y luego `@include mixins.gallery-image(220px, 160px);`.
- Esto ayuda a mantener estilos consistentes y facilita la adaptación responsive.

