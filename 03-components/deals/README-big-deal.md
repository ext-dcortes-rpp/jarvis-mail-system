# Big Deal

Tarjeta de deal destacado: el componente que muestra una oferta puntual con precio, descuento, descripción y CTA propio. Es uno de los dos "héroes" del sistema (junto con el Big Banner).

**Archivo:** [`deal-large.html`](deal-large.html)
**Tipo:** Organism (Atomic Design)
**Versión:** v1.1
**Figma:** [`06 · Organisms` → sección 6.3](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails)

---

## Anatomía

Estructura horizontal 50/50, max-width 480px, border-radius 16px:

```
┌─────────────────────┬─────────────────────┐
│  [tag1] [tag2]      │   ┌───────────┐     │
│                     │   │   LOGO    │     │
│  ┌─────────────┐    │   │  aliado   │     │
│  │ $70.000     │    │   └───────────┘     │
│  │ markdown    │    │                     │
│  └─────────────┘    │  [imagen producto]  │
│                     │                     │
│  40% OFF · $80.000  │                     │
│                     │   ┌─────────────┐   │
│  Descripción del    │   │ AL CARRITO  │   │
│  producto...        │   └─────────────┘   │
└─────────────────────┴─────────────────────┘
   COL IZQ (50%)         COL DER (50%)
   bg: deal_style_bg_general    bg: imagen producto
```

---

## Variables Liquid

### Inputs del editor

| Variable | Tipo | Truncate | Descripción |
|---|---|---|---|
| `deal_markdown_copy` | string | 22 chars | Precio destacado (ej. "$70.000") |
| `deal_porcentaje_off_copy` | string | 10 chars | Descuento (ej. "40% OFF") |
| `deal_antes_copy` | string | 25 chars | Precio anterior tachado (ej. "$80.000") |
| `deal_descripcion_copy` | string | 80 chars | Descripción corta del producto |
| `deal_cta_text` | string | 21 chars | Texto del CTA interno |
| `deal_recommendation_deeplink` | url | — | Click destination |
| `deal_recommendation_productimg` | url | — | Imagen del producto (columna derecha) |
| `deal_recommendation_brandlogo` | url | — | Logo del aliado |
| `deal_tag1_text` | string | — | Texto del primer tag (ej. "Descuento Pro") |
| `deal_style_look` | enum | — | Variante visual. Ver tabla abajo. |
| `deal_show_pro-crown` | bool | — | Mostrar corona Pro en el markdown (opcional) |
| `deal_style_logosize` | enum `'S'` o `'M'` | — | Tamaño del logo del aliado |

### Variables derivadas (no tocar)

`deal_style_bg_general` · `deal_style_bg_markdown` · `deal_style_box_backgroundimg` · `deal_style_txt_description` · `deal_style_txt_before` · `deal_style_txt_lgl1` · `deal_style_bg_cta` · `deal_style_crown_url`

---

## Variantes (`deal_style_look`)

| `deal_style_look` | `bg_general` | `bg_markdown` | `txt_description` | `txt_lgl1` |
|---|---|---|---|---|
| `'generico'` (default) | `#202020` | `#FBDC25` (amarillo) | `#E2E2E2` | `#919AAA` |
| `'neon'` | `#202020` | `#FBDC25` | `#E2E2E2` | `#919AAA` |
| `'problack'` | `#FBFBFB` (blanco frío) | `#D8D9D9` | `#292B30` | `#DAA868` |
| `'pro'` | `#1D1D1D` | `#D8D9D9` | `#E2E2E2` | `#919AAA` |

**Genérico vs Neon:** comparten todos los tokens excepto `deal_style_box_backgroundimg` (asset visual del fondo del producto). Neon usa una imagen con más energía visual.

---

## Mapeo KV → variante

| KV | `deal_style_look` |
|---|---|
| Genérico | `'generico'` |
| Turbo | `'neon'` |
| Neutro | `'generico'` |
| Pro | `'pro'` |
| ProBlack | `'problack'` |
| Cafe | `'generico'` (fallback) |

---

## Escalado dinámico (lógica crítica)

El Big Deal mide la longitud del `deal_markdown_copy` y del `deal_descripcion_copy` y aplica un tamaño + una clase CSS distintas. **Esto evita overflow en mobile cuando el texto es largo.**

### Markdown

```liquid
{% assign markdown_length = deal_markdown_copy.size %}

{% if markdown_length > 10 %}
  {% assign deal_markdown_size = '20px' %}
  {% assign deal_markdown_class = 'deal-destacado-s' %}
{% else %}
  {% assign deal_markdown_size = '24px' %}
  {% assign deal_markdown_class = 'deal-destacado-l' %}
{% endif %}
```

