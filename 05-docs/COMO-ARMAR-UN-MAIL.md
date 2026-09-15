# Guía: Cómo armar un mail desde cero

Esta guía es para diseñadores y miembros del equipo que quieren entender el flujo completo, sin necesidad de saber programar.

## La metáfora rápida

Imagina una caja de LEGO con dos tipos de cosas:
1. **Los bricks** (`02-components/`)
2. **Las instrucciones** (los comentarios INICIO/FIN dentro de cada archivo + esta guía)

## Los pasos

### Paso 1 — Decide el "tipo de mail"
- **¿Qué tema?** Uno de los 12 (Beige 100/150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Gris 100, Dark neon, Dark Turbo, Dark Neutro, Pro, ProBlack) — ver `GUIA-DE-TEMAS.md`.
- **¿Qué marca de header?** Rappi, Travel, SoyRappi, Turbo, Turbo Rest, Pro, ProBlack, Defensoría, RappiEntregador o Contenido aliado.
- **¿Qué módulos?** Solo banner + CTA, o algo más complejo con deals, cupones, beneficios y módulos de contenido.

### Las tres secciones del mail — léelo antes de todo lo demás

Todo mail tiene **tres secciones**, siempre en este orden. El esqueleto completo, con cada hueco marcado, está en `06-examples/estructura_general.html`.

```
╔═ 1 · HERO ═══════════════════════════════════════╗
║  <a>  ← un solo link para las tres piezas         ║
║   └ <table role="HERO-SECTION"> 600px             ║
║       ├ header            (1 de los 40 archivos)  ║
║       ├ banner            (horizontal O vertical) ║
║       └ imagen full width (opcional)              ║
╚═══════════════════════════════════════════════════╝
╔═ 2 · CONTENTS ═══════════════════════════════════╗
║   <table role="CONTENTS-SECTION"> 600px           ║
║    └ wrapper de contenidos          480px         ║
║        ├ CTA reglamentario   ← obligatorio, 1º    ║
║        ├ <div class="separador">                  ║
║        ├ módulo                                   ║
║        ├ <div class="separador">                  ║
║        └ módulo …                                 ║
╚═══════════════════════════════════════════════════╝
╔═ 3 · FOOTER ═════════════════════════════════════╗
║   fuera de las dos anteriores                     ║
╚═══════════════════════════════════════════════════╝
```

**HERO** es la parte superior: header · banner · imagen full width, en ese orden. **CONTENTS** es el interior y abre con el CTA reglamentario. **FOOTER** queda fuera de las dos.

> El CTA obligatorio **ya no va pegado debajo del banner**: el banner vive dentro del HERO, y el CTA es el primer elemento de CONTENTS.

Cuatro reglas que cambian cómo se insertan las piezas:

1. **El HERO lleva un solo link.** El `<a>` envuelve el HERO completo, así que header, banner e imagen apuntan al mismo destino. Los archivos de banner ya **no** traen `<a>` propio: si ves uno, es un residuo y hay que quitarlo — dos `<a>` anidados no son válidos.
2. **CONTENTS NO va envuelta en un `<a>`.** Aquí cada módulo decide si es clickeable y lleva su propio `<a href="LINKMODULO">`. Es la diferencia de fondo entre las dos secciones.
3. **El padding lateral en mobile lo dan los componentes, no el contenedor.** Se hace con la clase `mobile_paading`, que ya viene aplicada en los headers, en el `<div>` que envuelve cada banner y en el `<td>` del wrapper de contenidos. La imagen full width no la lleva a propósito: debe ocupar los 600px completos.
4. **El footer va fuera del `role="paddedcontainer"`.** Esa ubicación no es casual: si se mete dentro, hereda el ancho y el padding de CONTENTS.

Las dos secciones comparten el mismo `background-image` en su celda, para que la pieza se lea continua de arriba abajo.

### Paso 2 — Agrega un header
De `02-components/01_headers/`, elige la carpeta de marca y dentro de ella el archivo según fondo (claro/oscuro) y disposición (centrado/columnas). Las instrucciones de cobranding (sin / S / M / L / XL) están en los comentarios del archivo.

