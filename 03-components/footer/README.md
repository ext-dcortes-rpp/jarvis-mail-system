# Footer

El footer del mail. Es el componente más complejo del sistema porque combina **4 estilos visuales** con **internacionalización por 9 países** y **12 bloques condicionales** opcionales. Pero su comportamiento del lado del editor es simple: 4 flags Liquid resuelven todo.

**Archivo:** [`footer.html`](footer.html)
**Tipo:** Organism (Atomic Design)
**Versión:** v1.1
**Figma:** [`06 · Organisms` → sección 6.12](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails)

---

## Cómo funciona el footer en una frase

El editor setea `font_style_look` (estilo visual) y 3 booleans (`show_legal_tyc` / `show_legal_turbo` / `show_legal_liquor`). El footer detecta el país del usuario (`{{user_id}}` contains `'XX'`) y resuelve internamente: colores, logos, copies legales, URLs, bloque WhatsApp, membresía Pro.

**Si no detecta país,** el footer aborta el render: `{% abort_message('No country in user_id') %}`. Esto previene mails con legales rotos.

---

## Variables Liquid

### Inputs del editor (los únicos que se setean)

| Variable | Tipo | Default | Notas |
|---|---|---|---|
| `font_style_look` | enum | `'negro'` | `'negro'` · `'cafe'` · `'pro'` · `'blanco'` |
| `show_legal_tyc` | bool | — | Mostrar bloque de términos promo |
| `show_legal_turbo` | bool | — | Mostrar bloque legal RappiTurbo |
| `show_legal_liquor` | bool | — | Mostrar bloque legal de alcohol/licores |
| `cond` | string | `''` | Legales adicionales (string libre, admite HTML inline) |
| `pro_membresia` | string | — | Copy de membresía Pro (solo para `font_style_look = 'pro'`) |

### Variables derivadas (no tocar)

Se setean por cascada según `font_style_look` y país: `color_letra` · `color_textwa` · `color_bordewa` · `color_fondowa` · `walogo` · `logo` · `bigote` · `img-amor` · `show_hr` · `background_colour` · `color_membresia` · `centro_ayuda_url` · `aviso_privacidad_url` · `terminos_y_condiciones_url` · `legal_turbo_copy` · `legal_turbo_url` · `legal_liquor_copy` · `legal_liquor_img` · `wa-copy` · `wa-texto` · `deeplink_whatsapp` · `aplican_tyc` · `bottom_line_1` · `bottom_line_2`.

---

## Los 4 estilos (`font_style_look`)

### `'negro'` (default)

Footer oscuro, fondo `#040404`, texto gris `#7D8188`. WhatsApp verde (`#52ca2d`). Sin línea divisoria, sin bloque membresía.

| Token derivado | Valor |
|---|---|
| `color_letra` | `#7D8188` |
| `color_textwa` | `#52ca2d` |
| `color_bordewa` | `2px solid #52ca2d` |
| `color_fondowa` | `rgba(115,195,91,0.2)` |
| `show_hr` | `false` |
| `background_colour` | derivado del bg-body del KV |

**Usar para:** KVs Genérico, Turbo, Neutro.

### `'cafe'`

Footer cálido, texto marrón `#633D11`. WhatsApp verde (mismo que negro). Sin línea divisoria.

| Token derivado | Valor |
|---|---|
| `color_letra` | `#633D11` |
| `color_textwa` | `#52ca2d` |
| Resto | igual que `'negro'` |

**Usar para:** KV Cafe.

### `'pro'`

Footer premium. Texto gris `#7D8188`. WhatsApp naranja (`#F49502`). Línea divisoria activa (`<hr>`). Bloque de membresía Pro visible.

| Token derivado | Valor |
|---|---|
| `color_letra` | `#7D8188` |
| `color_textwa` | `#F49502` (naranja, no verde) |
| `color_bordewa` | `2px solid #F49502` |
| `show_hr` | `true` |
| `color_membresia` | `#7D8188` |

**Usar para:** KVs Pro y ProBlack.

### `'blanco'`

Footer luminoso, texto blanco sobre fondo oscuro/overlay. Sin bloque WhatsApp (`color_textwa = '—'`).

| Token derivado | Valor |
|---|---|
| `color_letra` | `#FFFFFF` |
| `background_colour` | `transparent` |

**Usar para:** mails que viven sobre overlays oscuros o imágenes full-bleed.

---

## Mapeo KV → estilo

| KV | `font_style_look` |
|---|---|
| Genérico | `'negro'` |
| Turbo | `'negro'` |
| Neutro | `'negro'` |
| Pro | `'pro'` |
| ProBlack | `'pro'` |
| Cafe | `'cafe'` |

**Notar:** Pro y ProBlack comparten footer. La diferencia visual entre ambos está en el resto del mail (banner, módulos), no en el footer.

---

## Internacionalización (9 países)

El footer detecta el país via `{% if ${user_id} contains 'XX' %}` y carga copies + URLs específicas:

