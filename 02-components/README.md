# 02 · Components

> Los bricks de LEGO. Cada archivo es una pieza independiente.

Esta es la carpeta más importante del repositorio. Aquí viven todos los bloques visuales que se combinan para armar un mail. Cada subcarpeta agrupa un tipo de pieza.

Las subcarpetas de abajo (`01_headers`, `02_banners`...) son la estructura operativa actual. En paralelo, el sistema también se piensa en términos de Atomic Design (átomos → moléculas → organismos) — ambas vistas describen las mismas piezas, solo que agrupadas distinto.

## Atomic Design (resumen)

Ver **`05-docs/ATOMIC-DESIGN.md`** para el detalle completo (tablas, mockups simulados, snippets HTML y hallazgos de auditoría) — este es solo un resumen de las 3 páginas del Figma del sistema (`Doc-DS-Mails`).

- **Átomos** — la pieza mínima sin contenedor propio: spacers verticales (`.separador` / `-M` / `-S` / `molecula-separador`), modificadores de texto (bold, tachado, vertical, interletrado...), el logo según los 10 contextos donde aparece, la imagen según los 12 tamaños donde aparece, tags/badges (genéricos vs. "$999"), y los 8 estilos de CTA (`style_Look`).
- **Moléculas** — átomos combinados con reglas propias, todavía sin contexto de página: el header (logo+cobranding, 2 estructuras × 4 tamaños), las 8 moléculas del banner (`banner_moleculas/`), las moléculas de contenido (`content_moleculas/`: bullets, tags/pastillas, combos exclusivos de Deals, link interno, franja de logos), y la tabla de cierre.
- **Organismos** — el bloque completo y autocontenido (`table role="module"`): Big Banner (vertical/horizontal), Módulo Título, Deals en Columnas, Módulo Cupones, Módulo Bullet, Módulo Beneficios, Módulo 1 Columna, Módulo Dos Columnas, Módulo Logos, Módulo 3 Columnas, y el Footer (General / Sin Amor / RTS, con tabla de variables por país cada uno).

## Subcarpetas

### `01_headers/` — La identidad del remitente

10 subcarpetas, una por marca. **Solo se usa UNA marca por mail**, y de esa marca se elige exactamente 1 de sus 4 archivos según fondo (claro/oscuro) y disposición (centrado/columnas):

| Carpeta | Marca |
|---------|-------|
| `rappi/` | Rappi (la marca general) |
| `rappi-travel/` | RappiTravel |
| `soyrappi/` | SoyRappi |
| `rappi-turbo/` | RappiTurbo |
| `rappi-turbo-rest/` | RappiTurbo Restaurantes |
| `rappi-pro/` | RappiPro |
| `rappi-pro-black/` | RappiPro Black |
| `rappi-defensoria/` | Defensoría |
| `rappi-entregador/` | RappiEntregador |
| `contenido-aliado/` | Contenido aliado |

Dentro de cada carpeta, los 4 archivos:

| Archivo | Fondo | Disposición |
|---------|-------|--------------|
| `centrado-claro.html` | Claro | Logo · divider · cobranding, centrado en una fila |
| `centrado-oscuro.html` | Oscuro | Logo · divider · cobranding, centrado en una fila |
| `columnas-claro.html` | Claro | Logo a la izquierda, cobranding a la derecha, sin divider |
| `columnas-oscuro.html` | Oscuro | Logo a la izquierda, cobranding a la derecha, sin divider |

Cada archivo contiene únicamente el `<tr>` del header (con su comentario identificador); el archivo `_header-wrapper.html` es la envolvente `<table>`/`<tbody>` común a todos y se conserva sin cambios.

**La elección de marca es independiente del tema del mail** (`tema_general_mail_general` en `05-docs/GUIA-DE-TEMAS.md`): cualquiera de los 10 headers puede combinarse con cualquiera de los 11 temas.

### `02_banners/` — La cabecera visual del mail

2 formatos. **Se usa solo UNO por mail.**

| Archivo | Cuándo se usa |
|---------|---------------|
| `big-banner-horizontal.html` | Mails con módulos de contenido en el body además de cierre y CTA |
| `big-banner-vertical.html` | Mails que solo tienen CTA y cierre, o banners con logos |

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema.

#### `banner_moleculas/` — Piezas internas del banner

| Archivo | Descripción |
|---------|-------------|
**MODULOS** — piezas fijas que se conservan tal cual dentro de `big-banner-*.html` (no son MOLECULAS, no se combinan libremente):

