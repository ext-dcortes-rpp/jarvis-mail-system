# Índice de componentes del sistema

Mapa rápido de todos los bricks disponibles. Para cada uno: qué hace y dónde vive.

> **Nota sobre las líneas de "HTML original":** las columnas de línea de este documento se escribieron cuando `06-examples/template_maestro_original.html` era un archivo de ~2.487 líneas. Ese archivo hoy tiene 1475 líneas — se recortó/simplificó y ya no conserva la mayoría de esas secciones en esas posiciones. Las referencias de línea que siguen (CTA, deals, cupones, beneficios, módulos de contenido, cierre, footer) están desactualizadas y no deberían usarse como fuente de verdad; pendiente recalcularlas o quitarlas.

## Headers · 10 bricks (marcas) · 41 archivos

Cada marca es una subcarpeta con 4 archivos (fondo claro/oscuro × disposición centrado/columnas). Ver el detalle completo en `02-components/README.md`.

| Carpeta | Marca |
|---------|-------|
| `02-components/01_headers/rappi/` | Rappi |
| `02-components/01_headers/rappi-travel/` | RappiTravel |
| `02-components/01_headers/soyrappi/` | SoyRappi |
| `02-components/01_headers/rappi-turbo/` | RappiTurbo |
| `02-components/01_headers/rappi-turbo-rest/` | RappiTurbo Restaurantes |
| `02-components/01_headers/rappi-pro/` | RappiPro |
| `02-components/01_headers/rappi-pro-black/` | RappiPro Black |
| `02-components/01_headers/rappi-defensoria/` | Defensoría |
| `02-components/01_headers/rappi-entregador/` | RappiEntregador |
| `02-components/01_headers/contenido-aliado/` | Contenido aliado |

Más el archivo `_header-wrapper.html` (la envolvente común a los 40 anteriores) = 41 archivos en total.

## Banners · 2 bricks + banner_moleculas/

| Componente | Archivo |
|------------|---------|
| Big banner horizontal | `02-components/02_banners/big-banner-horizontal.html` |
| Big banner vertical | `02-components/02_banners/big-banner-vertical.html` |

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema. Las piezas internas del banner viven en `02-components/02_banners/banner_moleculas/` (20 archivos actualmente):
- **MODULOS** fijos (se conservan tal cual en `big-banner-*.html`, no son MOLECULAS): `modulo_tags_horizontal/vertical`, `modulo_img_altofijo_horizontal/vertical`, `modulo_img_automatica_horizontal` (distinta de `molecula_img_automatica_*`), `modulo_texto_complementario` (placeholder, ver `USO-DE-CADA-PARTE.md`).
- **MOLECULAS** de `MODULO MOLECULAS`, nombre `molecula_*` para ambos banners: `molecula_creditos`, `molecula_promo`, `molecula_textoxl`, `molecula_textom`, `molecula_img_automatica`, `molecula_cta_interno`, cada uno en `_horizontal`/`_vertical`. (Renombradas de `atomo_*` — el Figma del sistema de diseño también movió esta sección de la página Atoms a la página Molecules.)

⚠️ **Posible duplicado sin resolver:** además de `molecula_textom_horizontal.html` / `molecula_textom_vertical.html` (los documentados arriba), también existen `molecula_texto_M_horizontal.html` / `molecula_texto_M_vertical.html` con contenido idéntico. El Figma del sistema documenta la tarjeta como "atomo_texto_M" (ahora molécula), lo que sugiere que `_textom` es el sobrante de una renombrada a medias — pendiente que el equipo lo confirme y borre el archivo que no corresponda.

(`modulo_img_variable` y `modulo_texto_secundario` se eliminaron por no ser necesarios.)

## CTAs · 1 brick

| Componente | Archivo |
|------------|---------|
| CTA template | `02-components/03_ctas/cta-template.html` |

## Deals · fuera de uso (0 bricks activos)

Ya no se usan en el sistema. Se conservan como `02-components/04_content-modules/deals/deal-large.backup.html` y `02-components/04_content-modules/deals/deal-small.backup.html` para no perder el trabajo — no están enlazados desde ningún template ni desde el visualizador.

⚠️ La carpeta también tiene `deal_columnas.html`, sin documentar todavía — pendiente confirmar con el equipo si reemplaza a los backups.

## Coupons · 1 brick · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo cupones | `02-components/04_content-modules/coupons/cupones-modulo.html` | 1893-1977 |

## Benefits · 1 brick · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo beneficios | `02-components/04_content-modules/benefits/modulo-beneficios.html` | 1979-2012 |

## Content modules · 5 bricks

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo título | `02-components/04_content-modules/title/modulo-titulo.html` | 1822-1857 |
| Módulo 3 columnas | `02-components/04_content-modules/3columnas/modulo-3-columnas.html` | 1859-1891 |
| Módulo contenido principal | `02-components/04_content-modules/1columna/modulo-1columna.html` | 2014-2173 |
| Módulo 2 columnas | `02-components/04_content-modules/2columnas/modulo-2-columnas.html` | 2175-2274 |
| Módulo logos | `02-components/04_content-modules/logos/modulo-logos.html` | 2276-2405 |

## Cierre · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Imagen de cierre | `02-components/05_closing/cierre.html` | 2407-2420 |

## Footer · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Footer general | `02-components/06_footer/footer.html` | 2430-2460 |

## Foundations · 2 archivos

| Archivo | Función | Líneas en HTML original |
|---------|---------|------------------------|
| `01-foundations/global-styles/head-meta-tags.html` | Meta tags y conditional comments Outlook | 429-451 |
| `01-foundations/global-styles/global-styles.html` | Bloque `<style>` completo + media queries | 452-884 |

---

## Resumen

**Total de bricks (componentes): 22**
- 10 headers (marcas)
- 2 banners
- 1 CTA
- 0 deals (fuera de uso, ver arriba)
- 1 cupones (NUEVO)
- 1 beneficios (NUEVO)
- 5 módulos de contenido
- 1 cierre
- 1 footer

**Total de archivos en `02-components/`: 81** (41 en `01_headers/` + 22 en `02_banners/` (incluye `banner_moleculas/`) + 2 en `03_ctas/` + 11 en `04_content-modules/` + 1 en `05_closing/` + 4 en `06_footer/`)

**Total de archivos de foundations: 2**

Este documento reemplaza un HTML monolítico original de ~2.487 líneas; hoy esa referencia histórica (`06-examples/template_maestro_original.html`) tiene 1475 líneas — ver la nota al inicio sobre por qué las columnas de línea ya no son confiables.
