# Guía completa de Temas

Esta guía documenta el sistema de **temas** de J.A.R.V.I.S.: cómo se elige el tema de un mail, qué variables Liquid controla, y las reglas particulares de cada grupo de temas.

> Lee esta guía completa antes de producir tu primer mail. Tenla a la mano siempre.

---

## ¿Qué es un tema?

Un **tema** es la identidad visual completa de un mail: fondo, tipografía, acentos, contenedores, tags, banner, y los componentes adicionales de descuento/créditos. Dos mails con los mismos componentes pero distinto tema se ven completamente diferentes.

El tema viene definido en la **fuente** que envía la persona que pide el mail, en la variable `tema_general_mail_general`. Todo el sistema de temas vive en un único lugar:

> **`01-foundations/global-styles/head-meta-tags.html`** — sección `TEMAS`, un bloque `{% if tema_general_mail_general == '...' %} ... {% endif %}` con una rama por tema.

No hay archivos CSS separados ni carpetas de "skins": el tema completo se resuelve como variables `{% assign %}` dentro de esa única rama, y el resto del HTML (headers, banners, módulos, footer) consume esas variables por nombre.

---

## Los 12 temas

| Grupo | Comportamiento | Temas | Slug (`tema_general_mail_general`) |
|---|---|---|---|
| **Pastel** (7) | Fondos claros y suaves | Beige 100, Beige 150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Gris 100 | `beige100`, `beige150`, `rosa100`, `purpura100`, `celeste100`, `verde100`, `gris100` |
| **Oscuros / invertidos** (3) | Fondo oscuro por defecto | Dark neon, Dark Turbo, Dark Neutro | `darkneon`, `darkturbo`, `darkneutro` |
| **Premium** (2) | Fondo fijo, look editorial | Pro, ProBlack | `pro`, `problack` |

Todas las variables se resuelven leyendo `tema_general_mail_general` una sola vez al principio del `<head>`; de ahí en adelante el resto del mail solo referencia las variables `{{ ... }}`, nunca vuelve a preguntar por el tema.

---

## Variables que define cada tema

Dentro de cada rama del `{% if %}` se asignan estas variables (todas con el sufijo `_mail_general` para evitar choques con otras variables del sistema):

### Fondo, texto y acentos
| Variable | Controla |
|---|---|
| `bg_solid_mail_general` | Fondo general del mail |
| `bg_rgb_mail_general` | Mismo tono que `bg_solid_mail_general`, en `rgba(x,x,x,0.7)`. ◀ NUEVO — variable de definición, todavía no se consume en ningún HTML del sistema |
| `color_texto_mail_general` | Tipografía general |
| `color_acento1_mail_general` | Tono sólido destacado 1 |
| `color_acento2_mail_general` | Tono sólido destacado 2 — **color de los montos de oferta ($, %)** |

### Contenedores y tags
| Variable | Controla |
|---|---|
| `bg_contenedor1_mail_general` | Fondo de bloques de texto, en `rgba()` con su propia opacidad |
| `bg_contenedor2_mail_general` | Fondo de celda/módulo, en `rgba()` con su propia opacidad |
| `bg_tag_fondo_mail_general` | Tag colocado sobre el fondo del módulo, en `rgba()` |
| `bg_tag_contenedor_mail_general` | Tag colocado sobre un contenedor, en `rgba()` |
| `color_tag_tipografia_mail_general` | Color del texto dentro del tag |

### Imágenes
| Variable | Controla |
|---|---|
| `img_overlay_1_mail_general` / `img_overlay_2_mail_general` | Overlays de contenedores de imagen |
| `img_fondo_especial_mail_general` | Fondo de "contenedores especiales" |
| `bg_header_mail_general` | Background del header — hoy solo asignado en los temas pastel |
| `bg_img_mail_general` / `bg_img_size_mail_general` | Background-image y su tamaño para el wrapper general — hoy solo asignado en los temas oscuros/invertidos y premium |

