# 06 · Assets

> Imágenes y logos. La biblioteca visual del sistema.

## Estructura
- `images/` — Imágenes que se usan en los mails (banners, productos, ilustraciones)
- `logos/` — Todos los logos: Rappi, Travel, Turbo, Pro, ProBlack, partners de cobranding

## Estado actual

Hoy las imágenes viven en Google Drive y se referencian desde el HTML por URL pública (`https://lh3.googleusercontent.com/d/...`). Existe una taxonomía en Google Sheets ("TAXONOMÍA ASSETS") con dos hojas: **NUEVO MAILS** y **LOGOS MAIL**.

> **Por decidir.** Hay tres opciones para cómo manejar los assets en este repo:
> 1. Mantener Google Drive como fuente única y solo documentar la taxonomía aquí.
> 2. Migrar todo a un CDN y referenciar URLs nuevas.
> 3. Subir los assets al repo (no recomendado para producción).

## Reglas

- Las URLs de imágenes están en los componentes como `src="https://..."`.
- Cuando se cree un mail, el creador NO sube imágenes nuevas. Las solicita al equipo de diseño, que las publica en la TAXONOMÍA ASSETS.
- Si una URL no existe en la taxonomía, el mail no se entrega hasta que la imagen esté disponible.
