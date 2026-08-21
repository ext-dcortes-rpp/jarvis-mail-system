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

### Paso 2 — Agrega un header
De `02-components/01_headers/`, elige la carpeta de marca y dentro de ella el archivo según fondo (claro/oscuro) y disposición (centrado/columnas). Las instrucciones de cobranding (sin / S / M / L / XL) están en los comentarios del archivo.

### Paso 3 — Agrega un banner
De `02-components/02_banners/`, elige `big-banner-horizontal.html` o `big-banner-vertical.html`. Las piezas internas (tag, imagen, créditos, textos) están en `02-components/02_banners/banner_moleculas/`.

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

La tabla general (`role="paddedcontainer"`, padding `20px 15px 0px 15px`) ya alinea todos los módulos entre sí — no se toca módulo por módulo. Cada módulo además tiene su propio padding según tenga o no fondo (`body_container_background_padding`: 10px con fondo, 0px sin fondo), para separar el contenido del fondo del contenedor.

| Después de... | Va... |
|---------------|-------|
| Un módulo (`role="module"`) | `<div class="separador"></div>` (16px) antes del siguiente |
| Un CTA | `<div class="separador"></div>` antes del siguiente, EXCEPTO si va el cierre debajo |
| Moléculas/componentes dentro de un módulo | `<div class="separador-M"></div>` (10px) o `<div class="separador-S"></div>` (4px) para aire mínimo |

### Paso 5 — Agrega el cierre (si aplica)
De `02-components/05_closing/cierre.html`. **Se OMITE si:**
- El tema es Pro o ProBlack (`tema_general_mail_general = 'pro'` o `'problack'`) — ⚠ auditoría: hoy `template_maestro_original.html` NO implementa esta exclusión, el cierre se renderiza igual para los 12 temas. Pendiente de confirmar con el equipo.
- La fuente dice "sin cierre"

### Paso 6 — Agrega el footer
De `02-components/06_footer/footer.html`. **El footer SIEMPRE va.** Solo cambias las variables Liquid según la fuente:
- `cond` → texto de legales adicionales (si lo hay)
- `font_style_look` → toma el valor de `{{color_footer_mail_general}}` según el tema activo (ver `GUIA-DE-TEMAS.md`)
- `show_legal_tyc` → true/false
- `show_legal_turbo` → true/false
- `show_legal_liquor` → true/false

## El mail terminado

```
[_header-wrapper.html ← contiene: header elegido]
   ↓
[banner elegido]
   ↓
[_contenidos_wrapper.html ← contiene: CTAs, deals, cupones, beneficios, módulos en orden libre]
   ↓
[cierre.html — opcional]
   ↓
[footer.html]
```

## Reglas especiales para módulos nuevos

### Cupones
- Siempre en **pares**. La tabla contiene 2 celdas por fila.
- La celda 1 puede reemplazarse por la celda suelta `celda_cupon_titulo.html` (título en vez de cupón) — es una decisión de contenido, no una regla automática por par/impar.
- Los legales se ponen en un `<tr>` aparte debajo de la fila principal.

### Beneficios
- Cada beneficio es una **tabla nueva**.
- Si hay 3 beneficios, hay 3 tablas seguidas con un separador entre cada una.