### Banner
| Variable | Controla |
|---|---|
| `bg_bannertono_mail_general` / `bg_bannerimg_mail_general` | Tono e imagen de fondo reservados para el banner por tema (vacíos en la mayoría de los pastel) |
| `bg_banner_tono_mail_general` / `bg_banner_tono_opacity_mail_general` | Tono sólido del banner con su opacidad — temas oscuros/invertidos y premium |
| `banner_gradiente_stop1_mail_general` / `_stop2_` / `_stop3_` / `banner_gradiente_opacity_mail_general` | Los 3 stops de color del gradiente del banner — **solo Dark neon** |

### Adicionales, legales y footer
| Variable | Controla |
|---|---|
| `bg_descuento_mail_general` / `color_descuento_mail_general` | Componente de descuento |
| `bg_creditos_mail_general` / `color_creditos_mail_general` | Componente de créditos |
| `color_textos_legales_mail_general` | Color de la letra legal — asignado en los 12 temas (en la mayoría de pastel coincide con `color_texto_mail_general`, pero es un token propio y puede diferenciarse a futuro) |
| `color_footer_mail_general` | `font_style_look` del footer: `'negro'` en pastel y oscuros/invertidos, `'pro'` en Pro/ProBlack |

### Espaciados internos (banner y deal)
| Variable | Controla |
|---|---|
| `padd_banner_mail_general` | Padding del banner — `'0px 0px'` en los 6 temas pastel, `'15px 10px'` en los 5 temas oscuros/invertidos + premium |
| `padd_deal_mail_general` | Padding del deal — `'5px 0px'` en pastel + oscuros/invertidos (9 temas), `'6px 8px'` en Pro/ProBlack |

### Contenedor de fondo del body — toggle Fondo/Sinfondo
Variables nuevas (no estaban en versiones anteriores de esta guía). Se activan con un toggle por tema:

| Variable | Controla |
|---|---|
| `body_container_background` | Toggle `'Fondo'` (default) / `'Sinfondo'`. Al activar `'Sinfondo'` se sobreescriben las 4 variables siguientes y `img_fondo_especial_mail_general` en los 12 temas |
| `body_container_background_padding` | `10px` en `'Fondo'`, `0px` en `'Sinfondo'` |
| `body_container_background_border` | Borde del contenedor — se anula (`0px solid rgba(255,255,255,0.0)`) en `'Sinfondo'` |
| `body_container_background_radius` | `16px` en `'Fondo'`, `0px` en `'Sinfondo'` |
| `body_container_background_radius-peq` | `8px` en los 12 temas. ⚠ NO se sobreescribe en `'Sinfondo'` — queda en `8px` siempre, a diferencia de `body_container_background_radius` |
| `body_container_background_padding-peq` | `7px` en los 12 temas ◀ NUEVO — hermano de `radius-peq`, usado por el Módulo 3 Columnas. Tampoco se sobreescribe en `'Sinfondo'` |
| `body_container_img_dots` | Imagen decorativa de puntos sobre el contenedor, propia de cada tema |

Usado por los 8 módulos de `04_content-modules/` que envuelven contenido en un contenedor genérico (1/2/3 Columnas, Wrapper, Beneficios, Bullet, Logos, Título).

### Adicionales de body / cupón Pro
| Variable | Controla |
|---|---|
| `coronapro_mail_body` | Ícono de corona junto al precio `$999` en los tags de deal/cupón |
| `bg_solid_generico100_mail_body` / `bg_solid_generico50_mail_body` | Fondo genérico sólido / al 50% de opacidad, para bloques de body |
| `icon_link_generico_mail_body` | Ícono de link genérico usado en contenido |

---

## Reglas y particularidades

**Temas invertidos (Dark neon / Dark Turbo / Dark Neutro):** su fondo por defecto es oscuro (`#040404`). No dependen de `bg_solid_mail_general` para el fondo del wrapper general, sino de `bg_img_mail_general` + `bg_img_size_mail_general`.

**Temas premium (Pro / ProBlack):** el fondo es fijo — Pro usa `#2A2B2B`, ProBlack usa `#ECEFF3` —, así que la legibilidad la dan los contenedores. En Pro, `color_acento2_mail_general` es gris (no rojo) y las variables de descuento/créditos usan tonos dorados en vez del amarillo/verde estándar.

