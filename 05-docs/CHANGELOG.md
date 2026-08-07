# Changelog

## [0.6.0] - Tema Gris 100, `bg_rgb_mail_general` y ajuste de interlineado

### Agregado
- **Tema Gris 100** — séptimo tema pastel del sistema (ahora 12 en total: 7 pastel + 3 oscuros/invertidos + 2 premium). Comunicación neutra, sin dorado, con acento gris (`#7D8188` light / `#B8BCC2` dark). Rama `{% elsif tema_general_mail_general == 'gris100' %}` en `01-foundations/global-styles/head-meta-tags.html` y en la copia embebida de `06-examples/template_maestro_original.html`. Las imágenes reutilizan las URLs del tema ProBlack — todavía no tiene asset propio.
- **`bg_rgb_mail_general`** en los 12 temas, debajo de `bg_solid_mail_general` — mismo tono en formato `rgba(x,x,x,0.7)`. Variable de definición: hoy no se consume en ningún HTML del sistema, queda lista para usos futuros que necesiten transparencia sobre el fondo sólido (overlays, sombras). Agregada tanto en `head-meta-tags.html` como en `template_maestro_original.html`.

### Cambiado
- **Interlineado +1px** en toda la tipografía de `01-foundations/global-styles/global-styles.html`: `h1`-`h6`, `.legal` y las 6 clases `bnr-*` (`xl`/`lg`/`md`/`hasta-xl`/`hasta-lg`/`sm`), en el bloque base y en los dos `@media` (`max-width: 480px` y `620px`). Solo `line-height` — ningún `font-size` cambió.
- `06-examples/template_maestro_original.html`: se reemplazó el `<head>` completo por la versión actualizada de `global-styles.html`. De paso corrigió dos divergencias que ya existían entre el maestro y el foundation real: `.bnr-md` en mobile tenía `font-size: 55px` (debía ser `45px`, igual que su propio `line-height`) y `cobranding-l` tenía valores desalineados (`36/31/42/26` en vez de `38/33/44/27`).
- Documentación (`05-docs/GUIA-DE-TEMAS.md`, `01-foundations/README.md`, `05-docs/INDICE-DE-COMPONENTES.md`) actualizada: menciones de "11 temas" pasan a "12", tabla de tamaños de texto y de `bnr-*` con los valores nuevos, y líneas de `template_maestro_original.html` recalculadas (el archivo pasó de 2.580 a 2.632 líneas por las adiciones de arriba).
- Figma **Doc-DS-Mails** sincronizado en paralelo: `02 · Tokens`, `03 · Temas`, `08 · HTML Bridge` y `10 · Changelog` (entrada `v2.2`) reflejan los mismos cambios de esta versión.

## [0.5.0] - Eliminación del esqueleto (base-template) y renumeración de carpetas

### Eliminado
- Carpeta `02-base-template/` (`opening.html`, `body-wrapper-open.html`, `body-wrapper-close.html`, `closing.html`) — el repo ya no incluye un archivo de "esqueleto" propio.
- Carpeta `08-examples/` (duplicado suelto de `test_claude_1_original.html`).

### Cambiado
- Renumeración de carpetas: `03-components/` → `02-components/`, `04-templates/` → `03-templates/`, `05-assets/` → `04-assets/`, `06-docs/` → `05-docs/`, `07-examples/` → `06-examples/`.
- El flujo de ensamblaje de un mail (README, `COMO-ARMAR-UN-MAIL.md`, `USO-DE-CADA-PARTE.md`) ya no incluye los pasos de esqueleto; empieza directamente en el header.
- `banners/`: ya son 2 formatos (horizontal, vertical) + `banner_atoms/`, no 3.

## [0.4.0] - Sistema de temas, reestructuración de headers y documentación al día

### Agregado
- **`06-docs/GUIA-DE-TEMAS.md`**: guía completa de los 11 temas del sistema (Beige 100/150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Dark neon, Dark Turbo, Dark Neutro, Pro, ProBlack), sus variables Liquid y reglas particulares.
- Sección Liquid `TEMAS` en `01-foundations/global-styles/head-meta-tags.html`: un `{% if tema_general_mail_general == '...' %}` por tema con todas sus variables de color/imagen.
- `03-components/headers/`: 10 carpetas de marca (antes 6 archivos sueltos), cada una con 4 variantes (`centrado-claro`, `centrado-oscuro`, `columnas-claro`, `columnas-oscuro`).

### Cambiado
- Renumeración de carpetas: `05-templates/` → `04-templates/`, `06-assets/` → `05-assets/`, `07-docs/` → `06-docs/`, `08-examples/` → `07-examples/`.
- `03-components/footer/footer.html`: `font_style_look` ahora toma el valor de `{{color_footer_mail_general}}` del tema activo en vez de asignarse a mano.
- READMEs de todas las carpetas actualizados para reflejar el sistema de temas, la nueva estructura de headers, y el footer dirigido por tema.

### Eliminado
- Carpeta `04-variants/` (los 5 CSS de `kv-types/` y su README) — el esquema que reemplazaban nunca se completó de esa forma; el tema se resuelve por Liquid, no por CSS aplicado como capa.
- `06-docs/GUIA-DE-KVS.md` — reemplazada por `06-docs/GUIA-DE-TEMAS.md`.

## [0.3.0] - Documentación expandida de KVs y uso de componentes

### Agregado
- **`06-docs/GUIA-DE-KVS.md`**: documentación exhaustiva de cómo se aplican los 5 KVs en las 7 zonas del HTML donde afectan. Incluye tabla maestra de referencia rápida y lista de errores comunes con cómo evitarlos.
- **`06-docs/USO-DE-CADA-PARTE.md`**: guía brick por brick de cuándo usar cada componente, sus reglas internas y el orden recomendado de ensamblaje.
- Sección "Documentación clave" en el README principal apuntando a estos dos documentos.

## [0.2.0] - Actualización con nuevos módulos

### Agregado
- **Módulo CUPONES** (`03-components/coupons/cupones-modulo.html`): tabla en pares con variante Cupón Title.
- **Módulo BENEFICIOS** (`03-components/benefits/modulo-beneficios.html`): card de beneficios con imagen + texto.

### Cambiado
- Reordenamiento del orden de headers: `RappiProBlack` ahora aparece antes de `RappiPro` (siguiendo el orden del HTML base actualizado).
- Renumeración de líneas en `INDICE-DE-COMPONENTES.md` al expandir el HTML base.
- Total de componentes: pasa de 19 a 21 bricks.

## [0.1.0] - Setup inicial

### Agregado
- Estructura inicial de carpetas (foundations, base-template, components, variants, templates, assets, docs, examples).
- Extracción de los 19 componentes del HTML base original.
- Documentación inicial: README principal, guía "cómo armar un mail", índice de componentes, contributing.
