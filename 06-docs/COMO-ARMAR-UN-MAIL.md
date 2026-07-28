# Guía: Cómo armar un mail desde cero

Esta guía es para diseñadores y miembros del equipo que quieren entender el flujo completo, sin necesidad de saber programar.

## La metáfora rápida

Imagina una caja de LEGO con tres tipos de cosas:
1. **El tablero base** (`02-base-template/`)
2. **Los bricks** (`03-components/`)
3. **Las instrucciones** (los comentarios INICIO/FIN dentro de cada archivo + esta guía)

## Los pasos

### Paso 1 — Decide el "tipo de mail"
- **¿Qué KV?** Genérico, Turbo, Neutro, Pro o Pro Black.
- **¿Qué marca?** Rappi, Travel, Turbo, Turbo Rest, Pro o Pro Black.
- **¿Qué módulos?** Solo banner + CTA, o algo más complejo con deals, cupones, beneficios y módulos de contenido.

### Paso 2 — Empieza por el esqueleto
Toma `02-base-template/opening.html` y pégalo al inicio. Te da el doctype, head, meta tags, estilos globales y la apertura del wrapper.

### Paso 3 — Agrega un header
De `03-components/headers/`, elige UNO según la marca. Las instrucciones de cobranding (sin / con tag / 1:1) están en los comentarios del archivo.

### Paso 4 — Agrega un banner
De `03-components/banners/`, elige UNO:
- `big-banner-horizontal.html` — Si el mail tiene módulos en el body
- `big-banner-vertical.html` — Si el mail solo tiene CTA y cierre
- `banner-editorial.html` — Banner full image

### Paso 5 — Abre la zona de contenido
Pega `02-base-template/body-wrapper-open.html`.

### Paso 6 — Inserta los bricks del cuerpo
Aquí se decide qué piezas y en qué orden:

- **CTA** → `03-components/ctas/cta-template.html`
- **Deal grande / small** → `03-components/deals/`
- **Cupones** → `03-components/coupons/cupones-modulo.html` (siempre en pares)
- **Beneficios** → `03-components/benefits/modulo-beneficios.html` (uno por beneficio)
- **Módulo título** → `03-components/content-modules/modulo-titulo.html`
- **Módulo 3 columnas** → `03-components/content-modules/modulo-3-columnas.html`
- **Módulo 2 columnas** → `03-components/content-modules/modulo-2-columnas.html`
- **Módulo logos** → `03-components/content-modules/modulo-logos.html`
- **Módulo contenido** → `03-components/content-modules/modulo-contenido.html`

**Reglas de espaciado entre bricks:**

| Después de... | Va... |
|---------------|-------|
| Un módulo (`role="module"`) | `<div class="separador"></div>` antes del siguiente |
| Un CTA | `<div class="separador"></div>` antes del siguiente, EXCEPTO si va el cierre debajo |
| Un deal | NADA, los deals tienen su propio aire |

### Paso 7 — Agrega el cierre (si aplica)
De `03-components/closing/cierre.html`. **Se OMITE si:**
- El KV es Pro o Pro Black
- La fuente dice "sin cierre"

### Paso 8 — Cierra la zona de contenido
Pega `02-base-template/body-wrapper-close.html`.

### Paso 9 — Agrega el footer
De `03-components/footer/footer.html`. **El footer SIEMPRE va.** Solo cambias las variables Liquid según la fuente:
- `cond` → texto de legales adicionales (si lo hay)
- `font_style_look` → 'negro' para Genérico/Turbo/Neutro, 'pro' para Pro/ProBlack
- `show_legal_tyc` → true/false
- `show_legal_turbo` → true/false
- `show_legal_liquor` → true/false

### Paso 10 — Cierra el HTML
Pega `02-base-template/closing.html`. Listo.

## El mail terminado

```
[opening.html]
   ↓
[_header-wrapper.html ← contiene: header elegido]
   ↓
[banner elegido]
   ↓
[body-wrapper-open.html]
   ↓
[CTAs, deals, cupones, beneficios, módulos en orden libre]
   ↓
[cierre.html — opcional]
   ↓
[body-wrapper-close.html]
   ↓
[footer.html]
   ↓
[closing.html]
```

## Reglas especiales para módulos nuevos

### Cupones
- Siempre en **pares**. La tabla contiene 2 celdas por fila.
- Si hay cantidad impar, una celda se convierte en "Cupón Title" (con ícono + título).
- Los legales se ponen en un `<tr>` aparte debajo de la fila principal.

### Beneficios
- Cada beneficio es una **tabla nueva**.
- Si hay 3 beneficios, hay 3 tablas seguidas con un separador entre cada una.
