# Guía: Cómo armar un mail desde cero

Esta guía es para diseñadores y miembros del equipo que quieren entender el flujo completo, sin necesidad de saber programar.

## La metáfora rápida

Imagina una caja de LEGO con dos tipos de cosas:
1. **Los bricks** (`02-components/`)
2. **Las instrucciones** (los comentarios INICIO/FIN dentro de cada archivo + esta guía)

## Los pasos

### Paso 1 — Decide el "tipo de mail"
- **¿Qué tema?** Uno de los 11 (Beige 100/150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Dark neon, Dark Turbo, Dark Neutro, Pro, ProBlack) — ver `GUIA-DE-TEMAS.md`.
- **¿Qué marca de header?** Rappi, Travel, SoyRappi, Turbo, Turbo Rest, Pro, ProBlack, Defensoría, RappiEntregador o Contenido aliado.
- **¿Qué módulos?** Solo banner + CTA, o algo más complejo con deals, cupones, beneficios y módulos de contenido.

### Paso 2 — Agrega un header
De `02-components/01_headers/`, elige la carpeta de marca y dentro de ella el archivo según fondo (claro/oscuro) y disposición (centrado/columnas). Las instrucciones de cobranding (sin / S / M / L) están en los comentarios del archivo.

### Paso 3 — Agrega un banner
De `02-components/02_banners/`, elige UNO:
- `big-banner-horizontal.html` — Si el mail tiene módulos en el body
- `big-banner-vertical.html` — Si el mail solo tiene CTA y cierre

Las piezas internas (tag, imagen, créditos, textos) están en `02-components/02_banners/banner_moleculas/`.

### Paso 4 — Inserta los bricks del cuerpo
Aquí se decide qué piezas y en qué orden:

- **CTA** → `02-components/03_ctas/cta-template.html`
- **Deal grande / small** → `02-components/04_content-modules/deals/`
- **Cupones** → `02-components/04_content-modules/coupons/cupones-modulo.html` (siempre en pares)
- **Beneficios** → `02-components/04_content-modules/benefits/modulo-beneficios.html` (uno por beneficio)
- **Módulo título** → `02-components/04_content-modules/title/modulo-titulo.html`
- **Módulo 3 columnas** → `02-components/04_content-modules/3columnas/modulo-3-columnas.html`
- **Módulo 2 columnas** → `02-components/04_content-modules/2columnas/modulo-2-columnas.html`
- **Módulo logos** → `02-components/04_content-modules/logos/modulo-logos.html`
- **Módulo contenido** → `02-components/04_content-modules/1columna/modulo-1columna.html`

**Reglas de espaciado entre bricks:**

| Después de... | Va... |
|---------------|-------|
| Un módulo (`role="module"`) | `<div class="separador"></div>` antes del siguiente |
| Un CTA | `<div class="separador"></div>` antes del siguiente, EXCEPTO si va el cierre debajo |
| Un deal | NADA, los deals tienen su propio aire |

### Paso 5 — Agrega el cierre (si aplica)
De `02-components/05_closing/cierre.html`. **Se OMITE si:**
- El tema es Pro o ProBlack
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
- Si hay cantidad impar, una celda se convierte en "Cupón Title" (con ícono + título).
- Los legales se ponen en un `<tr>` aparte debajo de la fila principal.

### Beneficios
- Cada beneficio es una **tabla nueva**.
- Si hay 3 beneficios, hay 3 tablas seguidas con un separador entre cada una.
