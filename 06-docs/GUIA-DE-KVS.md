# Guía completa de KVs

> **⚠️ OBSOLETO.** Esta guía documenta el esquema anterior de **5 KVs** (Genérico, Turbo, Neutro, Pro, ProBlack). Ese esquema **ya no se usa**: fue reemplazado por un sistema de **11 temas** (light/dark), implementado como variables Liquid en
> `01-foundations/global-styles/head-meta-tags.html` (sección `TEMAS`, condicionada por `tema_general`).
>
> Los 11 temas: **Pastel** (Beige 100, Beige 150, Rosa 100, Púrpura 100, Celeste 100, Verde 100), **Oscuros/invertidos** (Dark neon, Dark Turbo, Dark Neutro) y **Premium** (Pro, ProBlack). El mapeo KV↔CSS que esta guía anticipaba en la carpeta `04-variants/` nunca se completó de esa forma y esa carpeta fue eliminada del repositorio; el mecanismo real es el bloque Liquid mencionado arriba.
>
> El contenido de abajo queda como referencia histórica para entender mails ya producidos con el esquema viejo. **No lo uses para producir mails nuevos.**

Esta guía documenta cómo se aplicaban los 5 KVs (Key Visuals) del sistema J.A.R.V.I.S., antes de la migración al sistema de 11 temas.

---

## ¿Qué es un KV?

Un **KV (Key Visual)** es la "skin" visual del mail. Define los colores de fondo, los gradientes, los textos destacados, las imágenes de cierre y varias reglas particulares. Dos mails con los mismos componentes pero distinto KV se ven completamente diferentes.

El KV viene definido en la **fuente** que envía la persona que pide el mail (en la columna "Tipo de Kv" de la fuente). Los 5 KVs disponibles son:

| KV | Cuándo se usa | Característica visual |
|----|---------------|----------------------|
| **Genérico** | Mails generales de Rappi | Fondo oscuro con gradiente naranja-rojo Neon |
| **Turbo** | Mails de RappiTurbo | Fondo oscuro con gradiente verde-turquesa |
| **Neutro** | Mails sin marca dominante o multi-categoría | Fondo oscuro neutro, sin gradiente fuerte |
| **Pro** | Mails de RappiPro (claro) | Fondo oscuro con detalles dorados, textos blancos |
| **ProBlack** | Mails de RappiPro Black (oscuro) | Fondo claro con detalles dorados, textos negros |

> **Nota importante sobre Pro vs ProBlack:** El HTML base actualizado define Pro con fondo `#2A2B2B` (oscuro) y ProBlack con fondo `#ECEFF3` (claro). Esto puede sentirse contraintuitivo respecto al naming. Si tu fuente dice "Pro" o "ProBlack", **respeta exactamente el código del HTML base** y no inviertas los valores. Si encuentras una inconsistencia, repórtala al equipo en un issue.

---

## La regla mental antes de empezar

Cada vez que vayas a producir un mail, antes de tocar nada, responde estas tres preguntas:

1. **¿Cuál es el KV?** → de la fuente, columna "Tipo de Kv"
2. **¿Lleva cierre?** → solo si el KV NO es Pro/ProBlack y la fuente no dice "sin cierre"
3. **¿Qué `font_style_look` lleva el footer?** → `'negro'` para Genérico/Turbo/Neutro, `'pro'` para Pro/ProBlack

Si tienes estas tres respuestas claras desde el inicio, el resto del mail se arma solo siguiendo las reglas que vienen abajo.

---

## Las 7 zonas donde el KV afecta el HTML

Cuando aplicas un KV no estás cambiando "los colores del mail" en general. Estás aplicando reglas específicas en **7 zonas concretas** del HTML. Vamos zona por zona.

### Zona 1 — Background del body

El `<body>` tiene un `background-color` que cambia según el KV:

| KV | `background-color` |
|----|-------------------|
| Genérico | `#040404` (default) |
| Turbo | `#040404` (default) |
| Neutro | `#040404` (default) |
| **Pro** | `#2A2B2B` |
| **ProBlack** | `#ECEFF3` |

**Dónde está esta regla en el HTML base:** líneas 461-467 del template maestro, dentro del bloque `<style>`.

### Zona 2 — Background-image del wrapper (`.gradmobile`)

