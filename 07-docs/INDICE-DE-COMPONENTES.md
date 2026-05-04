# Índice de componentes del sistema

Mapa rápido de todos los bricks disponibles. Para cada uno: qué hace y dónde vive.

---

## Headers · 6 bricks

| Componente | Archivo |
|------------|---------|
| Header Rappi | `03-components/headers/rappi.html` |
| Header RappiTravel | `03-components/headers/rappi-travel.html` |
| Header RappiTurbo | `03-components/headers/rappi-turbo.html` |
| Header RappiTurboRest | `03-components/headers/rappi-turbo-rest.html` |
| Header RappiPro | `03-components/headers/rappi-pro.html` |
| Header RappiProBlack | `03-components/headers/rappi-pro-black.html` |

> Solo se usa un header por mail.

---

## Banners · 3 bricks

| Componente | Archivo |
|------------|---------|
| Banner horizontal | `03-components/banners/big-banner-horizontal.html` |
| Banner vertical | `03-components/banners/big-banner-vertical.html` |
| Banner editorial | `03-components/banners/banner-editorial.html` |

> Solo se usa un banner por mail.

---

## CTAs (botones de acción) · 1 brick

| Componente | Archivo |
|------------|---------|
| Botón de acción | `03-components/ctas/cta-template.html` |

> Se pueden usar varios CTAs por mail.

---

## Deals · 2 bricks

| Componente | Archivo |
|------------|---------|
| Deal grande | `03-components/deals/deal-large.html` |
| Deal small | `03-components/deals/deal-small.html` |

> Máximo 4 deals por mail.

---

## Módulos de contenido · 5 bricks

| Componente | Archivo |
|------------|---------|
| Módulo de título | `03-components/content-modules/modulo-titulo.html` |
| Módulo 3 columnas | `03-components/content-modules/modulo-3-columnas.html` |
| Módulo 2 columnas | `03-components/content-modules/modulo-2-columnas.html` |
| Módulo de logos | `03-components/content-modules/modulo-logos.html` |
| Módulo de contenido principal | `03-components/content-modules/modulo-contenido.html` |

> Se pueden usar varios módulos por mail, en el orden que necesites.

---

## Cierre · 1 brick

| Componente | Archivo |
|------------|---------|
| Imagen de cierre | `03-components/closing/cierre.html` |

> Se omite en mails Pro, Pro Black, o cuando la fuente dice "sin cierre".

---

## Footer · 1 brick

| Componente | Archivo |
|------------|---------|
| Pie de mail | `03-components/footer/footer.html` |

> El footer va siempre. Nunca se omite.

---

## Esqueleto · 4 archivos (no son bricks — son la estructura fija)

| Archivo | Función |
|---------|---------|
| `02-base-template/opening.html` | Inicio obligatorio del mail |
| `02-base-template/body-wrapper-open.html` | Abre la zona de contenido del cuerpo |
| `02-base-template/body-wrapper-close.html` | Cierra la zona de contenido del cuerpo |
| `02-base-template/closing.html` | Fin obligatorio del mail |

---

## Foundations · 2 archivos (reglas de diseño — no se tocan)

| Archivo | Función |
|---------|---------|
| `01-foundations/global-styles/head-meta-tags.html` | Configuración técnica del mail (compatibilidad con clientes de correo) |
| `01-foundations/global-styles/global-styles.html` | Todos los estilos visuales del sistema: colores, fuentes, tamaños, versión móvil |

---

## Resumen de bricks

| Tipo | Cantidad |
|------|---------|
| Headers | 6 |
| Banners | 3 |
| CTAs | 1 |
| Deals | 2 |
| Módulos de contenido | 5 |
| Cierre | 1 |
| Footer | 1 |
| **Total de bricks** | **19** |

Más 4 archivos de esqueleto y 2 de foundations = **25 archivos en total**, que reemplazaron un único archivo gigante de más de 2.400 líneas.