| Archivo | Descripción |
|---------|-------------|
| `modulo_tags_horizontal.html` | Tag/etiqueta que se muestra sobre el banner horizontal (alineado a la derecha, `float: right`) |
| `modulo_tags_vertical.html` | Igual, centrado (`margin: 0 auto`) para el banner vertical |
| `modulo_img_altofijo_horizontal.html` | Columna de imagen de alto fijo (`altobanner1`) para el banner horizontal |
| `modulo_img_altofijo_vertical.html` | Igual, con la clase/alto (`altobanner2`) del banner vertical |
| `modulo_img_automatica_horizontal.html` | Celda alternativa a `modulo_img_altofijo_horizontal.html` en el banner horizontal — **solo se usa una de las dos**. No confundir con `molecula_img_automatica_*` (son piezas distintas) |

**MOLECULAS** — viven dentro de `MODULO MOLECULAS` (la tabla que se conserva en `big-banner-*.html`) y se combinan libremente. Cada una tiene su par horizontal/vertical:

| Archivo | Descripción |
|---------|-------------|
| `molecula_promo_horizontal.html` / `molecula_promo_vertical.html` | Módulo de promo ("Ahora" + cifra), tamaños inline + tema (`bg_descuento_mail_general`, `color_descuento_mail_general`) |
| `molecula_creditos_horizontal.html` / `molecula_creditos_vertical.html` | Texto vivo de créditos ("$XXX" + "DE REINTEGRO"), usa `bnr-*` + tema (`bg_creditos_mail_general`, `color_creditos_mail_general`) |
| `molecula_textoxl_horizontal.html` / `molecula_textoxl_vertical.html` | Texto vivo XL adicional (`banner_copy_modulo_textoxl`), mismo comportamiento de tamaño que `molecula_promo_*` |
| `molecula_textom_horizontal.html` / `molecula_textom_vertical.html` | Texto vivo `.bnr-md` (`banner_copy_modulo_textom`), tamaño fijo inline (no depende del largo) |
| `molecula_img_automatica_horizontal.html` / `molecula_img_automatica_vertical.html` | Imagen automática (`banner_img_modulo_auto_ancho`) — pieza distinta a `modulo_img_automatica_horizontal.html` |
| `molecula_cta_interno_horizontal.html` (`cta_alineado: 'left'`) / `molecula_cta_interno_vertical.html` (`cta_alineado: 'center'`) | CTA embebido dentro del banner |
| `molecula_texto_complementario_horizontal.html` / `molecula_texto_complementario_vertical.html` | Texto de body (`<h4>`) que acompaña al texto destacado del banner — contenido pendiente de insertar manualmente en cada uno, es distinto por orientación |

El tamaño de las clases `bnr-*` usadas en las moléculas de créditos, promo y texto XL depende de si el banner que las envuelve está marcado con `id="BANNER_HORIZONTAL"` o `id="BANNER_VERTICAL"` (ver `01-foundations/global-styles/global-styles.html`). Los tamaños de escritorio de estas clases se aplican inline (vía las variables Liquid de largo de texto en `01-foundations/global-styles/head-meta-tags.html`); las clases `bnr-*` en el `<head>` solo cubren el override de mobile.

### `03_ctas/` — El botón de acción

| Archivo | Descripción |
|---------|-------------|
| `cta-template.html` | El botón en sí (HTML + Liquid), vive como content block de Braze (`content_blocks.${CTA-template}`) |
| `cta-llamado.html` | Lo que se inserta en el cuerpo del mail para instanciar un CTA: setea `cta_alineado`, `text_cta`, `deeplink_cta`, `style_Look` y llama `{{content_blocks.${CTA-template}}}` |

Un mail puede tener varios CTAs. Se insertan a lo largo del body según el orden de la fuente.

### `04_content-modules/` — Los bloques combinables del cuerpo

Aquí viven los bricks más versátiles. Se combinan libremente según las necesidades del mail.

| Archivo | Descripción |
|---------|-------------|
| `title/modulo-titulo.html` | Único módulo que se usa SIN contenedor. Solo título destacado. |
| `3columnas/modulo-3-columnas.html` | Tres columnas con imagen + texto |
| `2columnas/modulo-2-columnas.html` | Dos columnas con imagen + subtítulo + texto. Incluye versión escritorio y mobile (con `mobile_hide` y `desktop_hide`) |
| `logos/modulo-logos.html` | Módulo completo (título + subtítulo + grid de logos). La grid interna se reemplaza por una de las tres de abajo según cuántos logos traiga la fuente |
| `1columna/modulo-1columna.html` | El más versátil: imagen + componentes (bullet logo, bullet icono, bullet numerado) |
| `bullet/modulo_bullet.html` | Módulo con contenedor que envuelve una sola molécula bullet (ícono + subtítulo + texto) |

