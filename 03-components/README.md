# 03 · Components

> Los bricks de LEGO. Cada archivo es una pieza independiente.

Esta es la carpeta más importante del repositorio. Aquí viven todos los bloques visuales que se combinan para armar un mail. Cada subcarpeta agrupa un tipo de pieza.

## Subcarpetas

### `headers/` — La identidad del remitente

6 variantes de header, una por marca. **Solo se usa UNO por mail.**

| Archivo | Cuándo usarlo |
|---------|--------------|
| `rappi.html` | Mails de la marca Rappi en general |
| `rappi-travel.html` | Mails de RappiTravel |
| `rappi-turbo.html` | Mails de RappiTurbo |
| `rappi-turbo-rest.html` | Mails de RappiTurbo Restaurantes |
| `rappi-pro.html` | Mails de RappiPro (fondo claro) |
| `rappi-pro-black.html` | Mails de RappiPro Black (fondo oscuro) |

El archivo `_header-wrapper.html` es la envoltura común que se pega alrededor del header elegido. Todos los headers van dentro de ella.

Cada header soporta tres modos:
- **Sin cobranding** — solo el logo de la marca
- **Con cobranding tipo "Tag"** — el logo de la marca + una imagen tipo etiqueta de un partner
- **Con cobranding tipo "1:1"** — el logo de la marca + el logo cuadrado de un partner

Las instrucciones de qué mostrar en cada caso están escritas como comentarios dentro de cada archivo.

---

### `banners/` — La imagen principal del mail

3 formatos disponibles. **Solo se usa UNO por mail.**

| Archivo | Cuándo usarlo |
|---------|--------------|
| `big-banner-horizontal.html` | Mails que tienen módulos de contenido en el cuerpo (además del CTA y el cierre) |
| `big-banner-vertical.html` | Mails que solo tienen CTA y cierre, o banners con logos |
| `banner-editorial.html` | Imagen a todo el ancho, sin bloques de texto encima |

Dentro de cada banner hay sub-piezas que puedes conservar o eliminar según la fuente:
- **TAG** — etiqueta pequeña encima del banner (opcional)
- **BLOQUE DE TEXTOS** — título principal, subtítulo, textos de apoyo
- **LOGO** — logo dentro del banner (opcional)
- **TEXTO DE REFUERZO** — texto pequeño de apoyo (opcional)

Las reglas de cuándo conservar o eliminar cada sub-pieza están escritas como comentarios dentro del archivo.

---

### `ctas/` — El botón de acción

| Archivo | Descripción |
|---------|-------------|
| `cta-template.html` | El bloque del botón de acción. Las variables (texto del botón, link de destino, estilo visual) se completan según la fuente. |

Un mail puede tener varios CTAs. Se pegan en el cuerpo del mail según el orden de la fuente.

---

### `deals/` — Promociones de productos

| Archivo | Descripción |
|---------|-------------|
| `deal-large.html` | Deal grande: imagen prominente con texto a la derecha |
| `deal-small.html` | Deal pequeño: formato compacto |

**Máximo 4 deals por mail.** Si hay más, se sugiere convertir algunos a módulos de contenido.

---

### `content-modules/` — Los bloques combinables del cuerpo

Los bricks más versátiles. Se combinan libremente según las necesidades del mail.

| Archivo | Descripción |
|---------|-------------|
| `modulo-titulo.html` | Solo un título destacado. Es el único módulo que va SIN envoltura contenedora. |
| `modulo-3-columnas.html` | Tres columnas: imagen arriba + texto abajo (en celular se apilan verticalmente) |
| `modulo-2-columnas.html` | Dos columnas: imagen + subtítulo + texto |
| `modulo-logos.html` | Grilla de logos: se puede armar en grupos de 3, 4 o 6 logos |
| `modulo-contenido.html` | El más versátil: imagen + sub-componentes combinables |

#### Sub-piezas dentro del módulo de contenido

El archivo `modulo-contenido.html` contiene sub-piezas internas que se pueden mezclar:
- **BULLET LOGO** — imagen de logo + texto al lado
- **BULLET ICONO** — ícono pequeño + texto al lado
- **BULLET NUMERADO** — número en círculo + texto al lado
- **IMAGEN FULL** — imagen a todo el ancho del contenedor

Estas sub-piezas están dentro del mismo archivo para mantener su contexto visual.

---

### `closing/` — La imagen de cierre

| Archivo | Descripción |
|---------|-------------|
| `cierre.html` | Imagen de cierre del mail. Se omite en ciertos casos (ver reglas abajo). |

**Cuándo se omite el cierre:**
- Si el tipo de KV es Pro o Pro Black
- Si la fuente dice explícitamente "sin cierre"

En cualquier otro caso, se conserva. La imagen específica depende del tipo de KV (Genérico, Turbo, Neutro) y se elige desde la base de assets.

---

### `footer/` — El pie del mail

| Archivo | Descripción |
|---------|-------------|
| `footer.html` | El pie de mail con legales. Las variables (tipo de legales a mostrar, estilo visual) se completan según la fuente. |

**El footer SIEMPRE se conserva completo.** Nunca se omite. Solo cambian los valores de las variables según lo que indique la fuente del mail.

---

## Reglas comunes a todos los componentes

1. **No se modifica la estructura interna de las piezas.** Solo se cambian las URLs de imágenes y los textos.
2. **No se cambian los tamaños ni espaciados internos.** El padding, los márgenes, el ancho y el alto de cada pieza son fijos por diseño.
3. **Los comentarios de INICIO y FIN se conservan siempre.** Son la firma del componente.
4. **Los comentarios con instrucciones internas también se conservan.** Le dicen al siguiente diseñador qué hacer con esa pieza.

## Cómo proponer un nuevo componente

Si necesitas un bloque que no existe en el sistema, no lo agregues directamente. El proceso es:

1. Describe el caso de uso y súbelo como issue en GitHub.
2. Adjunta el diseño en Figma (archivo `MAILS_NEON_DESIGN_SYSTEM`).
3. El equipo evalúa si amerita ser un componente del sistema o si puede resolverse combinando los existentes.
4. Si se aprueba, se crea el archivo, se documenta aquí y se actualiza el Gem de Gemini.