| Longitud markdown | Size desktop | Class | Override mobile (≤620px) |
|---|---|---|---|
| ≤ 10 chars (ej. "$70.000") | 24/20px | `deal-destacado-l` | 19/15px |
| > 10 chars (ej. "Desde $140.000") | 20/20px | `deal-destacado-s` | 15/16px |

### Descripción

| Longitud descripción | Size desktop | Class | Override mobile (≤620px) |
|---|---|---|---|
| ≤ 30 chars | 16/17px | `deal-texto2` | 11/12px |
| > 30 chars | 14/15px | `deal-texto2-s` | 9/10px |

---

## Corona Pro (opcional)

Si `deal_show_pro-crown = true`, antes del markdown se inserta una imagen de corona:

```liquid
{% if deal_show_pro-crown == true %}
  <img src="{{deal_style_crown_url}}" height="7" alt="Pro">
{% endif %}
```

**Cuándo usar:** mails con KV Pro o ProBlack que necesitan reforzar visualmente la membresía dentro del deal.

---

## Logo del aliado (`deal_style_logosize`)

| Valor | Render |
|---|---|
| `'S'` | `width: 55px` fijo |
| `'M'` | `max-width: 180px; max-height: 30px` |

Usar `'S'` para logos cuadrados, `'M'` para logos horizontales (marcas con tagline al lado).

---

## Reglas de uso

1. **Máximo 4 deals por mail.** Si la fuente trae más, sugerir reemplazar algunos por módulos de contenido.
2. **Truncates automáticos:** los inputs se cortan en Liquid. Si necesitás más caracteres, hay que rediseñar el copy, no extender el truncate.
3. **CTA interno:** `border-radius: 50px` (no `55px` como el CTA principal). Es una pill más compacta. Texto siempre en blanco sobre fondo negro.
4. **Imagen del producto:** debe tener fondo transparente o ser rectangular limpia. La celda derecha aplica `background-image` con `background-size: cover`.
5. **Tag1:** texto corto (1-3 palabras), tipo "Descuento Pro", "Solo hoy", "Exclusivo". No usar para precios o porcentajes.
6. **Corona Pro:** solo si el KV es Pro o ProBlack. No usar en Standard family.

---

## Ejemplo de uso

```liquid
{% assign deal_style_look = 'pro' %}
{% assign deal_markdown_copy = '$70.000' %}
{% assign deal_porcentaje_off_copy = '40% OFF' %}
{% assign deal_antes_copy = '$80.000' %}
{% assign deal_descripcion_copy = 'McCombo Mediano con bebida' %}
{% assign deal_cta_text = 'AL CARRITO' %}
{% assign deal_tag1_text = 'Descuento Pro' %}
{% assign deal_recommendation_deeplink = 'https://rappi.com/restaurante/...' %}
{% assign deal_recommendation_productimg = 'https://...' %}
{% assign deal_recommendation_brandlogo = 'https://...' %}
{% assign deal_show_pro-crown = true %}
{% assign deal_style_logosize = 'S' %}
```

Resultado:
- Markdown "$70.000" (7 chars ≤ 10) → size 24px, class `deal-destacado-l`, en mobile 19px
- Descripción "McCombo Mediano con bebida" (25 chars ≤ 30) → size 16px
- Variante Pro: bg blanco frío, accent gris, texto oscuro
- Corona Pro visible antes del precio
- Logo del aliado a 55px

---

## Validación pre-deploy

- [ ] `deal_markdown_copy` no excede 22 chars (Liquid lo trunca, pero queremos evitar `...`)
- [ ] `deal_descripcion_copy` no excede 80 chars
- [ ] `deal_style_look` es uno de los 4 valores permitidos
- [ ] La imagen del producto se ve completa en desktop y mobile
- [ ] El markdown en mobile no overflowea su contenedor (verificar con texto largo > 10 chars)
- [ ] El CTA "AL CARRITO" mantiene el pill 50px en todos los clientes
- [ ] `deal_show_pro-crown` solo activo en KVs Pro/ProBlack
- [ ] Corona renderea correctamente cuando se activa

---

## Cambios v1.1

- Antes (v1.0): tamaños fijos para markdown y descripción, sin lógica de escalado, sin corona Pro, sin `logosize` configurable.
- Ahora (v1.1): escalado dinámico por longitud de copy, 4 variantes Liquid completas, corona Pro opcional, logosize S/M.