El gradiente principal del mail vive en una clase llamada `.gradmobile` que se aplica al wrapper. Cada KV tiene su propia URL de imagen:

| KV | URL del gradiente |
|----|------------------|
| Genérico | `https://lh3.googleusercontent.com/d/1rIa4_gp0V6xLfA1K3ipSWBFiTCWhuIb3` |
| Turbo | `https://lh3.googleusercontent.com/d/1H9gJ5jNpxyIlg7jPve-VafvLZhWDOeSF` |
| Neutro | `https://lh3.googleusercontent.com/d/1cxWexOAmboGIZePNaw43T_STs395wS8K` |
| Pro | `https://lh3.googleusercontent.com/d/1x630cZMTzzkDMhebuUutPEkWvL1ppPfW` |
| ProBlack | `https://lh3.googleusercontent.com/d/1ii-QN0RVxteKuS2cHWUr22ZyOZXZ2-JE` |

**Regla extra para Pro y ProBlack:** debes agregar a la clase `.gradmobile` el estilo `background-size: 100% 100% !important;` para que el gradiente cubra correctamente el mail completo.

**Dónde está esta regla:** líneas 613-628 del template maestro.

### Zona 3 — Background-image del header

El header tiene su propio background con una URL distinta por KV. Es la parte superior del mail donde va el logo:

| KV | URL del background del header |
|----|------------------------------|
| Genérico | `https://lh3.googleusercontent.com/d/19KdV3950aiUjZLKiWGguOfkv3S18e0ME` |
| Turbo | `https://lh3.googleusercontent.com/d/1_OEm4wzq5y0DssitaYtc01U9IGuhHHgc` |
| Neutro | `https://lh3.googleusercontent.com/d/15b2Dj9cVVtRrIXEJb4NZnOENgkIWx11E` |
| Pro | `https://lh3.googleusercontent.com/d/1gGi5QQh1U8rRltHxKbL1cWNZGg6QJhXw` |
| ProBlack | `https://lh3.googleusercontent.com/d/1-kA1lJ5jOUyU5QKrY-qgtAEmowq5nW5J` |

**Dónde está esta regla:** líneas 894-906 del template maestro.

### Zona 4 — Background y textos del banner

El big banner (horizontal, vertical o editorial) cambia varias cosas según el KV:

#### Background del banner

| KV | `background` |
|----|-------------|
| Genérico | `rgba(254,63,35,0.5)` + `background-image: url(...1qztlsm...)` (mantener imagen) |
| Turbo | `rgba(0,58,52,0.4)` + **quitar el `background-image`** |
| Neutro | `rgba(0,0,0,0.4)` + **quitar el `background-image`** |
| Pro | `rgba(42,43,43,1.0)` + **quitar el `background-image`** |
| ProBlack | `rgba(224,228,231,1.0)` + **quitar el `background-image`** |

#### Color de textos del banner (h1, h2, h3, h4, h5, h6, txts)

El default es `color: #E2E2E2` (blanco hueso). Pero cambia para Pro y ProBlack:

| KV | Color de textos del banner |
|----|---------------------------|
| Genérico | `#E2E2E2` (default) |
| Turbo | `#E2E2E2` (default) |
| Neutro | `#E2E2E2` (default) |
| **Pro** | `#FBFBFB` |
| **ProBlack** | `#040404` |

#### Tag del banner (la etiqueta superior)

Cuando hay tag, su `bgcolor` cambia:

| KV | `bgcolor` del tag |
|----|------------------|
| Genérico | default del template |
| Turbo | default del template |
| Neutro | default del template |
| Pro | `#D8D9D9` |
| ProBlack | `#D8D9D9` |

#### Border-radius adicional para Pro

Cuando el KV es **Pro**, hay que agregar `border-radius: 16px;` al `<td>` que contiene el banner.

**Dónde están estas reglas:** líneas 1189-1596 del template maestro (varían por tipo de banner).

### Zona 5 — Color de texto resaltado en el body

Cuando en la fuente hay un texto entre asteriscos `*texto*`, se envuelve en un `<span style="color: ...">` cuyo color depende del KV:

| KV | Color de texto resaltado |
|----|-------------------------|
| Genérico | `#FFEBC2` |
| Neutro | `#FFEBC2` |
| Turbo | `#F2ED93` |
| Pro | `#D6AB76` |
| ProBlack | `#D6AB76` |