#### `04_content-modules/logos/` — Grillas por cantidad de logos

| Archivo | Descripción |
|---------|-------------|
| `grilla3logos.html` | 1 fila de 3 celdas (`logo1`/`logo2`/`logo3`) |
| `grilla4logos.html` | Grid 2×2 (`thead` con 2 celdas + `tbody` con 2 celdas) |
| `grilla6logos.html` | 2 filas de 3 celdas (`logo1`...`logo6`) |

`modulo-logos.html` trae dos tablas completas (escritorio con `class="mobile_hide"` y mobile con `class="desktop_hide"`, mismo patrón que `modulo-2-columnas.html`). En cada una hay un placeholder que marca dónde insertar la grilla — **se inserta solo una** de las tres de arriba (la misma en ambas tablas), según la cantidad de logos que traiga la fuente. El título/subtítulo se replica igual en ambas tablas.

`_contenidos_wrapper.html` es la envolvente `<div>`/`<table>`/`<tbody>` común a la zona de CONTENIDOS del mail (donde se insertan los módulos elegidos, separados por `<div class="separador">`); se conserva sin cambios, igual que `_header-wrapper.html` en `01_headers/`.

#### Componentes internos de `1columna/modulo-1columna.html`

`modulo-1columna.html` ya no embebe las moléculas directamente: es un contenedor genérico (`role="contenedorgeneral"` + `divcomponentes`) con el placeholder `<!-- aqui las moleculas-->` donde se insertan las piezas de `content_moleculas/` que la fuente pida (bullets, tags, etc.), separadas por `<div class="separador-M">`. Puede llevar además una imagen automática opcional debajo.

#### `04_content-modules/content_moleculas/`

Moléculas de contenido extraídas de `06-examples/template_maestro_original.html` (marcadas ahí como `<!-- MOLECULA ... -->`). Cada una es una pieza suelta, sin el contexto de un módulo contenedor:

| Archivo | Descripción |
|---------|-------------|
| `molecula_tag_promo.html` | Badge de monto destacado ("$999") con fondo/color de descuento |
| `molecula_tag_verde.html` | Igual que `molecula_tag_promo`, con fondo/color de créditos |
| `molecula_tag_basico.html` | Igual que `molecula_tag_promo`/`molecula_tag_verde`, con fondo/color genérico (`bg_solid_generico100_mail_body`) |
| `molecula_separador_s.html` | Línea decorativa corta (50px) bajo un título, color acento 1 — no confundir con la utilidad de espaciado `.separador-S` |
| `molecula_icono.html` | Los 4 tamaños de ícono suelto (S 15px, M 25px, L 40px, XL 60px) — cada uno es un `<img>` independiente, se usa el que corresponda |
| `molecula_tag_icono.html` | Pill con ícono + texto pequeño (ícono y texto ocultables/cambiables) |
| `molecula_texto_pastilla.html` | Tabla de 2 celdas: una pastilla (ej. día) + un texto plano al lado, orden intercambiable (pastilla a la izquierda o a la derecha) |
| `molecula_link_interno.html` | Link circular con ícono + texto ("Clic aquí") |
| `molecula_bullet_numerado.html` | Número + subtítulo + texto, separados por `.separador-S` |
| `molecula_bullet_icono_s.html` | Bullet con ícono de 15px + subtítulo + texto |
| `molecula_bullet_icono_m.html` | Bullet con ícono de 25px + subtítulo + texto |
| `molecula_bullet_icono_l.html` | Bullet con imagen de 60px + subtítulo + texto |
| `molecula_franja_logos.html` | Fila de logos circulares (se agregan/quitan `<td>` para más o menos logos) |
| `molecula_img_automatica.html` | Imagen de ancho variable, opcionalmente clickeable |
| `modificadores-texto.html` | No es una molécula (por eso no lleva el prefijo `molecula_`) — es la referencia de modificadores de texto (tamaño h1-h5/.legal, subtono 1/2, bold, italic, tachado, subrayado, superíndice) que vive justo antes de las moléculas en el HTML maestro |

#### `04_content-modules/deals/`

`deal-large.html` y `deal-small.html` ya no se usan en el sistema. Se conservan en la carpeta renombrados como `deal-large.backup.html` / `deal-small.backup.html` para no perder el trabajo, pero no están enlazados desde ningún template ni desde el visualizador.

El archivo activo es **`deal_columnas.html`**: deals de a pares en una grilla de 2 celdas (50/50), con imagen + texto (título, descuento, rating, tags, CTA) por celda. Cuando la cantidad es impar, se elimina todo el contenido de la celda derecha (la celda queda vacía, la grilla no se rompe). Ver `05-docs/ATOMIC-DESIGN.md`, Organismos 6.4, para el detalle completo.

