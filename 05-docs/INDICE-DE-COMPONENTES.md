# Índice de componentes del sistema

Mapa rápido de todos los bricks disponibles. Para cada uno: qué hace y dónde vive.

> **Nota sobre las líneas de "HTML original":** recalculadas contra `06-examples/template_maestro_original.html` en su estado actual (2.632 líneas, tras sumar el tema Gris 100 + `bg_rgb_mail_general` en los 12 temas). Si el archivo vuelve a reestructurarse, estas líneas quedarán desactualizadas otra vez — ante cualquier duda, `grep` el rol/clase real en el archivo en vez de confiar en el número.

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

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema. Las piezas internas del banner viven en `02-components/02_banners/banner_moleculas/` (22 archivos actualmente):
- **MODULOS** fijos (se conservan tal cual en `big-banner-*.html`, no son MOLECULAS): `modulo_tags_horizontal/vertical`, `modulo_img_altofijo_horizontal/vertical`, `modulo_img_automatica_horizontal` (distinta de `molecula_img_automatica_*`).
- **MOLECULAS** de `MODULO MOLECULAS`, nombre `molecula_*` para ambos banners: `molecula_creditos`, `molecula_promo`, `molecula_textoxl`, `molecula_textom`, `molecula_img_automatica`, `molecula_cta_interno`, `molecula_texto_complementario`, cada uno en `_horizontal`/`_vertical`. (Renombradas de `atomo_*` — el Figma del sistema de diseño también movió esta sección de la página Atoms a la página Molecules.)
- `molecula_texto_complementario_horizontal.html` / `_vertical.html` reemplazan al viejo `modulo_texto_complementario.html` (sin sufijo, ya eliminado) — contenido pendiente de insertar manualmente en cada uno.

⚠️ **Posible duplicado sin resolver:** además de `molecula_textom_horizontal.html` / `molecula_textom_vertical.html` (los documentados arriba), también existen `molecula_texto_M_horizontal.html` / `molecula_texto_M_vertical.html` con contenido idéntico. El Figma del sistema documenta la tarjeta como "atomo_texto_M" (ahora molécula), lo que sugiere que `_textom` es el sobrante de una renombrada a medias — pendiente que el equipo lo confirme y borre el archivo que no corresponda.

(`modulo_img_variable` y `modulo_texto_secundario` se eliminaron por no ser necesarios.)

## CTAs · 2 archivos, 1 brick conceptual

| Componente | Archivo |
|------------|---------|
| Cómo se llama (define variables) | `02-components/03_ctas/cta-llamado.html` |
| El botón (content block, 8 variantes de `style_Look`) | `02-components/03_ctas/cta-template.html` |

## Deals · 1 brick activo

| Componente | Archivo |
|------------|---------|
| Deals en columnas (activo) | `02-components/04_content-modules/deals/deal_columnas.html` |

De a pares en una grilla de 2 celdas (50/50); si la cantidad es impar, se elimina el contenido de la celda derecha (la celda queda vacía). `deal-large.html` y `deal-small.html` ya no se usan — se conservan como `deal-large.backup.html` / `deal-small.backup.html` para no perder el trabajo, no enlazados desde ningún template ni visualizador.

## Coupons · 1 brick, 2 archivos · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo cupones (2 celdas, siempre en pares) | `02-components/04_content-modules/coupons/cupones-modulo.html` | 2100-2230 |
| Celda de título suelta (reemplaza a la celda 1) | `02-components/04_content-modules/coupons/celda_cupon_titulo.html` | 2122-2151 (inline dentro del ejemplo de cupones) |

## Benefits · 1 brick · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo beneficios | `02-components/04_content-modules/benefits/modulo-beneficios.html` | 1878-1916 |

## Content modules · 6 bricks

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo título | `02-components/04_content-modules/title/modulo-titulo.html` | 1783-1813 |
| Módulo bullet | `02-components/04_content-modules/bullet/modulo_bullet.html` | 1814-1834 |
| Módulo 3 columnas | `02-components/04_content-modules/3columnas/modulo-3-columnas.html` | 2232-2319 |
| Módulo 1 columna (bloques de moléculas + imagen full-width, en cualquier orden) | `02-components/04_content-modules/1columna/modulo-1columna.html` | 1835-1877 |
| Módulo 2 columnas | `02-components/04_content-modules/2columnas/modulo-2-columnas.html` | 2320-2417 |
| Módulo logos | `02-components/04_content-modules/logos/modulo-logos.html` | 2419-2583 |

## Cierre · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Imagen de cierre | `02-components/05_closing/cierre.html` | 2590-2600 |

## Footer · 1 brick, 4 archivos (1 orquestador + 3 variantes)

| Componente | Archivo |
|------------|---------|
| Orquestador (elige la variante y los toggles) | `02-components/06_footer/footer.html` |
| General — la más usada, toda comunicación a usuarios | `02-components/06_footer/footer_general.html` |
| Sin Amor — sin WhatsApp, comunicaciones más formales | `02-components/06_footer/footer_sinamor.html` |
| RTS — predeterminado para repartidores/colaboradores | `02-components/06_footer/footer_rts.html` |

## Foundations · 2 archivos

| Archivo | Función | Líneas en HTML original |
|---------|---------|------------------------|
| `01-foundations/global-styles/head-meta-tags.html` | Bloque Liquid de temas — un `{% if tema_general_mail_general == '...' %}` por cada uno de los 12 temas | 1-629 |
| `01-foundations/global-styles/global-styles.html` | `<head>` completo: meta tags, conditionals MSO para Outlook, bloque `<style>` y las dos media queries | 630-1185 |

---

## Resumen

**Total de bricks (componentes): 24**
- 10 headers (marcas)
- 2 banners
- 1 CTA
- 1 deals (activo: `deal_columnas.html`)
- 1 cupones
- 1 beneficios
- 6 módulos de contenido (título, bullet, 3 columnas, 1 columna, 2 columnas, logos)
- 1 cierre
- 1 footer (3 variantes: general, sin amor, rts)

**Total de archivos en `02-components/`: 103** (41 en `01_headers/` + 24 en `02_banners/` (incluye `banner_moleculas/`) + 2 en `03_ctas/` + 31 en `04_content-modules/` (incluye `content_moleculas/`, grillas de logos, backups de deals) + 1 en `05_closing/` + 4 en `06_footer/`)

**Total de archivos de foundations: 2**

Este documento reemplaza al HTML monolítico de referencia (`06-examples/template_maestro_original.html`), que hoy tiene 2.632 líneas y sirve como catálogo de ejemplo de casi todas las piezas del sistema (declara el tema al inicio, luego banner, CTAs, deals, cupones, beneficios, módulos de contenido, cierre y footer, en ese orden).