> **Nota:** el HTML maestro original tiene un typo en esta sección (línea 235-236 dice "Turbo" dos veces). El segundo valor `#D6AB76` aplica a Pro/ProBlack según la lógica del resto del sistema (es el dorado/cobre de Pro).

### Zona 6 — Color del cuerpo de texto general

Los textos generales del body (no resaltados) llevan un color base que cambia solo para ProBlack:

| KV | Color de texto del body |
|----|------------------------|
| Genérico | `#E2E2E2` |
| Turbo | `#E2E2E2` |
| Neutro | `#E2E2E2` |
| Pro | `#E2E2E2` |
| **ProBlack** | `#1D1D1D` |

### Zona 7 — Reglas especiales para Pro y ProBlack

Esto es lo que vuelve a Pro/ProBlack distintos. Son los detalles "premium":

#### A) Módulo de título con padding y fondo

Cuando KV es **Pro** o **ProBlack**, al `<table>` del módulo de título hay que agregarle:
- `padding: 15px;`
- `background-color: #E4E8EE` (para Pro)
- `background-color: #2A2B2B` (para ProBlack)

#### B) Separador dorado debajo del subtítulo

En módulos de título y de contenido, después del subtítulo se agregan estas dos divs (solo para Pro/ProBlack):

```html
<div class="separador-M"></div>
<div style="width: 50px; border-top: 1px solid #DAA868; margin-bottom: 5px; margin: 0 auto;"></div>
```

El color `#DAA868` es el dorado/cobre característico de Pro.

#### C) Bullets numerados

En el bullet numerado, el `border-right` que separa el número del texto:

| KV | Color del border-right |
|----|----------------------|
| Genérico, Turbo, Neutro | `#E2E2E2` |
| Pro, ProBlack | `#DAA868` |

#### D) Value prop de cupones

En el módulo de cupones, el value prop (el texto grande tipo "$10.000 de descuento"):

| KV | Color del value prop |
|----|---------------------|
| Genérico, Turbo, Neutro | color destacado del KV correspondiente |
| Pro, ProBlack | `#DAA868` |

#### E) Tabla de cierre (eliminación total)

> **REGLA ESTRICTA DE CIERRE:** Si el KV es Pro o ProBlack, debes **ELIMINAR LA TABLA DEL CIERRE POR COMPLETO**, sin importar si la fuente envía un texto en la variable "Pide img". Esta sección NO existe para Pro ni ProBlack.

Para Genérico, Turbo y Neutro se conserva la tabla y se usa la URL correspondiente de la base de datos de assets.

#### F) Variable `font_style_look` del footer

En el footer hay una variable Liquid que cambia el estilo visual:

| KV | `font_style_look` |
|----|------------------|
| Genérico | `'negro'` |
| Turbo | `'negro'` |
| Neutro | `'negro'` |
| Pro | `'pro'` |
| ProBlack | `'pro'` |

---

## Tabla maestra de KVs · referencia rápida

| Zona | Genérico | Turbo | Neutro | Pro | ProBlack |
|------|----------|-------|--------|-----|----------|
| Background body | `#040404` | `#040404` | `#040404` | `#2A2B2B` | `#ECEFF3` |
| Texto destacado (`*texto*`) | `#FFEBC2` | `#F2ED93` | `#FFEBC2` | `#D6AB76` | `#D6AB76` |
| Texto general del body | `#E2E2E2` | `#E2E2E2` | `#E2E2E2` | `#E2E2E2` | `#1D1D1D` |
| Texto en banner | `#E2E2E2` | `#E2E2E2` | `#E2E2E2` | `#FBFBFB` | `#040404` |
| Tag del banner `bgcolor` | default | default | default | `#D8D9D9` | `#D8D9D9` |
| Imagen de cierre | SÍ | SÍ | SÍ | **NO** | **NO** |
| `font_style_look` footer | `'negro'` | `'negro'` | `'negro'` | `'pro'` | `'pro'` |
| Separador dorado en módulos | NO | NO | NO | SÍ (`#DAA868`) | SÍ (`#DAA868`) |
| Padding extra en módulo título | NO | NO | NO | SÍ (15px + bg `#E4E8EE`) | SÍ (15px + bg `#2A2B2B`) |

---

## Errores comunes al aplicar KVs

