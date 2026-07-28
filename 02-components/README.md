# 03 · Components

> Los bricks de LEGO. Cada archivo es una pieza independiente.

Esta es la carpeta más importante del repositorio. Aquí viven todos los bloques visuales que se combinan para armar un mail. Cada subcarpeta agrupa un tipo de pieza.

## Subcarpetas

### `headers/` — La identidad del remitente

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

### `banners/` — La cabecera visual del mail

2 formatos. **Se usa solo UNO por mail.**

| Archivo | Cuándo se usa |
|---------|---------------|
| `big-banner-horizontal.html` | Mails con módulos de contenido en el body además de cierre y CTA |
| `big-banner-vertical.html` | Mails que solo tienen CTA y cierre, o banners con logos |

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema.

#### `banner_atoms/` — Piezas internas del banner

| Archivo | Descripción |
|---------|-------------|
| `modulo_tags.html` | Tag/etiqueta que se muestra sobre el banner |
| `modulo_img_altofijo.html` | Columna de imagen de alto fijo (banner horizontal) |
| `modulo_img_variable.html` | Franja de imagen de alto variable (banner vertical) |
| `modulo_creditos.html` | Texto vivo principal (créditos/cifra), usa las clases `bnr-*` |
| `modulo_texto_secundario.html` | Línea secundaria de texto vivo — contenido provisional, pendiente de definir |
| `modulo_texto_complementario.html` | Texto complementario del banner — contenido provisional, pendiente de definir |

El tamaño de las clases `bnr-*` usadas en `modulo_creditos.html` y `modulo_texto_secundario.html` depende de si el banner que las envuelve está marcado con `id="BANNER_HORIZONTAL"` o `id="BANNER_VERTICAL"` (ver `01-foundations/global-styles/global-styles.html`).

### `ctas/` — El botón de acción

| Archivo | Descripción |
|---------|-------------|
| `cta-template.html` | Bloque Liquid del CTA con sus variables (`text_cta`, `deeplink_cta`, `style_Look`) |

Un mail puede tener varios CTAs. Se insertan a lo largo del body según el orden de la fuente.

### `deals/` — Promociones de productos

| Archivo | Descripción |
|---------|-------------|
| `deal-large.html` | Deal grande (formato horizontal con imagen prominente) |
| `deal-small.html` | Deal small (formato compacto) |

**Máximo 4 deals por mail.** Si hay más, se sugiere convertir algunos a módulos de contenido.

### `coupons/` — Módulo de cupones · NUEVO

| Archivo | Descripción |
|---------|-------------|
| `cupones-modulo.html` | Tabla completa con 2 celdas (cupón title + cupón normal, o 2 cupones normales) |

**Reglas importantes:**
- Los cupones siempre vienen en **pares**. Por cada 2 cupones se inserta la tabla completa.
- Cuando hay cantidad impar de cupones, se usa la celda **Cupón Title** (`role="title"`) en lugar del segundo cupón. Esa celda lleva ícono + título y reemplaza a un cupón normal.
- Cada cupón puede tener: imagen top, tag (día/horario), vertical, value prop (mandatorio), complemento (opcional), y legal (opcional).
- El value prop usa color `#DAA868` para los temas Pro/ProBlack y `{{color_acento1_mail_general}}` (o el destacado del tema) para el resto.
- Los legales van en un `<tr>` separado debajo de la fila de cupones.

### `benefits/` — Módulo de beneficios · NUEVO

| Archivo | Descripción |
|---------|-------------|
| `modulo-beneficios.html` | Card con dos columnas: imagen a la izquierda + ícono/subtítulo/texto a la derecha |

**Reglas importantes:**
- Puede haber **varios módulos de beneficios seguidos**. Por cada beneficio se inserta una tabla nueva.
- La card tiene fondo `#202020` con un background-image decorativo encima.
- Contiene tres componentes que se pueden omitir individualmente: imagen del beneficio, ícono, subtítulo, y texto descriptivo.

### `content-modules/` — Los bloques combinables del cuerpo

Aquí viven los bricks más versátiles. Se combinan libremente según las necesidades del mail.

| Archivo | Descripción |
|---------|-------------|
| `modulo-titulo.html` | Único módulo que se usa SIN contenedor. Solo título destacado. |
| `modulo-3-columnas.html` | Tres columnas con imagen + texto |
| `modulo-2-columnas.html` | Dos columnas con imagen + subtítulo + texto. Incluye versión escritorio y mobile (con `mobile_hide` y `desktop_hide`) |
| `modulo-logos.html` | Grid de logos en bloques de 3, 4 o 6 |
| `modulo-contenido.html` | El más versátil: imagen + componentes (bullet logo, bullet icono, bullet numerado) |

#### Componentes internos del `modulo-contenido`

Dentro de `modulo-contenido.html` viven sub-piezas que se identifican con `role="componente"`:
- **BULLET LOGO** — Logo + subtítulo + texto al lado
- **BULLET ICONO** — Ícono pequeño + subtítulo + texto
- **BULLET NUMERADO** — Número grande + subtítulo + texto

Estos componentes están dentro del archivo `modulo-contenido.html` para mantener su contexto. Se pueden combinar libremente dentro del módulo, separados por `<div class="separador-M">`.

### `closing/` — La imagen de cierre

| Archivo | Descripción |
|---------|-------------|
| `cierre.html` | Tabla de imagen de cierre. Se OMITE si el tema es Pro o ProBlack, o si la fuente dice "sin cierre". |

Las URLs de las imágenes de cierre dependen de la marca del mail. Se eligen desde la base de datos de assets.

### `footer/` — El pie del mail

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