**Tags:** el color del tag depende de la superficie real donde se apoya (fondo vs. contenedor), no del nombre del contenedor. `color_tag_tipografia_mail_general` está definido en los 12 temas para que el texto del tag siempre sea legible sobre su propio fondo.

**Gris 100:** séptimo tema pastel, pensado como comunicación neutra — la vía media entre los pasteles de color (Beige, Rosa, Púrpura, Celeste, Verde) y los premium (Pro, ProBlack). Sin dorado; su acento 1 es gris (`#7D8188`). Las imágenes (`img_overlay_1/2`, `img_fondo_especial`, etc.) reutilizan las mismas URLs del tema ProBlack — todavía no tiene asset propio.

**Verde 100:** `color_acento1_mail_general` es el único acento que cambia entre distintos temas pastel de forma marcada (verde), y su tag sobre contenedor (`bg_tag_contenedor_mail_general`) es sólido y oscuro.

**Rosa 100:** `color_acento1_mail_general` (`#B451C0`) es un tono de acento/gradiente — **no** es el color de los montos de oferta. Esas ofertas siempre usan `color_acento2_mail_general`.

**Dark neon:** es el único tema con gradiente de banner real (`banner_gradiente_stop1/2/3_mail_general`). Los demás oscuros/invertidos usan solo un tono sólido de banner (`bg_banner_tono_mail_general`).

**Imágenes de overlay (`img_overlay_1/2`, `img_fondo_especial`):** no cambian entre modos claro/oscuro dentro de un mismo tema; conservan su tono.

---

## Cómo se relaciona con headers y footer

- **Headers** (`02-components/01_headers/`) se eligen por **marca**, no por tema: el mismo tema (`beige100`, `pro`, etc.) puede combinarse con cualquiera de los 10 headers de marca. Cada header sí tiene sus propias variantes de fondo claro/oscuro (`centrado-claro`, `centrado-oscuro`, `columnas-claro`, `columnas-oscuro`), independientes de `tema_general_mail_general`.
- **Footer** (`02-components/06_footer/footer.html`) no elige su propio estilo: toma `font_style_look` directamente de `{{color_footer_mail_general}}`, la variable que cada tema ya definió. No hay que setear el estilo del footer manualmente por tema.

---

## Estado actual / pendientes

- `bg_header_mail_general` (fondo del header) y `bg_img_mail_general` / `bg_img_size_mail_general` (fondo del wrapper general) hoy se asignan en grupos de temas distintos — pastel tiene uno, oscuros/premium tienen el otro. Falta unificar ambos para que los 12 temas definan ambas variables.
- `bg_rgb_mail_general` se agregó en los 12 temas pero todavía no se consume en ningún componente del HTML — queda listo para el día que algún módulo necesite transparencia sobre `bg_solid_mail_general`.
- El repositorio ya no tiene un archivo de "esqueleto" propio (`opening.html`/`closing.html`) que abra/cierre el `<body>` y el wrapper general — quien ensambla el mail debe aplicar `bg_solid_mail_general` (y las demás variables de fondo) directamente donde corresponda.
- El resto de los componentes (`02_banners/`, `04_content-modules/`, `04_content-modules/coupons/`, `05_closing/`) también tienen comentarios internos con lógica condicional propia por tema; migrarlos a leer directamente las variables de esta guía es un trabajo pendiente, componente por componente.
- `06-examples/template_maestro_original.html` sí ya consume estas variables (`{{bg_solid_mail_general}}`, etc.) en el wrapper general — es la referencia de a dónde debe llegar el resto del sistema.

---

## Referencias cruzadas

- Para entender cómo se arma un mail completo: ver `05-docs/COMO-ARMAR-UN-MAIL.md`
- Para entender cada brick individualmente: ver `05-docs/USO-DE-CADA-PARTE.md`
- Para ver la implementación real: ver `01-foundations/global-styles/head-meta-tags.html` (sección `TEMAS`)