| País | Idioma | Notas |
|---|---|---|
| 🇦🇷 AR | Español (voseo) | Pro membresía AR-style |
| 🇧🇷 BR | Portugués | `img-amor` especial · sin Pro membresía |
| 🇨🇱 CL | Español | `legal_liquor_img` custom (imagen, no texto) · Pro membresía |
| 🇨🇴 CO | Español | Legal alcohol Ley 30/1986 · Pro membresía |
| 🇨🇷 CR | Español (voseo) | Pro membresía AR-style |
| 🇪🇨 EC | Español | Pro membresía CO-style |
| 🇲🇽 MX | Español | Pro membresía con copy específico MX |
| 🇵🇪 PE | Español | Pro membresía CO-style |
| 🇺🇾 UY | Español (voseo) | Pro membresía AR-style |

**Si el `user_id` no contiene ninguno de estos códigos, el render aborta.**

---

## Bloques condicionales (12)

El footer está compuesto por 12 secciones. Algunas siempre aparecen, otras dependen de flags:

| Bloque | Condición | Notas |
|---|---|---|
| Logo Rappi superior | siempre | asset cambia por `font_style_look` |
| WhatsApp banner | opcional · todos los países excepto cuando `font_style_look = 'blanco'` | border 2px · "ÚNETE/UNITE/JUNTE-SE" según país |
| Centro de ayuda | siempre | mismo URL para todos los países |
| Aviso de privacidad | siempre | URL específica por país |
| Términos y Condiciones | siempre | URL específica por país |
| Cancelar suscripción | si `{% show_unsubscribe %}` | copy traducido por país |
| Legal turbo | si `show_legal_turbo == true` | copy + URL por país (CO y CL tienen URL extra) |
| Legal liquor | si `show_legal_liquor == true` | CL: imagen · resto: texto. Ley 30/1986 (CO), 124/1994 (CO menores) |
| Membresía Pro | solo si `font_style_look == 'pro'` | copy CO/EC/PE/CL · AR/UY/CR · MX. **Sin Brasil.** |
| Bigote ilustración | siempre | asset cambia por `font_style_look` |
| Img-amor (ilustración) | siempre | asset por `font_style_look` + variante BR |
| Bottom line 1 + 2 | siempre | copy localizado · Copyright entity legal por país |

---

## Reglas de uso

1. **Nunca omitir el footer.** Aunque la fuente no envíe datos, el footer se conserva como está en la base. Es el único organismo que no acepta ser borrado.

2. **`font_style_look` se decide por KV, no por preferencia editorial.** Es lookup automático.

3. **Pro y ProBlack siempre usan `'pro'`.** No `'problack'` — esa variante no existe en el footer.

4. **`show_legal_turbo` y `show_legal_liquor` son independientes.** Un mail de RappiTurbo con licores activa ambos.

5. **Si el país del usuario no existe en los 9 soportados, el render aborta.** Antes de subir un mail nuevo a un país, verificar que esté en la lista.

6. **El bloque WhatsApp depende del país, no del estilo.** Brasil no tiene WhatsApp banner aunque `font_style_look != 'blanco'`.

7. **Legales adicionales (`cond`):** si el editor envía un link, envolverlo:
   ```html
   <a href="linkaqui" style="text-decoration: none; color: #7D8188">linkaqui</a>
   ```

---

## Ejemplo de uso (mail de Pro con licores en CO)

```liquid
{% assign font_style_look = 'pro' %}
{% assign show_legal_tyc = true %}
{% assign show_legal_turbo = false %}
{% assign show_legal_liquor = true %}
{% assign cond = '' %}
{% assign pro_membresia = 'Tu membresía Rappi Pro se renovará automáticamente...' %}
```

Resultado (asumiendo `user_id` contiene `'CO'`):
- Footer en variante Pro (texto gris, WhatsApp naranja, línea divisoria)
- Centro de ayuda · Privacidad · TyC con URLs colombianas
- Legal liquor activo: texto Ley 30/1986
- Membresía Pro visible con copy CO-style
- Sin Legal turbo
- Bottom line con Copyright Rappi Colombia

---

## Validación pre-deploy

- [ ] `font_style_look` es uno de los 4 valores permitidos
- [ ] Los 3 booleans están seteados (no `null` ni undefined)
- [ ] El `user_id` del test corresponde a un país soportado (AR, BR, CL, CO, CR, EC, MX, PE, UY)
- [ ] Render preview en al menos 2 países distintos para verificar i18n
- [ ] Si es mail Pro: bloque membresía visible con copy correcto
- [ ] Si es mail con licores: legal liquor visible (texto o imagen según país)
- [ ] WhatsApp banner clickeable con touch target ≥ 44×44px en mobile
- [ ] Bottom line muestra la entidad legal correcta por país

---

## Cambios v1.1

- Antes (v1.0): 2 valores de `font_style_look` (`'negro'` / `'pro'`) con 4 flags Liquid. Los legales venían de un `content_block` de Braze (wrapper externo).
- Ahora (v1.1):
  - 4 estilos visuales (`'negro'` / `'cafe'` / `'pro'` / `'blanco'`)
  - Legales resueltos directamente en el footer (no en content_block externo)
  - Bloque WhatsApp opcional con copies para 9 países
  - Bloque membresía Pro con copy específico por país
  - KV Cafe agregado al sistema con su propio `font_style_look = 'cafe'`
