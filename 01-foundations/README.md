# 01 · Foundations

> Las reglas del LEGO.

Aquí viven las reglas que cualquier brick respeta: tipografías, colores, espaciados, separadores, media queries. **Nadie debería tocar esta carpeta sin coordinarlo con el equipo de diseño**, porque cualquier cambio aquí afecta a TODOS los mails.

## Archivos

### `global-styles/global-styles.html`
Bloque `<style>` completo del HTML base con:
- Tipografías y tamaños (h1 a h6, `.txts`, `.txtl`)
- Clases utilitarias (`.separador`, `.separador-M`, `.separador-S`)
- Reglas para `table.wrapper`
- Las dos media queries: `@media (max-width: 480px)` y `@media (max-width: 620px)`
- Todas las clases de header (`.header-logo`, `.header-logoturbo`, `.header-tag`...)
- Las clases de banner (`.banner-logo1-1`, `.banner-logo-multi`, `.altobanner1`)
- Las clases de cupones (`.cuponmob`)
- Las clases de alineación (`.alineado-center`, `.txtbigbanner`)

Adentro hay comentarios condicionales tipo:

```css
/*
si Tipo de Kv = Generico background-image debe ser https://...
si Tipo de Kv = Turbo background-image debe ser https://...
si Tipo de Kv = Pro background-image debe ser https://...
*/
```

Estos comentarios documentan un esquema de color anterior al sistema de temas actual; ya no se usan para producir mails nuevos.

### `global-styles/head-meta-tags.html`
Los meta tags del `<head>`: viewport, charset, conditional comments para Outlook (MSO). Se inyecta antes del `<style>`.

Además, aquí vive la sección Liquid **TEMAS**: el `{% if tema_general_mail_general == '...' %}` que define, para cada uno de los 11 temas (Beige 100/150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Dark neon, Dark Turbo, Dark Neutro, Pro, ProBlack), todas las variables de color/imagen del mail (`bg_solid_mail_general`, `color_texto_mail_general`, `color_acento1_mail_general`, `bg_contenedor1_mail_general`, `color_footer_mail_general`, etc.). Ver `06-docs/GUIA-DE-TEMAS.md` para el detalle completo de cada variable.

## Tokens (a futuro)

La carpeta `tokens/` está pensada para cuando el sistema migre a tokens de diseño. Por ahora está vacía, pero cuando exista contendrá:
- `colors.css` — La paleta Neon (FF7A4D, FF2526, FF4583, EB5583) + neutros
- `spacing.css` — Las medidas de los separadores (16px, 10px, 4px)
- `radii.css` — Los border-radius que se repiten (16px, 7px, 14px)
- `typography.css` — Familia Trebuchet/Arial y la escala de tamaños

## Por qué esto vive aparte

Cuando un diseñador quiere saber "qué color es #FF7A4D" o "cuánto es un separador-M", no debería tener que abrir un componente. Esa información vive aquí.
