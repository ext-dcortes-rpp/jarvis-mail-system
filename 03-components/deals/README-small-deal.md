# Small Deal

Versión compacta del Big Deal. Misma estructura visual (50/50 horizontal) pero con tamaños más chicos. Pensado para mails con varios deals donde el Big Deal sería visualmente demasiado pesado.

**Archivo:** [`deal-small.html`](deal-small.html)
**Tipo:** Organism (Atomic Design)
**Versión:** v1.1
**Figma:** [`06 · Organisms` → sección 6.4](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails)

---

## Cuándo usar Big Deal vs Small Deal

| | Big Deal | Small Deal |
|---|---|---|
| **Cuándo** | Un deal protagonista del mail | Múltiples deals secundarios |
| **Markdown** | 24/20px | 18/12px |
| **Descripción** | 16/14px | 15/13px |
| **Logo mobile** | hasta 55px | máximo 30px |
| **Border-radius** | 16px | 16px |
| **Posición típica** | Después del banner principal | Grilla de 2-4 deals en el cuerpo |

---

## Anatomía

Idéntica al Big Deal — estructura 50/50 con markdown amarillo a la izquierda y CTA pill negro a la derecha. La diferencia es solo de tamaños.

---

## Variables Liquid

**Mismas que el Big Deal pero con prefijo `smalldeal_*` en lugar de `deal_*`:**

| Variable | Tipo | Truncate |
|---|---|---|
| `smalldeal_markdown_copy` | string | 22 chars |
| `smalldeal_porcentaje_off_copy` | string | 10 chars |
| `smalldeal_antes_copy` | string | 25 chars |
| `smalldeal_descripcion_copy` | string | 80 chars |
| `smalldeal_cta_text` | string | 21 chars |
| `smalldeal_recommendation_deeplink` | url | — |
| `smalldeal_recommendation_productimg` | url | — |
| `smalldeal_recommendation_brandlogo` | url | — |
| `smalldeal_tag1_text` | string | — |
| `smalldeal_style_look` | enum | — |
| `smalldeal_show_pro-crown` | bool | — |

**Los truncates son idénticos al Big Deal por consistencia editorial** — un editor puede mover copy entre Big y Small sin tener que reescribir.

---

## Variantes (`smalldeal_style_look`)

Idénticas al Big Deal: `'generico'`, `'neon'`, `'problack'`, `'pro'`.

---

## Mapeo KV → variante

| KV | `smalldeal_style_look` |
|---|---|
| Genérico | `'generico'` |
| Turbo | `'neon'` |
| Neutro | `'generico'` |
| Pro | `'pro'` |
| ProBlack | `'problack'` |
| Cafe | `'generico'` (fallback) |

---

## Escalado dinámico

Misma lógica que Big Deal, distintos tamaños:

### Markdown

| Longitud | Size desktop | Class | Override mobile (≤620px) |
|---|---|---|---|
| ≤ 10 chars | 18/18px | `smalldeal-destacado-l` | 19/18px |
| > 10 chars | 12/18px | `smalldeal-destacado-s` | 15/18px |

### Descripción

| Longitud | Size desktop | Class | Override mobile (≤620px) |
|---|---|---|---|
| ≤ 30 chars | 15/16px | `smalldeal-texto2` | 14/14px |
| > 30 chars | 13/14px | `smalldeal-texto2-s` | 12/12px |

**Notar:** en Small Deal, el override mobile es más sutil que en Big Deal. La razón es que el componente ya es chico — no podemos achicarlo más sin perder legibilidad.

---

## Reglas de uso

1. **Logo del aliado:** siempre máximo 30px en mobile (no es configurable como en Big Deal).
2. **No mezclar Big y Small en el mismo bloque:** o todos Big o todos Small. Mezclar rompe la jerarquía visual.
3. **Grilla recomendada:** 2 Small Deals lado a lado en desktop. En mobile colapsan a stack vertical.
4. **CTA interno:** `border-radius: 50px`, mismo que Big Deal. No se vuelve más chico.
5. **Corona Pro:** opcional, mismas reglas que Big Deal.

---

## Ejemplo de uso

```liquid
{% assign smalldeal_style_look = 'neon' %}
{% assign smalldeal_markdown_copy = '$50.000' %}
{% assign smalldeal_porcentaje_off_copy = '30% OFF' %}
{% assign smalldeal_antes_copy = '$71.000' %}
{% assign smalldeal_descripcion_copy = 'McCombo Mediano' %}
{% assign smalldeal_cta_text = 'PEDIR' %}
```

Resultado:
- Markdown "$50.000" (7 chars ≤ 10) → 18px desktop, 19px mobile
- Descripción "McCombo Mediano" (15 chars ≤ 30) → 15px desktop, 14px mobile
- Variante neon: bg módulo oscuro, accent crema

---

## Validación pre-deploy

- [ ] Mismo checklist que Big Deal
- [ ] El stack en mobile (cuando hay 2 small deals en fila) se ve legible
- [ ] El logo del aliado a 30px sigue siendo reconocible

---

## Cambios v1.1

- Antes (v1.0): versión horizontal compacta con estructura distinta al Big Deal (logo+info+precio+CTA en una sola línea).
- Ahora (v1.1): replica exactamente la estructura visual del Big Deal pero con tamaños reducidos. Misma lógica de escalado dinámico, mismos truncates, mismas variantes. Esto baja la carga cognitiva: aprendés un componente, tenés dos.