### Paso 3 — Agrega un banner
De `02-components/02_banners/`, elige `big-banner-horizontal.html` o `big-banner-vertical.html` y pégalo en el hueco del banner dentro del HERO. Las piezas internas (tag, imagen, créditos, textos) están en `02-components/02_banners/banner_moleculas/`. Si el mail lleva imagen a sangre al pie del HERO, agrega después `imagen-full-width.html`.

El banner es **obligatorio** en todo mail — no es un adorno del contenido, es la apertura: debe dejar claro de qué trata el mail, siendo directo sobre el beneficio o contenido que se quiere comunicar. En formato horizontal, el uso de imagen es obligatorio.

**Jerarquías de texto:** dentro de un mismo banner, el tamaño mayor (XL) se usa una sola vez. Los tamaños de banner (`bnr-*`) son exclusivos del banner — no se usan en el body, donde se usan los tamaños `h1` a `h6`.

### Paso 4 — Inserta los bricks del cuerpo
Aquí se decide qué piezas y en qué orden:

- **CTA** → `02-components/03_ctas/cta-llamado.html` (define las variables) + `cta-template.html` (el botón, vía content block)
- **Deals** → `02-components/04_content-modules/deals/deal_columnas.html` (siempre en pares; `deal-large/small.backup.html` ya no se usan). Está diseñado para promociones, pero se puede usar para otro tipo de contenido adaptando los textos y usando las moléculas del módulo para distribuir los textos.
- **Cupones** → `02-components/04_content-modules/coupons/cupones-modulo.html` (siempre en pares)
- **Beneficios** → `02-components/04_content-modules/benefits/modulo-beneficios.html` (uno por beneficio)
- **Módulo título** → `02-components/04_content-modules/title/modulo-titulo.html`
- **Módulo bullet** → `02-components/04_content-modules/bullet/modulo_bullet.html`
- **Módulo 3 columnas** → `02-components/04_content-modules/3columnas/modulo-3-columnas.html`
- **Módulo 2 columnas** → `02-components/04_content-modules/2columnas/modulo-2-columnas.html`
- **Módulo logos** → `02-components/04_content-modules/logos/modulo-logos.html`
- **Módulo 1 columna** → `02-components/04_content-modules/1columna/modulo-1columna.html` (bloques de moléculas + imagen full-width, en el orden que se necesite)

**Cómo elegir un módulo de contenido:** se elige según la cantidad de información que se necesita comunicar y los elementos que cada módulo ya trae para ayudar a jerarquizar esa información — no por preferencia visual.

**Padding y espaciado entre bricks:**

El ancho y el margen lateral los da el **wrapper de contenidos** (480px, con `mobile_paading` en su `<td>`) — no se tocan módulo por módulo. El `role="paddedcontainer"` general va hoy en `padding: 0px`. Cada módulo además tiene su propio padding interno según tenga o no fondo (`body_container_background_padding`: 10px con fondo, 0px sin fondo), para separar el contenido del borde de su contenedor.

**La regla de separadores — tres niveles, tres clases.** Son `<div>` vacíos que solo aportan altura; las clases viven en `global-styles.html`:

| Clase | Alto | Separa... | ¿Obligatorio? |
|---|---|---|---|
| `<div class="separador"></div>` | 16px | dos **MÓDULOS** de contenido | **Sí.** Siempre que insertes un módulo debajo de otro |
| `<div class="separador-M"></div>` | 10px | dos **MOLÉCULAS** dentro de un módulo | Según el módulo |
| `<div class="separador-S"></div>` | 4px | dos **ELEMENTOS** dentro de una molécula | Según la molécula |

El patrón se lee así:

```
[ módulo título ]
<div class="separador"></div>      ← obligatorio entre módulos
[ módulo deals ]
<div class="separador"></div>
[ módulo cupones ]
```

Si quitas una pieza, quita también su separador: quedan huecos dobles.

