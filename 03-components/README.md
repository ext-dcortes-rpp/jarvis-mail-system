# 03 · Components

> Los bricks de LEGO. Cada archivo es una pieza independiente.

Esta es la carpeta más importante del repositorio. Aquí viven todos los bloques visuales que se combinan para armar un mail. Cada subcarpeta agrupa un tipo de pieza.

## Subcarpetas

### `headers/` — La identidad del remitente

6 variantes de header, una por marca:

| Archivo | Cuándo se usa |
|---------|---------------|
| `rappi.html` | Logo Rappi (la marca general) |
| `rappi-travel.html` | Mails de RappiTravel |
| `rappi-turbo.html` | Mails de RappiTurbo |
| `rappi-turbo-rest.html` | Mails de RappiTurbo Restaurantes |
| `rappi-pro-black.html` | Mails de RappiPro Black (KV oscuro) |
| `rappi-pro.html` | Mails de RappiPro (KV claro) |

**Solo se usa UNO por mail.** El archivo `_header-wrapper.html` es la envolvente común a todos.

Cada header soporta tres modos según la fuente: sin cobranding (solo logo), con cobranding tipo "Tag", o con cobranding tipo "1:1". Las instrucciones de cuál mostrar están comentadas dentro de cada archivo.

### `banners/` — La cabecera visual del mail

3 formatos. **Se usa solo UNO por mail.**

| Archivo | Cuándo se usa |
|---------|---------------|
| `big-banner-horizontal.html` | Mails con módulos de contenido en el body además de cierre y CTA |
| `big-banner-vertical.html` | Mails que solo tienen CTA y cierre, o banners con logos |
| `banner-editorial.html` | Banner estilo editorial (full image) |

Cada banner contiene piezas internas (TAG, CONTENEDOR DE TEXTOS, LOGO, TEXTO DE REFUERZO) cuyas reglas de inclusión/omisión están en los comentarios internos.

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
- El value prop usa color `#DAA868` para KV Pro/ProBlack y el color destacado por defecto para los demás KVs.
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
| `cierre.html` | Tabla de imagen de cierre. Se OMITE si KV es Pro, ProBlack, o si la fuente dice "sin cierre". |

Las URLs de las imágenes de cierre dependen del KV (Genérico, Turbo, Neutro). Se eligen desde la base de datos de assets.

### `footer/` — El pie del mail

| Archivo | Descripción |
|---------|-------------|
| `footer.html` | Bloque Liquid del footer con sus variables (`cond`, `font_style_look`, `show_legal_*`) |

**El footer SIEMPRE se conserva completo.** Nunca se omite. Solo cambian los valores de las variables Liquid según la fuente.

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
