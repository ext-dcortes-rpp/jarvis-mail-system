# 02 · Components

> Los bricks de LEGO. Cada archivo es una pieza independiente.

Esta es la carpeta más importante del repositorio. Aquí viven todos los bloques visuales que se combinan para armar un mail. Cada subcarpeta agrupa un tipo de pieza.

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

`modulo_texto_complementario.html` (sin sufijo) sigue siendo el único archivo para el texto de body (`<h4>`) que acompaña al texto destacado del banner. Su propio comentario interno marca como pendiente dividirlo en `modulo_texto_complemento_horizontal.html` / `_vertical.html`, pero esa versión todavía no existe en el sistema.

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
| `logos/modulo-logos.html` | Grid de logos en bloques de 3, 4 o 6 |
| `1columna/modulo-1columna.html` | El más versátil: imagen + componentes (bullet logo, bullet icono, bullet numerado) |

`_contenidos_wrapper.html` es la envolvente `<div>`/`<table>`/`<tbody>` común a la zona de CONTENIDOS del mail (donde se insertan los módulos elegidos, separados por `<div class="separador">`); se conserva sin cambios, igual que `_header-wrapper.html` en `01_headers/`.

#### Componentes internos de `1columna/modulo-1columna.html`

Dentro de `modulo-1columna.html` viven sub-piezas que se identifican con `role="componente"`:
- **BULLET LOGO** — Logo + subtítulo + texto al lado
- **BULLET ICONO** — Ícono pequeño + subtítulo + texto
- **BULLET NUMERADO** — Número grande + subtítulo + texto

Estos componentes están dentro del archivo `modulo-1columna.html` para mantener su contexto. Se pueden combinar libremente dentro del módulo, separados por `<div class="separador-M">`.

#### `04_content-modules/deals/`

`deal-large.html` y `deal-small.html` ya no se usan en el sistema. Se conservan en la carpeta renombrados como `deal-large.backup.html` / `deal-small.backup.html` para no perder el trabajo, pero no están enlazados desde ningún template ni desde el visualizador.

⚠️ **Sin documentar:** la carpeta también tiene `deal_columnas.html` (tabla de 2 celdas, deal a la izquierda y a la derecha) — no está descrito en ningún doc todavía ni enlazado desde el visualizador. Pendiente confirmar con el equipo si es el reemplazo activo de los backups o un work in progress.

#### `04_content-modules/coupons/` — Módulo de cupones · NUEVO

| Archivo | Descripción |
|---------|-------------|
| `cupones-modulo.html` | Tabla completa con 2 celdas (cupón title + cupón normal, o 2 cupones normales) |

**Reglas importantes:**
- Los cupones siempre vienen en **pares**. Por cada 2 cupones se inserta la tabla completa.
- Cuando hay cantidad impar de cupones, se usa la celda **Cupón Title** (`role="title"`) en lugar del segundo cupón. Esa celda lleva ícono + título y reemplaza a un cupón normal.
- Cada cupón puede tener: imagen top, tag (día/horario), vertical, value prop (mandatorio), complemento (opcional), y legal (opcional).
- El value prop usa color `#DAA868` para los temas Pro/ProBlack y `{{color_acento1_mail_general}}` (o el destacado del tema) para el resto.
- Los legales van en un `<tr>` separado debajo de la fila de cupones.

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
