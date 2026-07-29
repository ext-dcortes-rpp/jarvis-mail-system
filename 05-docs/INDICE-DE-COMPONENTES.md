# Índice de componentes del sistema

Mapa rápido de todos los bricks disponibles. Para cada uno: qué hace, dónde vive, y dónde estaba originalmente en el HTML base.

## Headers · 6 bricks

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Header Rappi | `02-components/headers/rappi.html` | 936-974 |
| Header RappiTravel | `02-components/headers/rappi-travel.html` | 978-1015 |
| Header RappiTurbo | `02-components/headers/rappi-turbo.html` | 1019-1054 |
| Header RappiTurboRest | `02-components/headers/rappi-turbo-rest.html` | 1058-1093 |
| Header RappiProBlack | `02-components/headers/rappi-pro-black.html` | 1097-1135 |
| Header RappiPro | `02-components/headers/rappi-pro.html` | 1138-1176 |

## Banners · 2 bricks + 6 atoms

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Big banner horizontal | `02-components/banners/big-banner-horizontal.html` | 1189-1352 |
| Big banner vertical | `02-components/banners/big-banner-vertical.html` | 1354-1510 |

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema. Las piezas internas del banner viven en `02-components/banners/banner_atoms/`: MODULOS fijos (`modulo_tags`, `modulo_img_altofijo_horizontal/vertical`, `modulo_img_automatica_horizontal` — esta última distinta de `atomo_img_automatica_*`) + ATOMOS de `MODULO ATOMOS`, todos con nombre `atomo_*` para ambos banners (`atomo_creditos`, `atomo_promo`, `atomo_textoxl`, `atomo_textom`, `atomo_texto_complemento`, `atomo_img_automatica`, `atomo_cta_interno`, cada uno en `_horizontal`/`_vertical`). Todavía sin línea de referencia en el HTML original, son ensamblados nuevos. (`modulo_img_variable` y `modulo_texto_secundario` se eliminaron por no ser necesarios.)

## CTAs · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| CTA template | `02-components/ctas/cta-template.html` | 1617-1635 |

## Deals · 2 bricks

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Deal grande | `02-components/deals/deal-large.html` | 1637-1727 |
| Deal small | `02-components/deals/deal-small.html` | 1729-1820 |

## Coupons · 1 brick · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo cupones | `02-components/coupons/cupones-modulo.html` | 1893-1977 |

## Benefits · 1 brick · NUEVO

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo beneficios | `02-components/benefits/modulo-beneficios.html` | 1979-2012 |

## Content modules · 5 bricks

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Módulo título | `02-components/content-modules/modulo-titulo.html` | 1822-1857 |
| Módulo 3 columnas | `02-components/content-modules/modulo-3-columnas.html` | 1859-1891 |
| Módulo contenido principal | `02-components/content-modules/modulo-contenido.html` | 2014-2173 |
| Módulo 2 columnas | `02-components/content-modules/modulo-2-columnas.html` | 2175-2274 |
| Módulo logos | `02-components/content-modules/modulo-logos.html` | 2276-2405 |

## Cierre · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Imagen de cierre | `02-components/closing/cierre.html` | 2407-2420 |

## Footer · 1 brick

| Componente | Archivo | Líneas en HTML original |
|------------|---------|------------------------|
| Footer general | `02-components/footer/footer.html` | 2430-2460 |

## Foundations · 2 archivos

| Archivo | Función | Líneas en HTML original |
|---------|---------|------------------------|
| `01-foundations/global-styles/head-meta-tags.html` | Meta tags y conditional comments Outlook | 429-451 |
| `01-foundations/global-styles/global-styles.html` | Bloque `<style>` completo + media queries | 452-884 |

---

## Resumen

**Total de bricks (componentes): 21**
- 6 headers
- 3 banners
- 1 CTA
- 2 deals
- 1 cupones (NUEVO)
- 1 beneficios (NUEVO)
- 5 módulos de contenido
- 1 cierre
- 1 footer

**Total de archivos de foundations: 2**

**Gran total: 23 archivos** que reemplazan un HTML monolítico de 2.487 líneas. (Nota: los conteos de headers y banners de esta página quedaron desactualizados tras la reestructuración a 10 marcas × 4 variantes y 2 banners + 6 átomos; pendiente de recalcular.)