### Error 1 — Olvidarse de eliminar el cierre en Pro/ProBlack
**Cómo se manifiesta:** El mail Pro queda con la firma de Rappi al final, lo cual no corresponde a la línea Pro.

**Cómo evitarlo:** Antes de hacer cualquier otra cosa, si el KV es Pro o ProBlack, **elimina la tabla del cierre desde el primer momento**. No la dejes "para después".

### Error 2 — Aplicar el color de texto resaltado de Genérico a Turbo
**Cómo se manifiesta:** Los textos entre `*asteriscos*` quedan en color crema (`#FFEBC2`) cuando deberían ir en amarillo verdoso (`#F2ED93`).

**Cómo evitarlo:** Ten la tabla maestra de arriba siempre abierta cuando reemplaces los `<span style="color: ...">`.

### Error 3 — Olvidarse de cambiar `font_style_look` a `'pro'`
**Cómo se manifiesta:** El footer de un mail Pro tiene tipografía/estilo de Genérico.

**Cómo evitarlo:** El footer es lo último que se inserta. Antes de cerrar el HTML, vuelve al footer y revisa que el `font_style_look` corresponda al KV.

### Error 4 — No invertir el texto del banner en ProBlack
**Cómo se manifiesta:** Un mail ProBlack (fondo claro `#ECEFF3`) queda con los textos del banner en blanco hueso `#E2E2E2`, que casi no se leen.

**Cómo evitarlo:** Para ProBlack, todos los `<h1>` a `<h6>` y `<span class="txts">` del banner deben tener `color: #040404`.

### Error 5 — Mezclar reglas de Pro con reglas de ProBlack
**Cómo se manifiesta:** El mail tiene fondo de Pro pero detalles de ProBlack o viceversa.

**Cómo evitarlo:** No leas las reglas de Pro y ProBlack al mismo tiempo. Trabaja con UNA sola columna de la tabla maestra desde principio a fin.

### Error 6 — Olvidar el separador dorado en Pro/ProBlack
**Cómo se manifiesta:** Los módulos de título y contenido en mails Pro quedan sin el detalle del separador dorado de 50px que es la firma de la marca.

**Cómo evitarlo:** Después de cada subtítulo (`<h5>`) en un mail Pro/ProBlack, insertar las dos divs (separador-M + línea dorada). Si tu módulo no tiene subtítulo, no aplica.

---

## Qué reemplazó a este sistema

Todo lo de arriba era un proceso manual: leer comentarios condicionales y cambiar valores uno por uno por cada una de las 7 zonas. Ese proceso ya se automatizó, pero no como esta guía anticipaba (una carpeta `04-variants/` con un CSS por KV que se aplica como capa encima).

Lo que existe hoy es distinto: un bloque Liquid único en `01-foundations/global-styles/head-meta-tags.html` (sección `TEMAS`) con un `{% if tema_general == '...' %} ... {% endif %}` por cada uno de los **11 temas**. Dentro de cada rama se asignan las variables de ese tema (fondo, texto, acentos, contenedores, tags, imágenes, banner, legales, descuento/créditos) que el resto del HTML consume por variable, no por clase CSS aplicada encima.

Diferencias clave frente al esquema viejo:
- Son **11 temas**, no 5: Pastel (Beige 100, Beige 150, Rosa 100, Púrpura 100, Celeste 100, Verde 100), Oscuros/invertidos (Dark neon, Dark Turbo, Dark Neutro) y Premium (Pro, ProBlack).
- Cada tema define valores para **light y dark**, no un único set de colores.
- La resolución es por variable Liquid (`{% assign %}`), no por un `.css` que se inyecta encima del HTML.

Producir un mail con un tema hoy es: `opening.html + componentes + closing.html`, con `tema_general` fijando qué rama del bloque `TEMAS` resuelve las variables — no hay un archivo de skin separado que aplicar.

---

## Referencias cruzadas

- Para entender cómo se arma un mail completo: ver `06-docs/COMO-ARMAR-UN-MAIL.md`
- Para entender cada brick individualmente: ver `06-docs/USO-DE-CADA-PARTE.md`
- Para ver dónde está cada regla en el HTML original: ver `07-examples/template_maestro_original.html`
- Para el sistema de temas actual: ver la sección `TEMAS` en `01-foundations/global-styles/head-meta-tags.html`
