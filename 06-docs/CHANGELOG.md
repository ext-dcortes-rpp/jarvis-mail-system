# Changelog

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
