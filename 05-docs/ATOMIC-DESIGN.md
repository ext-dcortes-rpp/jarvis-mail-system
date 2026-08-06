# Átomos, Moléculas y Organismos

Este documento es el equivalente en repo a las páginas **`04 · Atoms`**, **`05 · Molecules`** y **`06 · Organisms`** del Figma del sistema de diseño (`Doc-DS-Mails`). Reproduce, lo más fielmente posible, las tablas, mockups y reglas de cada página — con enlaces al archivo `.html` real detrás de cada pieza.

> **Estado:** clasificación completa. Las 3 páginas de Figma fueron revisadas y (para Moléculas y Organismos) reconstruidas pieza por pieza contra el código real durante este trabajo. Si algo en el Figma cambia, este doc puede quedar desactualizado — ante cualquier duda, el archivo `.html` real siempre gana.

## Índice

- [Átomos](#átomos)
  - [4.1 · Spacers verticales](#41--spacers-verticales)
  - [4.2 · Modificadores de texto](#42--modificadores-de-texto)
  - [4.3 · Logo — comportamiento por módulo](#43--logo--comportamiento-por-módulo)
  - [4.4 · Image atoms — tamaño por módulo](#44--image-atoms--tamaño-por-módulo)
  - [4.5 · Etiquetas y badges](#45--etiquetas-y-badges)
  - [4.6 · CTAs base (8 variantes)](#46--ctas-base-8-variantes)
- [Moléculas](#moléculas)
  - [5.1 · Header (Logo + Cobranding)](#51--header-logo--cobranding)
  - [5.2 · Moléculas de banner](#52--moléculas-de-banner)
  - [5.3 · Moléculas de contenido](#53--moléculas-de-contenido)
  - [5.4 · Tabla de cierre](#54--tabla-de-cierre-️-ver-nota)
- [Organismos](#organismos)
  - [6.1 · Big Banner · Vertical](#61--big-banner--vertical)
  - [6.2 · Big Banner · Horizontal](#62--big-banner--horizontal)
  - [6.3 · Módulo Título](#63--módulo-título)
  - [6.4 · Deals en Columnas](#64--deals-en-columnas)
  - [6.5 · Módulo Cupones](#65--módulo-cupones)
  - [6.6 · Módulo Bullet](#66--módulo-bullet)
  - [6.7 · Módulo Beneficios](#67--módulo-beneficios)
  - [6.8 · Módulo 1 Columna](#68--módulo-1-columna)
  - [6.9 · Módulo Dos Columnas](#69--módulo-dos-columnas)
  - [6.10 · Módulo Logos](#610--módulo-logos)
  - [6.11 · Módulo 3 Columnas](#611--módulo-3-columnas)
  - [6.12 · Footer: General, Sin Amor, RTS](#612--footer-general-sin-amor-rts)
- [Hallazgos de auditoría](#hallazgos-de-auditoría-consolidado)
- [Referencias cruzadas](#referencias-cruzadas)

---

## Átomos

**Elementos sueltos.** La pieza visual mínima: no tiene contenedor propio ni contexto — un texto, una imagen, un ícono, un tag, un separador, un CTA. Por sí solo no impone reglas de tamaño o posición; esas las adquiere cuando se combina dentro de una molécula.

> 📐 **Nota:** la tipografía del sistema (tamaños, jerarquías, comportamiento responsive) NO vive acá. Vive en **Tokens 2.3** — es la fuente única.

### 4.1 · Spacers verticales

Los átomos de espaciado. Los primeros tres son divs vacíos de alto fijo — puro espacio en blanco, sin línea visible. El cuarto SÍ es una línea visible, coloreada por tema.

| Clase | Tamaño | Uso |
|---|---|---|
| `.separador` | 16px | Entre dos `role="module"` del mismo tipo |
| `.separador-M` | 10px | Entre dos `role="componente"` |
| `.separador-S` | 4px | Espaciado fino para casos especiales |
| `molecula-separador` | contenedor 10px alto · línea 50×1px | Línea visible, color `{{color_acento1_mail_general}}`. Bajo títulos (2 Columnas, Logos, Módulo Título) |

```
.separador (16px)     .separador-M (10px)   .separador-S (4px)   molecula-separador
▭                     ▭                     ▭
   ↕ 16px                ↕ 10px                ↕ 4px             ──── (línea 50×1px,
▭                     ▭                     ▭                    color acento1)
```

Ver **Tokens 2.4** para las reglas de uso detalladas de `.separador` / `.separador-M` / `.separador-S`.

### 4.2 · Modificadores de texto

El texto ya no usa indicadores en la copia (`**`, `x`, `-`) para bold/resaltado/tachado. Los modificadores se aplican directo vía etiqueta HTML + `style` inline sobre `molecula-texto`. Fuente de verdad: `content_moleculas/modificadores-texto.html`.

| Modificador | Cómo se aplica | Módulos donde se usa |
|---|---|---|
| Tamaño | Etiqueta h1–h6 o `.legal` (escala en Tokens 2.3) | Content-modules — todos los `role="molecula-texto"` |
| Color base | `style="color: {{color_texto_mail_general}}"` | Content-modules — color por defecto |
| Subtono 1 | `style="color: {{color_acento1_mail_general}}"` | Destacar cifras u ofertas con el acento del tema |
| Subtono 2 | `style="color: {{color_acento2_mail_general}}"` | Destacar montos ($, %) — rojo Rappi universal |
| Bold | `font-weight: bold;` | Combinable con color (anidado) |
| Italic | `font-style: italic;` | Content-modules |
| Tachado | `text-decoration: line-through;` | Precios anteriores (Deals, Cupones) |
| Subrayado | `text-decoration: underline;` | Content-modules |
| Superíndice | Texto dentro de `<sup>` | Marcas registradas, notas al pie |
| Texto vertical | `writing-mode: vertical-rl;` (+ prefijos webkit/ms) | Banner — número de promo ("Ahora"), clases `bnr-hasta-*` |
| Interletrado ancho | `letter-spacing: 4px;` (clase `bnr-sm`, bold, mayúsculas) | Banner — módulo de créditos ("DE REINTEGRO") |

```
Bold          Tachado              Vertical (writing-mode: vertical-rl)
**Texto**     ~~Antes $50.000~~      A
                                     h
                                     o
                                     r
                                     a
```

### 4.3 · Logo — comportamiento por módulo

El logo no es un átomo de un solo tamaño: cambia de tamaño según el módulo. Lista completa, de menor a mayor:

| Tamaño | Elemento | Clase/Role | Módulo |
|---|---|---|---|
| 15px | Ícono genérico S | `role="molecula-iconoS"` | Content-modules — slot genérico |
| 21–34px (según marca) | Header — logo principal | `.logo-base1` … `.logo-base4` | Headers — 4 grupos de marca, ver `USO-DE-CADA-PARTE.md` |
| 24–47px (según marca/tamaño) | Header — cobranding | `.cobranding-s` / `-m` / `-l` | Headers, cobranding activo |
| 25px | Ícono genérico M | `role="molecula-iconoM"` | Content-modules |
| 38px (max-height) | Cierre — firma "RappiFirma" | `05_closing/cierre.html` | Cierre del mail |
| 50px | Ícono genérico L / logo aliado | `role="molecula-iconoL"` | Franja de Logos, Deals |
| 60px | Ícono genérico XL | `role="molecula-iconoXL"` | Content-modules, Bullet |
| 75px | Banner — imagen fija con logo | `.banner-logo1-1` | `banner_moleculas/modulo_img_altofijo_*.html` |
| 170px (max-width) | Footer — logo de firma final | `06_footer/footer_*.html` | Footer |
| Variable | Módulo de Logos — grilla 3/4/6 | `role="logoN"` | `grilla3/4/6logos.html` — 100% de la celda, sin tamaño fijo |

```
15px   ▪            Ícono S
21-47  ▪▪           Header (logo / cobranding)
25px   ▪▪           Ícono M
38px   ▪▪▪          Cierre "RappiFirma"
50px   ▪▪▪▪         Ícono L / logo aliado
60px   ▪▪▪▪▪        Ícono XL
75px   ▪▪▪▪▪▪       Banner imagen fija
170px  ▬▬▬▬▬▬▬▬     Footer firma final
var.   ▭▭▭▭▭▭▭▭▭▭   Grilla de Logos (3/4/6)
```

### 4.4 · Image atoms — tamaño por módulo

La imagen tampoco tiene un tamaño único — va de un micro-ícono de 6px a una imagen full-width de 480px. Las imágenes vienen de la hoja "TAXONOMÍA ASSETS", cada una con nombre semántico y URL pública en `lh3.googleusercontent.com`.

| Tamaño | Elemento | Módulo | Mobile |
|---|---|---|---|
| 6px | Corona Pro (`coronapro_mail_body`) | Badge "$999" (Tag Promo) en Deals/Cupones | Igual |
| 10px | Ícono rating ⭐ / tiempo 🕐 | Deals | Igual |
| 12–14px | Íconos sociales (WhatsApp/Telegram/Facebook) | Footer | Igual |
| 15px | Ícono genérico S | Content-modules | Igual |
| 25px | Ícono genérico M | Content-modules, 3 Columnas | Igual |
| 50px | Ícono genérico L / logo aliado | Franja de Logos, Deals | Igual |
| 60px | Ícono genérico XL | Content-modules, Bullet | Igual |
| ~160px (100% celda) | Imagen de celda | 3 Columnas | Igual (mantiene 3 columnas) |
| 192→240px (40%→50%) | Imagen de columna — Beneficios | `role="imagen-auto"` + `.beneficios-mob` | **Cambia** — 40%→50% |
| 240→480px (50%→100%) | Imagen de columna — 2 Columnas | 2 Columnas | **Cambia** — se apila full-width |
| Variable % | Imagen automática — Banner | `banner_img_modulo_auto_ancho` | Depende de la columna |
| 480px (100%) | Imagen full-width, puntos decorativos | 1 Columna, Cupones (`body_container_img_dots`) | Igual — ya es full-width |

```
6px    ▪    Corona Pro
15px   ▪    Icono S
25px   ▪▪   Icono M
50px   ▪▪▪  Icono L
60px   ▪▪▪▪ Icono XL
~160px ▭▭▭▭▭▭       3 Columnas (celda)
192-240▭▭▭▭▭▭▭▭     Beneficios (crece en mobile)
240-480▭▭▭▭▭▭▭▭▭▭▭  2 Columnas (crece en mobile)
480px  ▬▬▬▬▬▬▬▬▬▬▬▬▬▬ Full-width (1 Columna, Cupones)
```

### 4.5 · Etiquetas y badges

Pills chicas que clasifican contenido o destacan un precio/crédito. Dos familias: **tags genéricos** (banner, body, deals, cupones — colores por tema) y **badges** (Tag Promo/Verde/Básico, el estilo "$999").

**1 · Tags genéricos** — se adaptan al tema vía `bg_tag_fondo` / `bg_tag_contenedor` / `color_tag_tipografia`:

| Ejemplo | Estilo | Detalle |
|---|---|---|
| "tag 1" + ícono | Tag con ícono | radio 14px · padding 2px 4px · ícono 12–13px opcional · Banner, Body (`molecula_tag_icono`), Deals |
| "Solo en" | Pastilla chica (h5) | radio 30px · padding 4px 7px · texto 12/13px · Cupones (`molecula_texto_pastilla`) |
| "Martes" | Pastilla grande (h3) | radio 30px · padding 4px 7px · texto 16/17px · Content-modules ("Texto + Pastilla") |

**2 · Badges — Tag Promo / Verde / Básico:** h1, padding 2px 4px, radio 3px, line-height 20px. Colores fijos por función (no por tema), salvo una variante dorada en Pro/ProBlack.

| Theme group | Descuento (Tag Promo) | Créditos (Tag Verde) |
|---|---|---|
| Pastel / Dark | `50% OFF` — bg `#FBDB20` · texto `#000000` | `120 créditos` — bg `#29D884` · texto `#083410` |
| Pro / ProBlack | `50% OFF` — bg `#F8D263` (dorado) · texto `#000000` | `120 créditos` — bg `#CC984E` (dorado tostado) · texto `#FEE4C0` |

- **Tag Básico:** `color_acento2_mail_general` sobre `bg_solid_generico100_mail_body` — agrupación distinta (blanco en pastel+ProBlack, negro en dark+Pro).
- **Tag Promo + ícono:** el badge de precio del Deal antepone la corona (`coronapro_mail_body`, 6px) al monto.

```
(●)tag 1        (Solo en)      (Martes)        [50% OFF]        [120 créditos]
radio 14px      radio 30px     radio 30px       Pastel/Dark      Pastel/Dark
                                                 [50% OFF]dorado  [120 créditos]dorado
                                                 Pro/ProBlack     Pro/ProBlack
```

> ⚠ **Regla · nunca hardcodear colores de tag.** Aunque los valores son universales, siempre usar la variable Liquid — un cambio de paleta futuro solo debería tocar `head-meta-tags.html`.
>
> ⚠ **Auditoría:** el snippet de ícono+badge en el Figma usa `role="MARKDOWN"` sobre un `<h4>` — inconsistente con el patrón `role="molecula-texto"` usado en el resto de la página. Verificar contra el `.html` real antes de tomarlo como convención.

### 4.6 · CTAs base (8 variantes)

Botón pill (`border-radius` 55–60px) invocado desde `cta-llamado.html` vía `{{content_blocks.${CTA-template}}}`. `style_Look` define el bg sólido de respaldo, el ícono de flecha, y (solo en neon/verde) una imagen de fondo degradé.

> **Cambio v1.2:** el botón ya no se llama directo. `cta-llamado.html` define 4 variables (`cta_alineado`, `text_cta`, `deeplink_cta`, `style_Look`) y luego invoca `{{content_blocks.${CTA-template}}}`. `style_Look` pasó de 5 a 8 variantes reales.

| `style_Look` | Fondo | Mobile |
|---|---|---|
| `neon` (default) | bg-image degradé + flecha propia | sin borde |
| `blanconeon` | bg blanco sólido, sin degradé | `.borde_mobile` |
| `negroneon` | bg negro sólido | `.borde_mobile` |
| `verde` | bg-image degradé verde | `.borde_mobile` |
| `blancogris` | bg blanco sólido | `.borde_mobile` |
| `negrogris` | bg negro sólido | `.borde_mobile` |
| `problack` | predeterminado tema ProBlack | `.borde_mobile` |
| `pro` | predeterminado tema Pro | `.borde_mobile` |

> ⚠ **Deprecado:** `style_Look='blanco'` sigue existiendo como alias legacy idéntico a `blanconeon` — **no usar en código nuevo**.

```
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ neon        │ blanconeon  │ negroneon   │ verde       │
│[Pedir ahora→]│[Pedir ahora→]│[Pedir ahora→]│[Pedir ahora→]│
├─────────────┼─────────────┼─────────────┼─────────────┤
│ blancogris  │ negrogris   │ problack    │ pro         │
│[Pedir ahora→]│[Pedir ahora→]│[Pedir ahora→]│[Pedir ahora→]│
└─────────────┴─────────────┴─────────────┴─────────────┘
```

```liquid
{{ cta_alineado }}  → 'left' | 'center'
{{ text_cta }}      → texto del botón (máx. 35 chars, auto-truncate)
{{ deeplink_cta }}  → URL destino
{{ style_Look }}    → 'neon'(default) | 'blanconeon' | 'negroneon' | 'verde' |
                       'blancogris' | 'negrogris' | 'problack' | 'pro'
```

---

## Moléculas

Hay dos formas de ser molécula:

1. **Átomos dentro de un contenedor** que le impone sus propias reglas de tamaño/posición según dónde vive (un logo se ve distinto en un banner que en un deal).
2. **Átomos unidos que forman un elemento simple con reglas propias** — bullets, tags, módulos de promo.

Una molécula todavía no tiene contexto de página completa — eso la distingue del organismo.

### 5.1 · Header (Logo + Cobranding)

Header armado con logo base + divider + cobranding. Dos estructuras — **Centrado** y **Columnas** — cada una con 4 formatos (logo+cobranding S/M/L, y logo solo). El alto es fijo por grupo de marca; el ancho se ajusta automático. Los tamaños **sí cambian** entre desktop y mobile (valor propio por grupo en `global-styles.html`, no un 90% plano).

```
Centrado — PEQUEÑO                    Columnas — PEQUEÑO
┌───── Escritorio ─────┐             ┌───── Escritorio ─────┐
│   [LOGO] | [cobrand]   │             │ [LOGO]        [cobrand]│
└─────────────────────┘             └─────────────────────┘
   alto NNpx · ancho auto              logo izq · cobranding der · sin divider
```

**Tamaños de header — todas las variaciones** (F = px Figma, ≈ = aprox. HTML):

| Grupo | Aplica a | Logo (desktop) | Cob S | Cob M | Cob L |
|---|---|---|---|---|---|
| 1 | Rappi, Travel, SoyRappi | F70/≈30 | F77/≈33 | F84/≈36 | F95/≈41 |
| 2 | Turbo, Pro, ProBlack, Defensoría | F60/≈26 | F66/≈28 | F72/≈31 | F82/≈35 |
| 3 | Turbo Rest | F80/≈34 | F88/≈38 | F96/≈41 | F109/≈47 |
| 4 | RappiEntregador, Contenido aliado | F50/≈21 | F55/≈24 | F60/≈26 | F67/≈29 |

Mobile (mismo agrupamiento): Grupo 1 → logo F63/≈28, Cob S/M/L F69·76·86 / ≈31·34·38 · Grupo 2 → F54/≈24, F59·65·75/≈26·29·33 · Grupo 3 → F72/≈32, F79·86·100/≈35·38·44 · Grupo 4 → F45/≈20, F50·54·61/≈22·24·27.

4 tamaños × (logo-base + cobranding S/M/L) = **16 clases HTML**. Aproximación calibrada con el ejemplo Size-1: desktop ≈ Figma×0.43, mobile ≈ Figma×0.44 — ajustable en implementación.

### 5.2 · Moléculas de banner

Viven en `02-components/02_banners/banner_moleculas/`. Piezas exclusivas del Big Banner (horizontal + vertical) — ver [6.1](#61--big-banner--vertical) y [6.2](#62--big-banner--horizontal) para la estructura completa.

**Módulos del banner** (posición fija, no intercambiables):

| Módulo | Descripción | Horizontal | Vertical |
|---|---|---|---|
| MODULO TAGS | Hasta 3 tags, bg `{{bg_tag_fondo_mail_general}}` | Fijo abajo, no se mueve | Movible, por defecto abajo |
| IMAGEN FIJA | Imagen estática + logo opcional sobre `{{img_overlay_2_mail_general}}` | ✓ columna 240px | ✓ opcional, movible |
| IMAGEN AUTOMÁTICA | Imagen dinámica Braze, ancho variable `{{banner_img_modulo_auto_ancho}}%` | ✓ alterna con la fija | No existe como módulo — usar `molecula_img_automatica` |

**Moléculas combinables** (dentro de MODULO MOLECULAS — horizontal: orden fijo, vertical: reordenable/duplicable):

| Molécula | Archivo | Descripción |
|---|---|---|
| `molecula_promo` | `molecula_promo_horizontal/vertical.html` | "Ahora" + monto, color `{{color_descuento_mail_general}}` |
| `molecula_creditos` | `molecula_creditos_horizontal/vertical.html` | Créditos disponibles + "DE REINTEGRO" |
| `molecula_textoxl` | `molecula_textoxl_horizontal/vertical.html` | Texto vivo XL, mensaje principal |
| `molecula_texto_M` | `molecula_texto_M_horizontal/vertical.html` | Texto vivo M / complemento |
| `molecula_img_automatica` | `molecula_img_automatica_horizontal/vertical.html` | Imagen embebida entre moléculas (Braze) |
| `molecula_cta_interno` | `molecula_cta_interno_horizontal/vertical.html` | CTA embebido dentro del banner |
| `molecula_texto_pastilla` | `molecula_texto_pastilla.html` (un solo archivo) | Texto + pastilla, orden intercambiable |
| `molecula_texto_complementario` | `molecula_texto_complementario_horizontal/vertical.html` | Texto libre complementario (h2) |

```html
<!-- MODULO MOLECULAS: se insertan solo las necesarias, una debajo de otra -->
<table width="240" align="left"> <!-- horizontal 240px fijo · vertical width:100% -->
  <tr><td style="padding: {{padd_banner_mail_general}}">
    <!-- MOLECULA PROMOS / CREDITOS / TEXTO XL / TEXTO M / IMG AUTOMATICA / CTA INTERNO -->
  </td></tr>
</table>
```

> **Regla · orden y colores:** en horizontal el orden es fijo (promo → créditos → texto XL → texto M → img automática → cta interno); en vertical es libre y el módulo se puede duplicar. Ninguna molécula hardcodea color — todas heredan variables de tema.
>
> ⚠ **Duplicado sin resolver:** `molecula_textom_horizontal.html` y `molecula_texto_M_horizontal.html` (y sus pares `_vertical`) son **byte-idénticos** — dos nombres para el mismo archivo. Pendiente decidir cuál nombre se conserva.

### 5.3 · Moléculas de contenido

Viven en `02-components/04_content-modules/content_moleculas/`. Piezas insertables dentro de módulos de contenido (1/2/3 Columnas, Beneficios, Cupones, Logos, Título).

**1 · Bullets** — marcador a la izquierda (número o ícono, 4 tamaños) + bloque de texto a la derecha, mismo patrón en las 4 variantes:

| Molécula | Archivo | Marcador |
|---|---|---|
| Bullet numerado | `molecula_bullet_numerado.html` | Número, borde `{{color_acento2_mail_general}}` |
| Bullet ícono S | `molecula_bullet_icono_s.html` | `role="molecula-iconoS"` |
| Bullet ícono M | `molecula_bullet_icono_m.html` | `role="molecula-iconoM"` |
| Bullet ícono L | `molecula_bullet_icono_l.html` | `role="molecula-iconoL/XL"` |

```
[1]  Subtítulo          [●]  Subtítulo          [◐]  Subtítulo         [▣]  Subtítulo
     bloque de texto          bloque de texto         bloque de texto        bloque de texto
Bullet numerado          Bullet ícono S            Bullet ícono M          Bullet ícono L
```

**2 · Tags y pastillas:**

| Molécula | Archivo | Composición |
|---|---|---|
| Tag con ícono | `molecula_tag_icono.html` | `role="molecula-tag"` · bg `{{bg_tag_fondo_mail_general}}`, radio 14px · ícono opcional/intercambiable |
| Tag Promo | `molecula_tag_promo.html` | bg `{{bg_descuento_mail_general}}` · "$999" — badge de sistema (Descuento) |
| Tag Verde | `molecula_tag_verde.html` | bg `{{bg_creditos_mail_general}}` · "$999" — badge de sistema (Créditos) |
| Tag Básico | `molecula_tag_basico.html` | bg `{{bg_solid_generico100_mail_body}}` · agrupación de color distinta |
| Texto + Pastilla | `molecula_texto_pastilla.html` | Texto + pastilla, orden de celdas intercambiable |

**3 · Moléculas deals** — combinaciones compactas exclusivas de Deals, viven inline en `deals/deal_columnas.html` (no son archivo aparte). Cada elemento interno es independiente: si no tiene texto, se elimina solo ese tag, no la molécula completa.

| Molécula | Composición |
|---|---|
| Texto + Rating | CATEGORIA (texto plano) + RATING (⭐ + texto) + TIEMPO (🕐 + texto) |
| Línea de Markdown | MARKDOWN (Tag Promo + corona 6px) + COMPLEMENTO 1 ("99% OFF") + COMPLEMENTO 2 ("| Antes $999" tachado) |

```
Italiana   ⭐ 4.9   🕐 xx min.        👑 $999   99% OFF   | Antes ~~$999~~
Texto + Rating                        Línea de Markdown
```

**4 · Otras moléculas:**

| Molécula | Archivo | Composición |
|---|---|---|
| Link interno | `molecula_link_interno.html` | Pill con círculo + ícono (17px) + "Clic aquí" — `<a>` completo, `target="_blank"` |
| Franja de logos | `molecula_franja_logos.html` | N × [círculo decorativo + `role="molecula-iconoL"` 50px con `<a href="LINKLOGO">`] — celdas agregables/removibles |

### 5.4 · Tabla de cierre ⚠️ (ver nota)

> ⚠ **Nota de clasificación:** el propio texto de esta sección se autodescribe como *"el último organismo antes del footer"* — es decir, el contenido mismo dice ser un **organismo**, no una molécula, aunque está numerado en la página de Moléculas. Se documenta acá tal cual está en el Figma actual, sin reclasificar unilateralmente.

Imagen final de cierre (firma de marca). Se elige 1 de 10 variantes de URL según la variable fuente "Pide img".

**Comportamiento:**
- Si "Pide img" coincide con uno de los 10 textos conocidos → usar la URL correspondiente de la base.
- Si "Pide img" es exactamente `"sin cierre"` → eliminar la etiqueta `<img>` por completo (tabla contenedora vacía).
- Si el tema es `'pro'`/`'problack'` → toda la tabla debería eliminarse (regla no implementada hoy en `template_maestro_original.html` — ver [Hallazgos de auditoría](#hallazgos-de-auditoría-consolidado)).
- Si "Pide img" no coincide con nada de la base → conservar la imagen que ya trae la plantilla base.

**Base de datos · 10 URLs** (texto en "Pide img" → familia → URL):

| Texto en "Pide img" |
|---|
| "Pide un Rappi" |
| "Pedí un Rappi" |
| "Pídelo por Rappi mx" |
| "Pede um Rappi" |
| "Pide un RappiTurbo" |
| "Pídelo por RappiTurbo mx" |
| "Pedí un RappiTurbo" |
| "Pide un RappiTurbo + Carulla" |
| "Pide un RappiTurbo + MiComisariato" |
| "Pede um RappiTurbo" |

Debajo de esta sección **no se debe insertar** ningún módulo de contenido o CTA — solo puede seguir el footer.

---

## Organismos

**La pieza de LEGO con estructura fija**, compuesta de varias moléculas combinadas — banners, deals, módulos en columnas, cupones. Cada organismo es autocontenido: tiene su propio padding, su propia lógica, y vive como bloque completo (`table role="module"`) dentro del HTML.

> La numeración de abajo (6.1–6.12) sigue las etiquetas internas de cada sección en Figma, que están limpias y consecutivas. Algunos nombres de capa (layer name, panel de outline de Figma) quedaron desincronizados por ediciones concurrentes — es puramente cosmético del panel de capas y no afecta el contenido; se ignoran acá.

### 6.1 · Big Banner · Vertical

**Archivo:** sin archivo único — se referencia como `BANNER_VERTICAL` (ver `banner_moleculas/`). **Cuándo se usa:** mails que solo tienen CTA y cierre, o banners con logos.

3 módulos apilables en una sola columna — MODULO MOLECULAS, MODULO IMAGEN FIJA, MODULO TAGS — libremente reordenables. A diferencia del horizontal (6.2), ninguna posición es fija.

```
┌─────────────────────────┐
│  MODULO MOLECULAS         │   "Pídelo en Rappi"
│  (orden libre)             │   "Y recibe lo que necesitas
│                             │    en minutos"
├─────────────────────────┤
│  MODULO IMAGEN FIJA        │   (opcional, se puede eliminar)
├─────────────────────────┤
│  + MODULO TAGS (libre)     │   por defecto abajo
└─────────────────────────┘
        Vertical / Mobile (mismo layout, elementos más chicos)
```

**Reglas:** MODULO MOLECULAS se puede duplicar y reordenar libremente; MODULO IMAGEN FIJA es opcional (se puede eliminar o mover); MODULO TAGS tiene posición libre. Moléculas insertables (ver [5.2](#52--moléculas-de-banner)): `promo`, `creditos`, `textoxl`, `texto_M`, `texto_complementario`, `texto_pastilla`, `img_automatica`, `cta_interno`.

```html
<a role="vertical" href="AQUIELLINKDELBANNER" style="text-decoration:none; display:inline-block; width:100%;">
<table id="BANNER_VERTICAL" width="480" style="width:480px; margin:0 auto;">
  <tr valign="middle">
    <td style="background-image:url({{bg_bannerimg_mail_general}}); border-radius:16px; overflow:hidden;">
      <div style="background:{{bg_bannertono_mail_general}}; max-width:480px; overflow:hidden;">
        <!-- MODULO MOLECULAS: reordenable/duplicable -->
        <!-- MODULO IMAGEN FIJA: opcional -->
        <!-- MODULO TAGS: posición libre -->
      </div>
    </td>
  </tr>
</table>
</a>
```

### 6.2 · Big Banner · Horizontal

**Cuándo se usa:** mails con módulos de contenido en el body además de cierre y CTA.

SIEMPRE 2 columnas fijas de 240px: MODULO MOLECULAS (izquierda) + MODULO IMAGEN (derecha — **obligatoria**, fija o automática, a diferencia del vertical donde es opcional). Debajo, a todo el ancho, MODULO TAGS con posición fija.

```
┌───────────────┬───────────────┐
│ $40.000         │                 │
│ Tienes 5 créditos│  MODULO IMAGEN │   fija o automática
│ Texto vivo M    │  SIEMPRE presente│  (obligatoria)
│ /complemento    │                 │
├───────────────┴───────────────┤
│              [tag1][tag2][tag3] │   fijo abajo, no se mueve
└─────────────────────────────────┘
        Desktop / Mobile (mismo layout, elementos más chicos)
```

**Anatomía:** 2 columnas fijas de 240px · columna imagen obligatoria · hasta 3 tags alineados a la derecha, posición fija · colores 100% por tema · tamaños de moléculas inline en desktop + clases `.bnr-*` solo en mobile (`!important`).

Moléculas disponibles (vive en `banner_moleculas/molecula_<nombre>_horizontal.html`): `promo`, `creditos`, `textoxl`, `texto_M`, `img_automatica`, `texto_complementario`, `texto_pastilla`, `cta_interno`.

```html
<a role="horizontal" href="AQUIELLINKDELBANNER" style="text-decoration:none; display:block;">
<table id="BANNER_HORIZONTAL" width="480" style="width:480px; margin:0 auto;">
  <tr valign="middle">
    <td style="background-image:url({{bg_bannerimg_mail_general}}); border-radius:16px; overflow:hidden;">
      <div style="background:{{bg_bannertono_mail_general}}; max-width:480px; overflow:hidden;">
        <table width="240" align="left"><tr><td style="padding:{{padd_banner_mail_general}}">
          <!-- MOLECULA PROMOS / CREDITOS / TEXTO XL / TEXTO M / IMG AUTOMATICA / CTA INTERNO -->
        </td></tr></table>
        <!-- MODULO IMG: FIJA o AUTOMÁTICA, nunca ambas -->
        <!-- MODULO TAGS: fijo abajo -->
      </div>
    </td>
  </tr>
</table>
</a>
```

### 6.3 · Módulo Título

**Archivo:** `04_content-modules/title/modulo-titulo.html`

H2 Título + H3 bloque de texto, con `molecula-separador` opcional entre ambos. Alineado vía `{{body_alineado_molecular}}` (left/center). Se pueden agregar más moléculas, siempre separadas por el separador. Fondo apagado por defecto (encendido por defecto solo en Pro/ProBlack). Módulo clickeable opcional.

```
Alineado: left              Alineado: center (+ separador)
Título del módulo             Título del módulo
Bloque de texto...              ──── (separador)
                                Bloque de texto...
```

**Elementos editables:** TÍTULO (H2, `molecula-texto`) · SEPARADOR (`molecula-separador`, opcional) · BLOQUE DE TEXTO (H3, `molecula-texto`) · + moléculas · FONDO · LINK MÓDULO.

```html
<a href="LINKMODULO">
<div style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}};">
  <table role="module" data-type="text" width="100%" style="max-width:480px;">
    <tr><td>
      <h2 role="molecula-texto" style="text-align:{{body_alineado_molecular}};">Titulo</h2>
      <div role="molecula-separador" style="margin-bottom:10px;">
        <div style="height:10px; width:50px; border-bottom:1px solid; border-color:{{color_acento1_mail_general}};"></div>
      </div>
      <h3 role="molecula-texto">bloque de texto</h3>
    </td></tr>
  </table>
</div>
</a>
```

### 6.4 · Deals en Columnas

**Archivo:** `04_content-modules/deals/deal_columnas.html` — reemplaza a los backups `deal-large.backup.html` / `deal-small.backup.html`, ya no usados.

Los deals vienen en **PARES** en una grilla de 2 celdas (50/50). Cada celda tiene bloque de imagen (overlay + producto + logo opcional) y bloque de texto (título, descuento, rating, tags, CTA). Cuando el número de deals es **IMPAR**, se elimina todo el contenido de la celda derecha — la celda permanece vacía pero la grilla no se rompe. Pensado para promociones frecuentes en la app: da espacio para destacar tanto la promo como el restaurante/comercio.

```
Par (2 deals):                     Impar (celda derecha vacía):
┌────────┬────────┐               ┌────────┬────────┐
│ deal 1   │ deal 2   │               │ deal 1   │ (vacía)  │
│ $999     │ $999     │               │ $999     │          │
│ ⭐4.9     │ ⭐4.9     │               │ ⭐4.9     │          │
└────────┴────────┘               └────────┴────────┘
```

**Anatomía:** grilla fija 2 celdas, 3 filas (IMÁGENES / TEXTOS / LEGALES) · celda imagen con overlay + producto (reemplazable) + logo opcional (`molecula-iconoL` 50px) · celda texto con cada línea independiente y removible sin afectar la celda · colores 100% por tema · título con `href="LINKDEAL"` activo por defecto (único módulo de contenido con link activo de fábrica).

**Elementos editables (por celda):** línea 1 (título, bold) · línea 2 (descripción) · MARKDOWN (descuento + ícono Corona Pro togglable) · COMPLEMENTO 1 (ej. "99% OFF") · COMPLEMENTO 2 (ej. "| Antes $999") · TEXTOS RATING → CATEGORIA + RATING + TIEMPO (independientes) · TAG1/TAG2 (`molecula-tag`, ícono removible) · CTA · LEGALES (fila aparte, off por defecto).

```html
<table role="module" width="100%" style="table-layout:fixed; max-width:480px;">
  <!-- SECCION IMAGENES: 2 tds 50% c/u, overlay + producto + molecula-iconoL -->
  <tr><td width="50%">
    <a href="LINKDEAL">
      <div style="background:{{bg_solid_mail_general}}; border-radius:{{body_container_background_radius-peq}};">
        <h4 role="molecula-texto"><strong>{{deals_copy_1_promo}}</strong></h4>
        <h4 role="molecula-texto">{{deals_copy_2_promo}}</h4>
        <h4 role="MARKDOWN">👑 $999</h4>
        <h5 role="COMPLEMENTO 1">99% OFF</h5>
        <h5 role="COMPLEMENTO 2">| Antes $999</h5>
        <div role="TEXTOS RATING"><h5 role="CATEGORIA">Italiana</h5><h5 role="RATING">⭐ 4.9</h5><h5 role="TIEMPO">⏱ xx min.</h5></div>
        <div role="molecula-tag">🏷 tag 1</div><div role="molecula-tag">🏷 tag 2</div>
        <h4>Pide ahora ⤍</h4>
      </div>
    </a>
  </td><td width="50%"><!-- CELDA 2, mismo patrón, se puede vaciar --></td></tr>
  <!-- SECCION LEGALES: off por defecto -->
</table>
```

### 6.5 · Módulo Cupones

**Archivo:** `04_content-modules/coupons/cupones-modulo.html`

Los cupones siempre vienen de a **PARES** en una tabla de 2 celdas — por cada par se repite la tabla completa. Cada celda de cupón: imagen de producto (reemplazable) + línea punteada fija + pastilla/texto + markdown grande + separador + bullet, sobre un fondo que **SIEMPRE está activo** (no se puede desactivar) y con alineado **fijo** (solo los pesos de texto se pueden cambiar). La celda 1 puede reemplazarse por la celda suelta `celda_cupon_titulo.html` (`role="titulocupon"`), dejando la celda 2 como cupón normal. **No es el mismo patrón que [6.3 Módulo Título](#63--módulo-título)** — tiene su propia estructura: línea punteada arriba Y abajo (ninguna removible), tag con ícono (`molecula-tag`, ícono cambiable/removible), y un H1 título grande.

```
Cupón + Cupón:                     Título + Cupón:
┌─────────┬─────────┐            ┌─────────┬─────────┐
│ [img]      │ [img]      │            │ ┄┄┄┄┄┄┄┄┄┄ │ [img]      │
│ Solo en    │ Solo en    │            │ (●) tag 1   │ Solo en    │
│ Restaurante│ Restaurante│            │ Aca un      │ Restaurante│
│ $5 OFF     │ $5 OFF     │            │  título     │ $5 OFF     │
│ • Cupón xx │ • Cupón xx │            │ ┄┄┄┄┄┄┄┄┄┄ │ • Cupón xx │
└─────────┴─────────┘            └─────────┴─────────┘
                                    (celda_cupon_titulo.html)
```

**Elementos editables — celda cupón:** imagen de producto · línea punteada (`{{body_container_img_dots}}`, NO removible) · pastilla + texto ("Solo en"/"Restaurantes", cada uno apagable) · MARKDOWN (H1, color `{{color_acento2_mail_general}}`) · separador-S · bullet (ícono removible + texto) · + moléculas.

**Elementos editables — celda título (`celda_cupon_titulo.html`):** línea punteada arriba y abajo (ambas NO removibles) · tag con ícono (`role="molecula-tag"`, ícono cambiable — si se quita, se elimina toda la molécula) · H1 título (`role="molecula-texto"`) · link opcional vía `<a href="LINKTITULO">`.

```html
<table role="module" width="100%" style="table-layout:fixed; max-width:480px;">
  <tr>
    <td role="cupon" width="50%" style="background:{{bg_contenedor1_mail_general}};">
      <a href="LINKCUPON">
        <img role="imagenfull" width="100%" src="PRODUCTO.png">
        <img width="100%" src="{{body_container_img_dots}}">
        <table><tr>
          <th style="background:{{bg_tag_contenedor_mail_general}}; border-radius:30px;"><h5 role="molecula-texto">Solo en</h5></th>
          <th><h5 role="molecula-texto">Restaurantes</h5></th>
        </tr></table>
        <h1 role="molecula-texto" style="color:{{color_acento2_mail_general}};">Aca un<br>markdown</h1>
        <div class="separador-S"></div>
        <table><tr><td><img role="molecula-iconoS" width="15"></td><td><h4 role="molecula-texto">Cupón xxxxxxxxxxx</h4></td></tr></table>
      </a>
    </td>
    <td role="cupon" width="50%"><!-- CELDA 2: mismo patrón, siempre cupón --></td>
  </tr>
  <!-- SECCION LEGALES: off por defecto -->
</table>
<!-- si hay otro par, se repite la tabla completa -->
```

### 6.6 · Módulo Bullet

**Archivo:** `04_content-modules/bullet/modulo_bullet.html`

Celda 1 = ícono (`molecula-iconoXL`, intercambiable por S/M/L) + celda 2 = H3 Subtítulo + separador + H4 bloque de texto. La celda derecha está **ABIERTA**: se pueden agregar más moléculas, siempre separadas por un separador. Se puede usar **con o sin fondo** (`{{bg_contenedor1_mail_general}}`). Módulo clickeable opcional.

```
Con fondo:                       Sin fondo:
┌────────────────────┐          ┌────────────────────┐
│[ícono] Subtítulo      │          │[ícono] Subtítulo      │
│         bloque de texto│          │         bloque de texto│
│         + molécula     │          │         + molécula     │
└────────────────────┘          └────────────────────┘
```

**Elementos editables:** ÍCONO (intercambiable) · SUBTÍTULO (H3) · SEPARADOR · BLOQUE DE TEXTO (H4) · + moléculas · FONDO · LINK MÓDULO.

```html
<a href="LINKMODULO">
<div style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}}; overflow:hidden; max-width:480px;">
  <table role="componente" style="margin:{{alineado_molecular_mail_body}}; padding:{{body_container_background_padding}};">
    <tr>
      <td width="50px" valign="top"><img role="molecula-iconoXL" width="60px" style="border-radius:7px;"></td>
      <td valign="middle" style="padding-left:7px;">
        <h3 role="molecula-texto">Subtitulo</h3>
        <div class="separador-S"></div>
        <h4 role="molecula-texto">bloque de texto</h4>
      </td>
    </tr>
  </table>
</div>
</a>
```

> ⚠ **Inconsistencia real:** la tabla exterior usa `role="componente"`, mientras que todos los demás módulos de contenido de esta página (Título, Deals, Cupones, 1 Columna, Dos Columnas, Logos, 3 Columnas) usan `role="module"`. Parece un remanente de antes de que Bullet se normalizara — el resto de la molécula (ícono, texto, tema) sí está actualizado.

### 6.7 · Módulo Beneficios

**Archivo:** `04_content-modules/benefits/modulo-beneficios.html`

Celda 1 = imagen (`imagen-auto`, reemplazable) + celda 2 (`role="celda2"`) = ícono + subtítulo + texto, todo separado por separadores. La proporción de las 2 celdas **cambia** entre desktop y mobile: en desktop la celda de imagen es más angosta que la de texto (40/60), en mobile ambas pasan a 50/50 (`.beneficios-mob`). El fondo del contenedor es opcional. La celda 2 está **ABIERTA**.

```
Desktop (40/60, con fondo):        Mobile (50/50, sin fondo):
┌──────┬──────────────┐          ┌───────┬───────┐
│imagen  │[ícono]           │          │ imagen  │[ícono]  │
│-auto   │Descuentos de xxx │          │ -auto   │Descuento│
│(40%)   │En todos tus...     │          │ (50%)   │En todos │
└──────┴──────────────┘          └───────┴───────┘
```

**Elementos editables:** IMAGEN (celda 1) · ÍCONO (celda 2, `molecula-iconoM`) · SUBTÍTULO (H3) · BLOQUE DE TEXTO (H4) · + moléculas · FONDO · LINK MÓDULO.

```html
<a href="LINKMODULO">
<div style="border-radius:{{body_container_background_radius}}; overflow:hidden; border:{{body_container_background_border}};">
  <table role="module" width="100%" style="max-width:480px; background:{{bg_contenedor1_mail_general}};">
    <tr style="background-image:url({{img_fondo_especial_mail_general}});">
      <td width="40%" class="beneficios-mob" style="padding:{{body_container_background_padding}};">
        <img role="imagen-auto" width="100%" style="border-radius:8px;">
      </td>
      <td role="celda2">
        <img role="molecula-iconoM" width="25" style="margin:{{alineado_molecular_mail_body}};">
        <div class="separador-S"></div>
        <h3 style="text-align:{{body_alineado_molecular}};">Descuentos de hasta xxx</h3>
        <div class="separador-S"></div>
        <h4 style="text-align:{{body_alineado_molecular}};">En todos tus pedidos, desde $XXXXXX</h4>
      </td>
    </tr>
  </table>
</div>
</a>
```

> ⚠ **Auditoría (en el archivo real):** hay un `<h5 role="componente">` vacío entre los dos separadores (línea 33) — parece un slot de molécula sin usar, no texto real.

### 6.8 · Módulo 1 Columna

**Archivo:** `04_content-modules/1columna/modulo-1columna.html`

Uno o varios bloques `divcomponentes` (moléculas separadas por `separador-M`) y, aparte, una imagen full-width (`imagen-auto`) opcional. Ambos bloques se pueden mover, duplicar u omitir libremente — combinaciones como Moléculas+Imagen, Imagen+Moléculas, Moléculas+Imagen+Moléculas. Mantiene una sola columna en desktop y mobile (no cambia de estructura). Fondo opcional, colores 100% por tema.

```
Moléculas+Imagen:      Imagen+Moléculas:       Moléculas+Imagen+Moléculas:
┌────────────┐        ┌────────────┐         ┌────────────┐
│ MOLÉCULAS    │        │ IMAGEN full  │         │ MOLÉCULAS    │
├────────────┤        ├────────────┤         ├────────────┤
│ IMAGEN full  │        │ MOLÉCULAS    │         │ IMAGEN full  │
└────────────┘        └────────────┘         ├────────────┤
                                                │ MOLÉCULAS    │
                                                └────────────┘
```

**Elementos editables:** `divcomponentes` (bloque de moléculas) · moléculas (separadas por `separador-M`) · `imagen-auto` (opcional, se elimina la etiqueta completa si no se usa) · orden · FONDO · LINK MÓDULO.

```html
<a href="LINKMODULO">
<div style="display:inline-block;">
  <table role="module" width="100%" style="table-layout:fixed; max-width:480px;">
    <tr><td>
      <div role="contenedorgeneral" style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}}; overflow:hidden;">
        <div role="divcomponentes" style="padding:{{body_container_background_padding}};"><!-- moléculas --></div>
        <img role="imagen-auto" width="100%">
        <div role="divcomponentes" style="padding:{{body_container_background_padding}};"><!-- más moléculas --></div>
      </div>
    </td></tr>
  </table>
</div>
</a>
```

### 6.9 · Módulo Dos Columnas

**Archivo:** `04_content-modules/2columnas/modulo-2-columnas.html`

Celda imagen + celda de moléculas (`molecula-texto`), en el orden que se necesite. Se **DUPLICA** la tabla completa: una versión `class="mobile_hide"` (2 columnas lado a lado en desktop) y otra `class="desktop_hide"` (una celda debajo de la otra en mobile) — cualquier cambio se aplica a **AMBAS** versiones. El fondo del contenedor y el de la imagen se pueden quitar de forma independiente.

```
Desktop (Imagen+Texto):          Desktop (Texto+Imagen):
┌────────┬────────┐            ┌────────┬────────┐
│ IMAGEN   │ Título   │            │ Título   │ IMAGEN   │
└────────┴────────┘            └────────┴────────┘

Mobile (apilado):
┌────────────┐
│ IMAGEN        │
├────────────┤
│ Título          │
│ bloque de texto │
└────────────┘
```

**Regla crítica:** se inserta 2 veces (`mobile_hide` = desktop, `desktop_hide` = mobile) · ⚠ si son N módulos en la fuente, se inserta 2N en HTML · contenido idéntico obligatorio en ambas versiones · orden de celdas intercambiable, igual en ambas.

**Elementos editables:** ORDEN DE CELDAS · IMAGEN (full sin padding, o ancho modificable `{{body_img_modulo_auto_ancho}}%` max 240px con padding) · columna-textos (H2+separador+H3, admite varias moléculas) · FONDO CONTENEDOR · FONDO IMAGEN (independiente) · ALINEADO · LINK MÓDULO (`href="LINKMODULOCOULUMNAS"` — así está escrito en el archivo real, con el typo).

```html
<a href="LINKMODULOCOULUMNAS">
<div style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}}; overflow:hidden;">
  <table class="mobile_hide" role="module" width="100%" style="max-width:480px;">
    <tr>
      <td role="columna-textos">
        <h2 role="molecula-texto" style="text-align:{{body_alineado_molecular}};">Titulo</h2>
        <div role="molecula-separador"></div>
        <h3 role="molecula-texto">bloque de texto</h3>
      </td>
      <td width="50%" style="background-image:url({{img_overlay_2_mail_general}}); border-radius:10px;">
        <img width="100%" style="border-radius:12px;">
        <div style="padding:10px;"><img style="width:{{body_img_modulo_auto_ancho}}%; max-width:240px;"></div>
      </td>
    </tr>
  </table>
  <table role="module" class="desktop_hide" width="100%">
    <tr><td role="columna-textos"><!-- mismas moléculas --></td></tr>
    <tr><td width="100%"><!-- misma celda de imagen --></td></tr>
  </table>
</div>
</a>
```

### 6.10 · Módulo Logos

**Archivo:** `04_content-modules/logos/modulo-logos.html` + `grilla3/4/6logos.html`

Se comporta igual que Módulo Dos Columnas — se duplica la tabla completa. En desktop se ven 2 celdas lado a lado: moléculas + grid de logos (la celda de logos es más ancha, 60% vs 40%). En mobile ambas celdas se apilan. La celda de logos acepta grillas de 3, 4 o 6 logos (solo una por instancia).

```
Desktop (40/60):                  Mobile (apilado):
┌──────┬────────────┐           ┌────────────┐
│Título   │ [L1][L2][L3]│           │ Título          │
│bloque   │  (60%)         │           │ bloque de texto │
│(40%)    │              │           ├────────────┤
└──────┴────────────┘           │ [L1][L2][L3]    │
                                    └────────────┘
```

**Reglas:** insertado 2 veces (mismo patrón que Dos Columnas) · grillas válidas: 3 (3×1), 4 (2×2, tabla `thead`/`th` distinta), 6 (3×2) — solo una por instancia · 5 logos → se usa la grilla de 6, la 6ª celda queda con el fondo placeholder (no se quita ni se modifica) · orden de celdas intercambiable · fondo removible · clickeable completo o logo a logo.

> Cada `<td>` de logo tiene 2 imágenes: el `background-image` (el logo real, reemplazable) y un `<img>` vacío dentro del `<a>` que **no se quita ni se modifica**.

**Elementos editables:** ORDEN DE CELDAS · GRID DE LOGOS (3/4/6) · LOGO (`background-image`, radio 7px) · columna-textos · FONDO · CLICKEABLE (completo o por logo) · LINK MÓDULO.

```html
<a href="LINKMODULLOGOS">
<div style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}}; overflow:hidden;">
  <table class="mobile_hide" role="module" width="100%" style="max-width:480px;">
    <tr>
      <td role="columna-textos"><h2 role="molecula-texto">Titulo</h2><div role="molecula-separador"></div><h3 role="molecula-texto">bloque de texto</h3></td>
      <td width="60%">
        <!-- INSERTAR SOLO UNA GRILLA: grilla3/4/6logos.html -->
        <table><tr>
          <td role="logo1" style="background-image:url(LOGO1.png); border-radius:7px;">
            <a href="AQUIELLINKDELOGO1"><img style="width:100%;" alt="LOGO"></a>
          </td>
          <td role="logo2">...</td><td role="logo3">...</td>
        </tr></table>
      </td>
    </tr>
  </table>
  <table role="module" class="desktop_hide" width="100%">
    <tr><td role="columna-textos"><!-- mismas moléculas --></td></tr>
    <tr><td width="100%"><!-- misma grilla --></td></tr>
  </table>
</div>
</a>
```

### 6.11 · Módulo 3 Columnas

**Archivo:** `04_content-modules/3columnas/modulo-3-columnas.html`

3 celdas idénticas, en desktop **y** mobile (no cambia de estructura). Cada celda = contenedor de moléculas (`molecula-iconoM` + separador + H4 texto corto) + una imagen que ocupa el 100% de la celda, debajo. Ambos son opcionales/removibles. El fondo se puede quitar **celda por celda** (nunca las 3 a la vez). Cada celda puede ser clickeable de forma independiente.

```
┌─────────┬─────────┬─────────┐
│[ícono]     │[ícono]     │[ícono]     │
│Compra fácil│Llega rápido│Sin tarifa   │
│[IMG 100%]  │[IMG 100%]  │[IMG 100%]  │
│(con fondo) │(con fondo) │(SIN fondo) │
└─────────┴─────────┴─────────┘
```

**Recomendaciones:** usar moléculas pequeñas y textos cortos (en mobile las 3 celdas se ven muy chicas) y que las 3 imágenes midan lo mismo entre sí.

**Elementos editables:** ÍCONO (`molecula-iconoM`, 25px) · TEXTO (H4, corto) · IMAGEN FULL (100%, opcional) · FONDO (por celda) · CLICKEABLE (por celda, `LINKCELDA{n}`) · ALINEADO.

```html
<table role="module" width="100%" style="table-layout:fixed; max-width:480px;">
  <tr>
    <td valign="top">
      <a href="LINKCELDA1">
        <div role="contenedorgeneral" style="background:{{bg_contenedor1_mail_general}}; border-radius:{{body_container_background_radius}}; overflow:hidden;">
          <div role="divcomponentes" style="display:table; padding:{{body_container_background_padding-peq}};">
            <img role="molecula-iconoM" width="25" style="margin:{{alineado_molecular_mail_body}};">
            <div class="separador-S"></div>
            <h4 role="molecula-texto" style="text-align:{{body_alineado_molecular}};">Texto corto</h4>
          </div>
          <img width="100%" alt="-">
        </div>
      </a>
    </td>
    <td valign="top"><!-- CELDA 2 --></td>
    <td valign="top"><!-- CELDA 3 --></td>
  </tr>
</table>
```

### 6.12 · Footer: General, Sin Amor, RTS

Existen 3 archivos de footer, cada uno para un caso de uso distinto. Los 3 resuelven legales, URLs y copies dinámicamente según el país del usuario (`{{user_id contains 'XX'}}`; si no detecta país → `{% abort_message %}`).

```
General:                    Sin Amor:                   RTS (Repartidores):
┌──────────────┐          ┌──────────────┐          ┌──────────────┐
│ "Hecho con Amor" │          │ (sin imagen)     │          │ "Hecho con Amor" │
│ [WhatsApp]         │          │ (sin botón WA)   │          │ [WA][Telegram]   │
│ texto legal Pro    │          │ texto legal Pro   │          │ (sin texto Pro)  │
│ Ayuda|Privac|TyC|  │          │ Ayuda|Privac|TyC| │          │ Ayuda|Privac|TyC │
│  Cancelar          │          │  Cancelar          │          │  Cancelar        │
│ Recibiste...|TyC   │          │ Recibiste...|TyC   │          │ Legal_blog+blog. │
│ Legal Turbo/Liquor │          │ Legal Turbo/Liquor │          │ "Soy Rappi"      │
└──────────────┘          └──────────────┘          └──────────────┘
```

Los 3 tienen una variante de estilo **"pro"**: en **General** y **Sin Amor**, `'pro'` solo agrega un texto legal de membresía (no cambia estructura); en **RTS**, `'pro'` **solo cambia colores** — no agrega ningún texto legal (a diferencia de los otros dos).

#### A · Footer General — `06_footer/footer_general.html`

El más usado: se aplica a **toda comunicación dirigida a usuarios** (promociones, transaccionales, marketing general).

**Estilos visuales (`color_footer`)** — 2 valores, disparados desde `head-meta-tags.html` según el tema:

| Variable | `'negro'` (default) | `'pro'` |
|---|---|---|
| color_letra | #7D8188 | #7D8188 |
| color_textwa | #52ca2d | #F49502 |
| color_bordewa | #52ca2d 2px | #F49502 2px |
| color_fondowa | rgba(115,195,91,0.2) | rgba(244,149,2,0.0) |
| show_hr | false | true |
| color_membresia | — | #7D8188 |

Temas: `negro` → Pastel (Beige, Rosa, Púrpura, Celeste, Verde) + Dark (Darkneon, Darkturbo, Darkneutro). `pro` → Pro, ProBlack.

**Bloques condicionales:**

| Bloque | Condición | Notas |
|---|---|---|
| Logo Rappi superior | siempre | asset cambia por `color_footer` |
| WhatsApp banner | opcional | border 2px solid, "ÚNETE/UNITE/JUNTE-SE" según país |
| Centro de ayuda | siempre | mismo URL para todos los países |
| Aviso de privacidad | siempre | URL específica por país |
| Términos y Condiciones | siempre | URL específica por país |
| Cancelar suscripción | solo si `{% show_unsubscribe %}` | copy traducido por país |
| Legal turbo | si `{% show_legal_turbo == true %}` | copy legal RappiTurbo |
| Legal liquor | si `{% show_legal_liquor == true %}` | copy o imagen (según país) |
| Membresía Pro | solo si `color_footer == 'pro'` | sin Brasil; copy específico por país |

**Tabla de variables por país — Footer General** (idéntica para Sin Amor, mismo bloque LEGALES):

| País | WhatsApp (copy → texto → link) | Legal Turbo | Legal Liquor | Legales (aplican_tyc / bottom_line_1 / bottom_line_2) |
|---|---|---|---|---|
| AR | "Encontrá promos exclusivas..." → ¡UNITE ACÁ! → `whatsapp.com/channel/0029VazNdlY...` | *El tiempo de entrega puede variar según clima y tráfico. (sin URL) | Beber con moderación. Prohibida su venta a menores de 18 años. | Aplican TyC \| Recibiste este mail porque sos nuestro usuario. \| © Rappi ARG S.A.S. |
| BR | "Entre no canal e descubra promoções exclusivas" → JUNTE-SE AQUI → `whatsapp.com/channel/0029VbABTy...` | *Consulte disponibilidade na sua região. | Aprecie com moderação. Venda e consumo proibidos para menores de 18 anos. Se beber não dirija. | Aplicam-se T&C \| Você recebeu este e-mail porque está cadastrado na nossa base. \| © Rappi Brasil Intermediação de Negócios LTDA. |
| CO | "Encuentra promos exclusivas..." → ÚNETE AQUÍ → `whatsapp.com/channel/0029VazYoNj...` | *Tiempo estimado, depende de clima y tráfico: (con URL propia) | El exceso de alcohol es perjudicial para la salud. Ley 30/1986. Prohibido a menores y mujeres embarazadas. Ley 124/1994. | Aplican TyC \| Recibiste este mail porque eres nuestro usuario. \| © RAPPI S.A.S. |
| CL | "Encuentra promos exclusivas..." → ÚNETE AQUÍ → `whatsapp.com/channel/0029Vb7ux1c...` | *Puede variar según clima, tráfico u otros factores. (con URL propia) | `legal_liquor_img` — imagen especial `{{$imgchile}}`, no texto | Aplican TyC \| Recibiste este mail porque eres nuestro usuario. \| © Rappi Chile SpA. |
| CR | "Encontrá promos exclusivas..." → ¡UNITE ACÁ! → deeplink `"#"` (sin canal real) | `""` (vacío — sin copy de Turbo) | El exceso de alcohol es nocivo para la salud. | Aplican TyC \| Recibiste este mail porque sos nuestro usuario. \| © Rappi Pura Vida S.A. |
| EC | "Encuentra promos exclusivas..." → ÚNETE AQUÍ → `whatsapp.com/channel/0029Vb09QNe...` | *Puede variar según clima/tráfico/otros. + 2 sub-variantes: Turbo Super / Turbo Restaurantes (URLs propias) | Advertencia: consumo excesivo de alcohol puede perjudicar la salud. Ministerio de Salud Pública del Ecuador. | Aplican TyC \| Recibiste este mail porque eres nuestro usuario. \| © Rappiec S.A. |
| MX | "Encuentra promos exclusivas..." → ÚNETE AQUÍ → `linktr.ee/rappimx...` | *Puede variar... (Turbo súper solo en CDMX, Monterrey, Guadalajara, Puebla y Mérida) | El abuso en el consumo de este producto es nocivo para la salud. | Aplican TyC \| Recibiste este mail porque eres nuestro usuario. \| © Tecnologías Rappi S.A.P.I. de C.V. |
| PE | "Encuentra promos exclusivas..." → ÚNETE AQUÍ → `whatsapp.com/channel/0029Vb4K60y...` | *Tiempo estimado, según demanda/tráfico/otros. + 2 sub-variantes: Turbo Super / Turbo Restaurantes | TOMAR BEBIDAS ALCOHÓLICAS EN EXCESO ES DAÑINO. (letter-spacing especial en el render) | Aplican TyC \| Recibiste este mail porque eres nuestro usuario. \| © Rappi S.A.C. |
| UY | "Encontrá promos exclusivas..." → ¡UNITE ACÁ! → deeplink `"#"` (sin canal real) | *Puede variar según clima y tráfico. | Beber con moderación. Prohibida su venta a menores de 18 años. | Aplican TyC \| Recibiste este mail porque sos nuestro usuario. \| © Brisanier SA - Rappi Uruguay |

#### B · Footer Sin Amor — `06_footer/footer_sinamor.html`

Versión simple: sin canal de WhatsApp y sin la frase "Hecho con Amor en Latinoamérica" que abre el Footer General. Se usa para **comunicaciones más formales**.

**4 estilos visuales** (más que General, que solo tiene 2):

| Variable | `'negro'` (default) | `'cafe'` | `'pro'` | `'blanco'` |
|---|---|---|---|---|
| color_letra | #7D8188 | #633D11 | #7D8188 | #FFFFFF |
| show_hr | false | false | true | false |
| color_membresia | — | — | #7D8188 | — |
| background_colour | no seteado (blanco por defecto) | no seteado | no seteado | transparent |
| logo/bigote/img-amor | assets genéricos | assets café (logo propio) | assets Pro | assets blancos (+ `imgchile` en CL) |

Comparte exactamente los mismos valores de Legal Turbo / Legal Liquor / Legales por país que Footer General (ver tabla arriba — mismo bloque LEGALES, byte-idéntico).

> ⚠ **Auditoría:** las variables de WhatsApp (`color_textwa`, `color_bordewa`, `color_fondowa`, `walogo`, `wa-copy`, `wa-texto`, `deeplink_whatsapp`) se siguen asignando en el bloque STYLE LOOK/LEGALES, pero nunca se usan — el archivo no tiene botón de WhatsApp en el body. Lo mismo pasa con `img-amor`: se asigna en los 4 estilos pero tampoco se usa.

#### C · Footer RTS (Repartidores) — `06_footer/footer_rts.html`

Predeterminado para comunicaciones a **repartidores/colaboradores de delivery**. Son comunicaciones de la marca a los colaboradores, no a usuarios: los legales y los canales de comunicación que se mencionan son los de repartidores ("Soy Rappi" / "Rappi Entregador"), no los del footer de usuarios.

- Sí tiene la imagen "Hecho con Amor en Latinoamérica" (igual que General) — a diferencia de Sin Amor.
- Canal de comunicación variable **por país**: MX = WhatsApp + Telegram · BR = solo WhatsApp · CO = Telegram + Facebook · AR/CL/CR/EC/UY = solo Facebook.
- Legales propios: `Legal_blog` + link a `blog.[país]` + razón social firmada "Soy Rappi - [país]" o "Rappi Entregador - BR".
- Cancelar suscripción usa `{{${set_user_to_unsubscribed_url}}}` (no `preference_center` como en General/Sin Amor).

**3 estilos visuales** — `'pro'` aquí **solo cambia colores**, no agrega texto legal:

| Variable | `'negro'` (default) | `'pro'` | `'blanco'` |
|---|---|---|---|
| color_letra | #7d8188 | #A4A5A6 | #FFFFFF |
| color_textwa/bordewa | #52ca2d | #f8b76f | #52ca2d |
| color_texttg/bordetg | #1888C9 | #f8b76f | #1888C9 |
| color_textfb/bordefb | #2669F6 | #f8b76f | #2669F6 |
| show_hr | false | true | false |
| color_membresia | — | #D0D0D1 (asignada, pero `pro_membresia` nunca se muestra en el body) | — |

**Tabla de variables por país — Footer RTS:**

| País | Canal(es) mostrados | Razón social / Legal_blog | Blog URL |
|---|---|---|---|
| AR | Facebook: "Encontrá promos exclusivas..." → ¡UNITE ACÁ! | "Soy Rappi - AR" · © Rappi ARG S.A.S. | soyrappi.com.ar |
| BR | WhatsApp: "Entre no canal do WhatsApp pra promoções exclusivas" → ENTRE AQUI | "Rappi Entregador - BR" · © Rappi Brasil Intermediação de Negócios LTDA. | rappientregador.com.br |
| CL | Facebook: "Encuentra en el canal de Facebook promos exclusivas" → ÚNETE AQUÍ | "Soy Rappi - CL" · © Rappi Chile SpA. | soyrappi.cl |
| CO | Telegram + Facebook: "...promos exclusivas" → ÚNETE AQUÍ (ambos) | "Soy Rappi - CO" · © RAPPI S.A.S. | soyrappi.com.co |
| CR | Facebook: "Encontrá promos exclusivas..." → ¡UNITE ACÁ! | "Soy Rappi - CR" · © Rappi Pura Vida S.A. | soyrappi.co.cr |
| EC | Facebook: "Encuentra en el canal de Facebook promos exclusivas" → ÚNETE AQUÍ | "Soy Rappi - EC" · © Rappi Pura Vida S.A. (⚠ ver auditoría) | soy-rappi.com.ec |
| MX | WhatsApp + Telegram → ÚNETE AQUÍ (ambos) | "Soy Rappi - MX" · © Tecnologías Rappi S.A.P.I. de C.V. | soyrappi.com.mx |
| PE | ⚠ Ninguno se renderiza (variables de Facebook asignadas, sin bloque condicional que incluya PE) | "Soy Rappi - PE" · © Rappi S.A.C. | soyrappi.com.pe |
| UY | Facebook (⚠ deeplink apunta por error a una URL de WhatsApp) | "Soy Rappi - UY" · © Brisanier SA - Rappi Uruguay | soyrappi.com.uy |

---

## Hallazgos de auditoría (consolidado)

Lista única de inconsistencias encontradas en el código real durante esta revisión, documentadas tal cual (sin "corregir" el código sin confirmar con el equipo):

1. **Deals en Columnas (6.4):** typo "TESTOS RATING" debería ser "TEXTOS RATING" — aparece tanto en el label como en `role="TESTOS RATING"` del HTML real.
2. **Deals en Columnas (6.4):** usa placeholders `role` en MAYÚSCULAS ad-hoc (`MARKDOWN`, `COMPLEMENTO 1/2`, `CATEGORIA`, `RATING`, `TIEMPO`) en vez de la convención `molecula-*` en minúsculas usada en el resto del sistema.
3. **Módulo Dos Columnas (6.9):** el placeholder de link dice `LINKMODULOCOULUMNAS` (typo real en el archivo — debería ser `LINKMODULOCOLUMNAS`).
4. **Módulo Bullet (6.6):** tabla exterior usa `role="componente"` en vez de `role="module"` (única excepción a la convención en toda la página de Organismos).
5. **Módulo Beneficios (6.7):** hay un `<h5 role="componente">` vacío entre dos separadores — parece un slot de molécula sin usar, no contenido real.
6. **Footer Sin Amor:** variables de WhatsApp e `img-amor` se asignan en el bloque de estilos pero nunca se usan en el body — dead code heredado del Footer General.
7. **Footer RTS:** PE tiene variables de Facebook asignadas pero ningún bloque condicional del body las incluye — en la práctica PE no muestra ningún canal.
8. **Footer RTS:** los deeplinks de Facebook de PE y UY apuntan por error a una URL de `whatsapp.com` (probable copy-paste).
9. **Footer RTS:** la razón social de EC copia la de Costa Rica ("© Rappi Pura Vida S.A.") — posible error de copy-paste en el archivo fuente.
10. **Tabla de Cierre (5.4):** la regla "se omite en Pro/ProBlack" NO está implementada hoy en `template_maestro_original.html` — mismo hallazgo documentado en Foundations 1.4.
11. **Tabla de Cierre (5.4):** el propio contenido se autodescribe como "el último organismo" pese a estar numerado en la página de Moléculas — posible reclasificación pendiente, no resuelta unilateralmente acá.
12. **Moléculas de banner (5.2):** `molecula_textom_horizontal.html` y `molecula_texto_M_horizontal.html` (y sus pares `_vertical`) son archivos byte-idénticos — pendiente decidir cuál nombre se conserva y cuál se elimina.
13. **Etiquetas y badges (4.5):** el snippet de ícono+badge usa `role="MARKDOWN"` sobre un `<h4>` — inconsistente con `role="molecula-texto"`; verificar contra el `.html` real.
14. **CTAs base (4.6):** `style_Look='blanco'` es un alias legacy idéntico a `blanconeon` — no usar en código nuevo.

---

## Referencias cruzadas

- Figma — `Doc-DS-Mails`: página `04 · Atoms` (node `19:2`), página `05 · Molecules` (node `3:7`), página `06 · Organisms` (node `3:8`).
- Inventario de archivos actual: `05-docs/INDICE-DE-COMPONENTES.md`.
- Guía operativa por pieza: `05-docs/USO-DE-CADA-PARTE.md`.
- Escala tipográfica y reglas de spacers: Figma, página `02 · Tokens`, secciones 2.3 y 2.4.
- Estructura de carpetas operativa (`02-components/`): `02-components/README.md`.