#### `04_content-modules/coupons/` — Módulo de cupones

| Archivo | Descripción |
|---------|-------------|
| `cupones-modulo.html` | Tabla completa con 2 celdas de cupón normal (siempre de a pares) |
| `celda_cupon_titulo.html` | Celda de título suelta (`role="titulocupon"`) — reemplaza a la **celda 1** cuando se necesita un título en vez de un cupón; la celda 2 siempre queda como cupón normal |

**Reglas importantes:**
- Los cupones siempre vienen en **pares**. Por cada 2 cupones se inserta la tabla completa.
- La celda 1 puede convertirse en celda de título (`celda_cupon_titulo.html`) — es una decisión de contenido, no una regla automática de balanceo par/impar. Esa celda tiene su propia estructura: línea punteada arriba y abajo (ninguna removible), tag con ícono, y un H1 título grande — **no** es el mismo patrón que `title/modulo-titulo.html`.
- Cada celda de cupón normal tiene: imagen de producto (reemplazable), línea punteada fija (no removible), pastilla + texto (cada uno apagable), MARKDOWN (H1, texto grande), separador, y bullet (ícono removible + texto).
- El fondo de la celda **siempre está activo** (no se puede desactivar) y el alineado es fijo — solo se pueden modificar los pesos de texto.
- Los legales van en una fila separada debajo de la fila de cupones, desactivada por defecto.

#### `04_content-modules/benefits/` — Módulo de beneficios · NUEVO

| Archivo | Descripción |
|---------|-------------|
| `modulo-beneficios.html` | Card con dos columnas: imagen a la izquierda + ícono/subtítulo/texto a la derecha |

**Reglas importantes:**
- Puede haber **varios módulos de beneficios seguidos**. Por cada beneficio se inserta una tabla nueva.
- La card tiene fondo `#202020` con un background-image decorativo encima.
- Contiene tres componentes que se pueden omitir individualmente: imagen del beneficio, ícono, subtítulo, y texto descriptivo.

### `05_closing/` — La imagen de cierre

| Archivo | Descripción |
|---------|-------------|
| `cierre.html` | Tabla de imagen de cierre. Se OMITE si el tema es Pro o ProBlack, o si la fuente dice "sin cierre". |

Las URLs de las imágenes de cierre dependen de la marca del mail. Se eligen desde la base de datos de assets.

### `06_footer/` — El pie del mail

| Archivo | Descripción |
|---------|-------------|
| `footer.html` | Bloque Liquid orquestador: setea `cond`, `font_style_look`, `show_legal_tyc`, `show_legal_turbo`, `show_legal_liquor`, e inserta el content block de legales correspondiente |
| `footer_general.html` | Contenido del content block `FOOTER_q1_2024_legales` (variante general) |
| `footer_sinamor.html` | Contenido del content block `FOOTER_VERSION2` (variante "sin amor") |
| `footer_rts.html` | Contenido del content block `FOOTER_RTS_q3_2024_legales` (variante RTS) |

**El footer SIEMPRE se conserva completo.** Nunca se omite. `font_style_look` ya no se elige a mano: toma el valor de `{{color_footer_mail_general}}`, la variable que el tema activo definió en `05-docs/GUIA-DE-TEMAS.md` (`'negro'` en la mayoría de los temas, `'pro'` en Pro/ProBlack). Lo único que cambia por fuente es cuál de las 3 variantes de legales (`footer_general` / `footer_sinamor` / `footer_rts`) se referencia y los toggles `show_legal_*`.

## Reglas comunes a todos los componentes

1. **No se modifica la estructura HTML interna.** Solo se cambian las URLs de imágenes y los textos.
2. **No se cambian estilos inline.** El padding, margin, width, height, border-radius son fijos.
3. **Los comentarios INICIO/FIN se conservan SIEMPRE.** Son la firma del componente.
4. **Las instrucciones internas (los `<!-- ... -->` con reglas) también se conservan.** Le dicen al siguiente diseñador qué hacer.

## Cómo proponer un nuevo componente

Si necesitas un brick que no existe, no lo agregues directo. El proceso es:

1. Abre un issue en GitHub describiendo el caso de uso.
2. Sube el diseño en Figma (file `MAILS_NEON_DESIGN_SYSTEM`).
3. Se discute en equipo si amerita ser un componente del sistema o si es algo que se resuelve combinando los existentes.
4. Si se aprueba, se crea el archivo, se documenta, y se actualiza la guía del Gem de Gemini.
