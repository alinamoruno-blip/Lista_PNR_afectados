# Procesador de PNR Afectados

App web estática (un solo archivo `index.html`) que replica en el navegador
el mismo proceso que hicimos manualmente sobre el Excel:

1. Lee la hoja "PNR" y la hoja "Pasajeros".
2. Genera la hoja "Afectados" con las filas coincidentes (o "No se encontró
   coincidencia" resaltado en naranja si un PNR no aparece en Pasajeros).
3. Genera la hoja "CONTACTOS A NOTIFCAR" con las columnas Pasajero, PNR,
   SSR CTCM, SSR CTCE y todas las columnas que empiezan con "AP".
4. Descarga el Excel resultante.

Todo el procesamiento ocurre en el navegador del usuario (usando la librería
ExcelJS vía CDN) — no hay backend ni servidor, por lo que los archivos nunca
se suben a ningún lado. Esto significa que se puede desplegar como sitio 100%
estático en Netlify, sin necesidad de Netlify Functions.

## Cómo desplegar en Netlify (opción más rápida: arrastrar y soltar)

1. Ve a https://app.netlify.com/drop
2. Arrastra esta carpeta completa (la que contiene `index.html` y
   `netlify.toml`) a la zona de "drag and drop".
3. Netlify le asigna automáticamente una URL pública (algo como
   `nombre-al-azar.netlify.app`). Ya está en línea.
4. Opcional: en "Site settings" puedes cambiar el nombre del sitio o
   conectar un dominio propio.

## Cómo desplegar conectando un repositorio de GitHub (recomendado si vas a
seguir editando la app)

1. Sube esta carpeta a un repositorio de GitHub.
2. En Netlify: "Add new site" → "Import an existing project" → conecta tu
   cuenta de GitHub y selecciona el repositorio.
3. Build command: (déjalo vacío, no hay build)
   Publish directory: `.`
4. Deploy site.

Cada vez que hagas push a GitHub, Netlify volverá a desplegar automáticamente.

## Notas

- El archivo subido debe tener una hoja llamada "Pasajeros" (con una columna
  "PNR" y una columna "Pasajero") y una hoja llamada "PNR" (con una columna
  "PNR"). Si tus archivos usan otros nombres de hoja, la app tiene dos campos
  para ajustar esos nombres antes de procesar.
- Si el archivo es muy grande (varios miles de filas), el procesamiento puede
  tardar unos segundos — es normal, todo corre en el navegador.
- No requiere claves ni configuración adicional para funcionar.