> ⚠️ **No confundir** `molecula_separador_s.html` con `<div class="separador-S">`. El primero es una **línea decorativa** (`role="molecula-separador"`, un borde de color); el segundo es un **espaciador invisible**. Nombres parecidos, cosas distintas.

### Paso 5 — Agrega el footer
De `02-components/06_footer/footer_general.html`. **El footer SIEMPRE va**, y va **fuera** de HERO y CONTENTS. Solo cambias las variables Liquid según la fuente:

- `cond` → texto de legales adicionales (si lo hay)
- `font_style_look` → el color del footer. **Ojo: no es el tema del mail.** El footer tiene su propia paleta; ver la nota de abajo.
- `firma` → `general` (Pídelo por Rappi) · `turbo` (Pídelo por Rappi Turbo) · `pro` (corona) · vacío (el bigote)
- `show_legal_tyc` / `show_legal_turbo` / `show_legal_liquor` → true/false

> **El footer no usa los tokens del tema.** Su tipografía, el borde superior de los legales y el borde del botón de WhatsApp salen de `font_style_look`, que tiene sus propios valores y no coincide con el `color_texto` del tema en Púrpura, Verde, Gris ni Pro. La tabla completa está en `CLAUDE.md` §6.3.

> **El bloque de CIERRE ya no existe.** La firma "Pídelo por Rappi" que antes iba suelta entre el contenido y el footer se eliminó del sistema: ahora vive **dentro** del footer, controlada por la variable `firma`.

## El mail terminado

```
╔═ 1 · HERO SECTION ═══════════════════════════════════╗
║  <a href="AQUIELLINKDELBANNER">   un link para todo   ║
║  ┌─ contenedor header ───────────────────────────┐   ║
║  │   └─ 01_headers/<marca>/<disposición>-<fondo> │   ║
║  └───────────────────────────────────────────────┘   ║
║  ┌─ big-banner-horizontal.html  ó  -vertical.html┐   ║
║  └───────────────────────────────────────────────┘   ║
║  ┌─ imagen-full-width.html — opcional ───────────┐   ║
║  └───────────────────────────────────────────────┘   ║
╚═══════════════════════════════════════════════════════╝
╔═ 2 · CONTENTS SECTION ═══════════════════════════════╗
║  ┌─ _contenidos_wrapper.html  (480px) ───────────┐   ║
║  │   cta-llamado.html        ← obligatorio, 1º   │   ║
║  │   <div class="separador">                     │   ║
║  │   módulo                                      │   ║
║  │   <div class="separador">                     │   ║
║  │   módulo … (orden libre)                      │   ║
║  └───────────────────────────────────────────────┘   ║
╚═══════════════════════════════════════════════════════╝
╔═ 3 · FOOTER ═════════════════════════════════════════╗
║  06_footer/footer_general.html                        ║
║  fuera del paddedcontainer, siempre presente          ║
╚═══════════════════════════════════════════════════════╝
```

**Los wrappers no se editan.** `_header-wrapper.html` y `_contenidos_wrapper.html` son contenedores: solo se les inserta dentro el header o los módulos elegidos. El banner, la imagen full width y el footer no tienen wrapper propio — van directo en la cadena.

**Qué es obligatorio y qué no:**

| Pieza | ¿Va siempre? |
|---|---|
| Header | Sí, uno |
| Banner | Sí, uno solo (horizontal **o** vertical) |
| Imagen full width | No, opcional |
| CTA reglamentario | Sí, y es el primer elemento de CONTENTS |
| Módulos de contenido | Los que pida la fuente, con `separador` entre ellos |
| Footer | Sí, completo |

## Reglas especiales para módulos nuevos

### Cupones
- Siempre en **pares**. La tabla contiene 2 celdas por fila.
- La celda 1 puede reemplazarse por la celda suelta `celda_cupon_titulo.html` (título en vez de cupón) — es una decisión de contenido, no una regla automática por par/impar.
- Los legales se ponen en un `<tr>` aparte debajo de la fila principal.

### Beneficios
- Cada beneficio es una **tabla nueva**.
- Si hay 3 beneficios, hay 3 tablas seguidas con un separador entre cada una.