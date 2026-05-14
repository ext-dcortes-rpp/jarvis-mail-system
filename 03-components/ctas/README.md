# CTA · Call to Action

Botón pill principal del mail. Es el componente más visible del sistema — toda la jerarquía visual del email se construye alrededor de empujar al usuario hacia este click.

**Archivo:** [`cta-template.html`](cta-template.html)
**Tipo:** Atom (Atomic Design)
**Versión:** v1.1
**Figma:** [`04 · Atoms` → sección 4.3](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails)

---

## Anatomía

```
┌─────────────────────────────────────────┐
│  ┌───────────────────────────────────┐  │   ← <a> wrapper (deeplink_cta)
│  │                                   │  │
│  │      [text_cta] [bg-image →]      │  │   ← <table class="estilomobile">
│  │                                   │  │     pill border-radius 55px
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

**Características clave:**
- Border-radius: `55px` (pill completo)
- Max-width: `480px` (mobile-first)
- Background-image que cambia por variante (flecha/icono decorativo a la derecha)
- Border 1px `rgba(125, 129, 136, 0.5)` siempre visible
- Texto centrado, truncado a 40 caracteres
- Font: Helvetica, Tahoma, Verdana, sans-serif (fallback web-safe)

---

## Variables Liquid

| Variable | Tipo | Default | Notas |
|---|---|---|---|
| `text_cta` | string | — | Texto del botón. Se auto-trunca a 40 chars. |
| `deeplink_cta` | url | — | URL destino. Va en `href` y `originalsrc`. |
| `style_Look` | enum | `'neon'` | Define la variante visual. Ver tabla abajo. |
| `color_letra` | hex | derivado | Color del texto. Se setea automáticamente según `style_Look`. |
| `background_color` | hex | derivado | Color de fondo. Se setea automáticamente. |
| `cta_style_bg` | url | derivado | Background-image (flecha decorativa). Se setea automáticamente. |
| `estilomobile` | string | derivado | Clase CSS para el override mobile. |
| `estilomobiletxt` | string | derivado | Clase CSS para el texto en mobile. |

**Sólo `text_cta`, `deeplink_cta` y `style_Look` son inputs del editor.** El resto se derivan en cadena.

---

## Variantes (`style_Look`)

| `style_Look` | `color_letra` | `background_color` | `estilomobile` | Cuándo se usa |
|---|---|---|---|---|
| `'neon'` (default) | `#000000` | `#FFFFFF` | `botmobblanco` | KVs Genérico, Turbo |
| `'problack'` | `#FFFFFF` | `#000000` | `botmobpro` | KV ProBlack |
| `'pro'` | `#000000` | `#FFFFFF` | `botmobpro` | KV Pro |
| `'blanco'` | `#000000` | `#FFFFFF` | `botmobblanco` | KV Cafe (fallback). Idéntico a 'neon'. |
| `'negro'` | `#FFFFFF` | `#000000` | `botmobblanco` | KV Neutro |

**Por qué `'neon'` y `'blanco'` son idénticos:** son dos nombres para el mismo render. `'neon'` es el default editorial, `'blanco'` es el fallback explícito para Cafe. Si en el futuro el comportamiento se diferencia, los dos slots ya están separados.

---

## Mapeo KV → variante

| KV | `style_Look` |
|---|---|
| Genérico | `'neon'` |
| Turbo | `'neon'` |
| Neutro | `'negro'` |
| Pro | `'pro'` |
| ProBlack | `'problack'` |
| Cafe | `'blanco'` (fallback) |

---

## Comportamiento mobile

En mobile (`@media max-width:480px` y `max-width:620px`), las clases `botmobblanco / botmobnegro / botmobneon / botmobpro` aplican un border adicional para garantizar visibilidad:

```css
.botmobblanco, .botmobnegro, .botmobneon, .botmobpro {
  border: 1px solid rgba(125, 129, 136, 0.5) !important;
}
```

El `border-radius: 55px` se mantiene en mobile — el pill nunca se vuelve cuadrado.

---

## Reglas de uso

1. **Texto:** máximo 40 caracteres (Liquid trunca automáticamente). Recomendado: 2-3 palabras en mayúsculas o sentence case.
2. **`style_Look`:** elegir según el KV editorial del mail. No mezclar variantes en un mismo mail.
3. **Deeplink:** siempre URL absoluta. Usar deeplinks de la app cuando aplique (`rappi://...`).
4. **Posición:** el CTA principal nunca va dentro de un módulo de contenido — va aislado como su propia fila.
5. **Cantidad:** un solo CTA primario por mail. Si necesitás múltiples acciones, usar Big Deal o Small Deal con sus CTAs internos (border-radius `50px`, no `55px`).

---

## Ejemplo de uso

```liquid
{% assign text_cta = 'PEDIR AHORA' %}
{% assign deeplink_cta = 'https://rappi.com/pedido' %}
{% assign style_Look = 'pro' %}
```

Resultado:
- Texto "PEDIR AHORA" (5 chars, no se trunca)
- Click va a rappi.com/pedido
- Render con fondo blanco, texto negro, bg-image variante Pro
- Mobile: border 1px gris añadido vía `botmobpro`

---

## Validación pre-deploy

- [ ] `text_cta` no excede 40 chars
- [ ] `deeplink_cta` es URL absoluta válida
- [ ] `style_Look` es uno de los 5 valores permitidos
- [ ] El CTA renderea en mobile manteniendo el pill (radius 55px)
- [ ] El bg-image carga correctamente (algunos clientes bloquean imágenes externas; el `background_color` debe quedar legible si la imagen falla)
- [ ] El border 1px se ve en clientes que soportan `rgba()` (Outlook 2007-2013 puede fallar; aceptable)

---

## Cambios v1.1

- Antes (v1.0): 2-3 variantes rectangulares con border-radius pequeño y bg sólido.
- Ahora (v1.1): 5 variantes pill (radius 55px) con background-image por look + clases mobile específicas.
