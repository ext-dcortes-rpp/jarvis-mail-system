# 06 · Assets

> Imágenes y logos. La biblioteca visual del sistema.

## Estructura

- `images/` — Imágenes que se usan en los mails: banners, productos, ilustraciones
- `logos/` — Todos los logos: Rappi, Travel, Turbo, Pro, Pro Black, y logos de partners de cobranding

## Dónde viven las imágenes hoy

Las imágenes del sistema están almacenadas en Google Drive y se referencian en los mails mediante su URL pública. Existe una taxonomía oficial en Google Sheets llamada **"TAXONOMÍA ASSETS"**, con dos hojas:
- **NUEVO MAILS** — imágenes de banners y contenido
- **LOGOS MAIL** — logos del sistema

> **Pendiente de decisión.** Hay tres opciones para manejar los assets en este repositorio:
>
> 1. **Mantener Google Drive como fuente única** y solo documentar la taxonomía aquí.
> 2. **Migrar todo a un CDN** y usar URLs nuevas en los mails.
> 3. **Subir los assets al repositorio** (no recomendado para producción, pero útil para tener la biblioteca documentada en un solo lugar).
>
> Esta decisión se tomará cuando el sistema esté en uso regular y se tenga claridad sobre volúmenes y frecuencia de actualización.

## Reglas de trabajo con imágenes

- Las URLs de imágenes aparecen dentro de los componentes, en el atributo `src="..."` de cada imagen.
- Cuando se crea un mail, quien lo arma **no sube imágenes nuevas por su cuenta**. Las solicita al equipo de diseño, que las publica en la TAXONOMÍA ASSETS.
- Si una URL de imagen no existe en la taxonomía, el mail no se entrega hasta que la imagen esté disponible y publicada.

Esta regla viene del Gem de Gemini y aplica también para este repositorio.
