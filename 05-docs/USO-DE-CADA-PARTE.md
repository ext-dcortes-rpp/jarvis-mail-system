# Uso correcto de cada parte de J.A.R.V.I.S.

Esta guía explica brick por brick cómo se usa cada componente del sistema. Es la referencia operativa: si tienes dudas sobre cuándo usar qué componente o cómo combinarlos, busca aquí.

> Esta guía asume que ya leíste el README principal y entiendes la metáfora del LEGO. Si no, empieza por ahí.

---

## Índice

1. [Foundations · las reglas](#1-foundations--las-reglas)
2. [Headers · la identidad del remitente](#2-headers--la-identidad-del-remitente)
3. [Banners · la cabecera visual](#3-banners--la-cabecera-visual)
4. [CTAs · el botón de acción](#4-ctas--el-botón-de-acción)
5. [Deals · promociones de productos](#5-deals--promociones-de-productos)
6. [Coupons · cupones de descuento](#6-coupons--cupones-de-descuento)
7. [Benefits · beneficios del programa](#7-benefits--beneficios-del-programa)
8. [Content Modules · los bricks combinables del cuerpo](#8-content-modules--los-bricks-combinables-del-cuerpo)
9. [Closing · la imagen de cierre](#9-closing--la-imagen-de-cierre)
10. [Footer · el pie del mail](#10-footer--el-pie-del-mail)
11. [Orden recomendado de uso](#11-orden-recomendado-de-uso)

---

## 1. Foundations · las reglas

📁 `01-foundations/`

### ¿Qué es?
Las reglas que rigen a todos los bricks: tipografías, colores base, separadores, media queries. Nada de esto se inyecta como bloque visible — son los "estilos globales" que vienen escritos en el `<style>` del head del mail.

### ¿Cuándo se toca?
**Casi nunca.** Solo se modifica cuando hay un cambio estructural del sistema (nueva tipografía, nuevo tamaño de heading, nuevo separador). Cualquier cambio aquí afecta a TODOS los mails que existen y los que vendrán.

### ¿Cuándo se usa?
Siempre. Cada mail incluye `head-meta-tags.html` y `global-styles.html` en el `<head>`.

### Reglas críticas
- **No agregues clases nuevas aquí** sin discutirlo con el equipo.
- **No quites comentarios condicionales** — todavía quedan algunos con la nomenclatura anterior (`/* si Tipo de Kv = ... */`) en componentes no migrados; son la fuente de verdad hasta que se actualicen al sistema de temas.
- Si necesitas un color o un tamaño nuevo, primero pregunta al equipo de diseño si encaja en el sistema.

### Aplicar el tema
Las variables del tema (`bg_solid_mail_general`, `background-image` de `.gradmobile`, background del header, etc.) se aplican en las zonas correspondientes del mail según `GUIA-DE-TEMAS.md`. Consulta esa guía para los valores exactos y qué falta por migrar (sección "Estado actual / pendientes").

---

## 2. Headers · la identidad del remitente

📁 `02-components/headers/`

### Las 10 marcas disponibles

| Carpeta | Cuándo se usa |
|---------|---------------|
| `rappi/` | Mails generales de la marca Rappi |
| `rappi-travel/` | Mails de RappiTravel |
| `soyrappi/` | Mails de SoyRappi |
| `rappi-turbo/` | Mails de RappiTurbo (verticales rápidas) |
| `rappi-turbo-rest/` | Mails de RappiTurbo Restaurantes |
| `rappi-pro/` | Mails de RappiPro |
| `rappi-pro-black/` | Mails de RappiPro Black |
| `rappi-defensoria/` | Mails de Defensoría |
| `rappi-entregador/` | Mails de RappiEntregador |
| `contenido-aliado/` | Mails de contenido aliado |

### Regla #1 · Solo UNO por mail
Un mail tiene exactamente **un header**, nunca más, nunca menos. Lo eliges según la marca/vertical de la fuente — la elección es independiente del tema del mail (ver `GUIA-DE-TEMAS.md`).

### Regla #2 · Cada marca tiene 4 archivos: fondo × disposición
Dentro de la carpeta de la marca elegida, se usa exactamente 1 de estos 4 archivos:

| Archivo | Fondo | Disposición |
|---------|-------|--------------|
| `centrado-claro.html` | Claro | Logo · divider · cobranding, centrado |
| `centrado-oscuro.html` | Oscuro | Logo · divider · cobranding, centrado |
| `columnas-claro.html` | Claro | Logo a la izquierda, cobranding a la derecha, sin divider |
| `columnas-oscuro.html` | Oscuro | Logo a la izquierda, cobranding a la derecha, sin divider |

### Regla #3 · El cobranding tiene 4 tamaños
Cada header soporta estas variantes de cobranding, todas con la misma estructura (logo + tag del partner), cambiando solo el tamaño:

1. **Sin cobranding** — Solo el logo/divider. Es el modo por defecto.
2. **Cobranding S** (`cobranding-s`) — Tamaño pequeño.
3. **Cobranding M** (`cobranding-m`) — Tamaño mediano.
4. **Cobranding L** (`cobranding-l`) — Tamaño grande.

### El wrapper compartido
El archivo `_header-wrapper.html` (con guion bajo) es la **envolvente común a todos los headers**. Cuando armas un mail, el flujo es: insertas el wrapper, y dentro del wrapper insertas el `<tr>` de uno de los 40 archivos específicos (10 marcas × claro/oscuro × centrado/columnas).

---

## 3. Banners · la cabecera visual

📁 `02-components/banners/`

### Los 2 banners disponibles

| Archivo | Cuándo se usa |
|---------|---------------|
| `big-banner-horizontal.html` | Cuando el mail tiene módulos en el body además de CTA y cierre |
| `big-banner-vertical.html` | Cuando el mail solo tiene CTA y cierre (mail simple) |

`banner-editorial.html` y `_banner-section-close.html` se eliminaron del sistema.

### Regla #1 · Solo UNO por mail
Igual que el header, un mail tiene exactamente un banner.

### Regla #2 · Eliges según la composición del mail, no según el tema
El tema define los colores del banner; el **tipo de banner se elige según qué módulos tendrá el mail**:

- **¿El mail solo tiene CTA + cierre?** → big banner vertical
- **¿El mail tiene módulos de contenido, deals, cupones, beneficios?** → big banner horizontal

### Regla #3 · Las piezas internas del banner viven en `banner_atoms/`
📁 `02-components/banners/banner_atoms/` — piezas que se combinan dentro de cada banner. La mayoría vienen en pareja horizontal/vertical porque los tamaños de escritorio se aplican inline según en qué banner se insertan:

1. **`modulo_tags.html`** — Tag/etiqueta superior. Si la fuente no trae tag, se omite.
2. **`modulo_img_altofijo.html`** — Columna de imagen de alto fijo, para el banner horizontal.
3. **`modulo_creditos_horizontal.html`** / **`modulo_creditos_vertical.html`** — Texto vivo de créditos ("$XXX" + "DE REINTEGRO"), usa las clases `bnr-*`.
4. **`modulo_promo_horizontal.html`** / **`modulo_promo_vertical.html`** — Módulo de promo ("Ahora" + cifra).
5. **`modulo_textoxl_horizontal.html`** / **`modulo_textoxl_vertical.html`** — Texto vivo XL adicional, mismo comportamiento de tamaño que el módulo de promo.
6. **`modulo_textom_horizontal.html`** / **`modulo_textom_vertical.html`** — Texto vivo `.bnr-md`, tamaño fijo inline.
7. **`modulo_texto_complemento_horizontal.html`** / **`modulo_texto_complemento_vertical.html`** — Versión `<h2>` del mismo texto de `modulo_textom`.
8. **`modulo_img_automatica_horizontal.html`** / **`modulo_img_automatica_vertical.html`** — Imagen automática dentro del banner.
9. **`modulo_cta_interno_horizontal.html`** / **`modulo_cta_interno_vertical.html`** — CTA embebido dentro del banner.

`modulo_texto_complementario.html` (sin sufijo) es un placeholder de una versión anterior — pendiente de revisar si sigue haciendo falta ahora que existe `modulo_texto_complemento_horizontal/vertical.html`. `modulo_img_variable.html` y `modulo_texto_secundario.html` se eliminaron.

### Regla #4 · El banner cambia mucho según el tema
El banner es donde más reglas de tema se aplican: background-color, background-image, color de textos, bgcolor del tag, border-radius. Antes de armar el banner, consulta `GUIA-DE-TEMAS.md` para los valores exactos (los comentarios internos del banner todavía usan la nomenclatura anterior; los valores de referencia son los de esa guía).

---

## 4. CTAs · el botón de acción

📁 `02-components/ctas/`

### El único archivo: `cta-template.html`

Es un bloque Liquid con 3 variables:

```liquid
{% assign text_cta = 'Súper completo en 10 min' %}
{% assign deeplink_cta = '#' %}
{% assign style_Look = 'blanco' %}
{{content_blocks.${CTA-template}}}
```

### ¿Qué cambia entre un CTA y otro?

Solo el contenido de las 3 variables:
- **`text_cta`** — el texto del botón
- **`deeplink_cta`** — la URL a la que lleva el botón
- **`style_Look`** — el estilo visual del botón, que depende del fondo donde se inserta:

| Si el "Fondo" en la fuente es... | `style_Look` debe ser... |
|----------------------------------|--------------------------|
| Gris | `'blanco'` |
| Neon | `'blanco'` |
| Pro | `'pro'` |
| ProBlack | `'problack'` |

### Regla #1 · Puede haber varios CTAs en un mail
Un mail puede tener 1, 2 o 3 CTAs intercalados a lo largo del body. La fuente te dice cuántos y dónde.

### Regla #2 · Separadores alrededor del CTA
- **Después de un CTA** siempre va un `<div class="separador"></div>` ANTES del siguiente componente.
- **Excepción:** si justo debajo del CTA va el cierre, NO se inserta el separador.

### Regla #3 · El CTA siempre va con el `<div class="separador">` antes
Si el componente anterior es un módulo (`role="module"`), insertas el separador entre módulo y CTA.

---

## 5. Deals · promociones de productos

📁 `02-components/deals/`

### Los 2 tipos de deal

| Archivo | Cuándo se usa |
|---------|---------------|
| `deal-large.html` | Deal grande con imagen prominente, formato horizontal |
| `deal-small.html` | Deal compacto, formato reducido |

### Regla #1 · Máximo 4 deals por mail
Si la fuente trae más de 4 deals, el equipo de mails debe sugerir convertir los excedentes a módulos de contenido. No se ponen 8 deals en un mail.

### Regla #2 · Por cada deal, una tabla nueva completa
**No combines deals.** Cada deal es una tabla independiente. Si hay 3 deals, hay 3 tablas seguidas, cada una con su estructura completa.

### Regla #3 · No cambies la estructura, solo las variables
Los deals tienen variables Liquid del tipo `{% assign deal_recommendation_deeplink = '#' %}`. **Solo cambias el valor de las variables**, nunca eliminas líneas ni cambias la estructura HTML del deal.

### Regla #4 · Los deals NO necesitan separador antes ni después
A diferencia de módulos y CTAs, los deals tienen su propia "área de respeto" interna. No insertes `<div class="separador">` alrededor de deals.

---

## 6. Coupons · cupones de descuento

📁 `02-components/coupons/`

### El único archivo: `cupones-modulo.html`

Es una tabla que contiene **2 celdas por fila**. Cada celda es un cupón. Pueden ser:
- Dos cupones normales (cuando hay cantidad par)
- Un Cupón Title + un cupón normal (cuando hay cantidad impar y se necesita "balancear")

### Regla #1 · Los cupones siempre van en pares
Si hay 4 cupones, se insertan 2 tablas (cada una con 2 cupones). Si hay 6, se insertan 3 tablas. **Por cada 2 cupones, una tabla completa nueva.**

### Regla #2 · Cantidad impar = usar Cupón Title
Cuando la fuente trae cantidad impar de cupones (1, 3, 5...), la última celda se convierte en **Cupón Title**:
- Tiene `role="title"`
- Lleva un ícono y un título grande (ej: "Tus cupones del mes")
- Reemplaza a un cupón normal en esa celda

### Regla #3 · Las piezas internas de cada cupón
Un cupón normal puede tener:
- **Imagen top** — la imagen principal del cupón (mandatoria)
- **Tag** — etiqueta superior con día/horario (opcional, si no hay se elimina el `<th>`)
- **Vertical** — categoría del partner (opcional)
- **Value prop** — el texto grande tipo "$10.000 de descuento" (mandatorio)
- **Complemento** — texto adicional con ícono (opcional, si no hay se elimina el div completo)
- **Legal** — texto fino debajo (opcional, va en un `<tr>` aparte)

### Regla #4 · Color del value prop según KV
- Pro/ProBlack → `#DAA868` (dorado)
- Los demás → color destacado del KV correspondiente

### Regla #5 · Los legales viven en un `<tr>` aparte
Los legales NO van dentro del cupón. Van en una fila separada debajo de la fila principal, alineados al cupón al que pertenecen. Si solo un cupón tiene legal, la celda del otro va vacía.

---

## 7. Benefits · beneficios del programa

📁 `02-components/benefits/`

### El único archivo: `modulo-beneficios.html`

Es una **card horizontal** dividida en 2 columnas:
- Izquierda: imagen del beneficio
- Derecha: ícono + subtítulo + texto descriptivo

### Regla #1 · Por cada beneficio, una tabla nueva
Si la fuente trae 3 beneficios, se insertan **3 tablas de beneficios seguidas**, no se combinan en una sola.

### Regla #2 · Entre beneficios va un separador
Como cualquier módulo (`role="module"`), entre dos beneficios consecutivos va un `<div class="separador">`.

### Regla #3 · Piezas internas opcionales
Cada beneficio puede tener:
- **Imagen** del beneficio (mandatoria)
- **Ícono** pequeño arriba del subtítulo (opcional)
- **Subtítulo** (h5) (opcional, se elimina si no aplica)
- **Texto descriptivo** (opcional, se elimina si no aplica)

### Regla #4 · No cambies el `vertical-align`
Dentro del archivo hay comentarios que dicen `<!-- no cambies este vertical align -->`. Respétalos. El alineado vertical es parte del diseño y no debe modificarse.

---

## 8. Content Modules · los bricks combinables del cuerpo

📁 `02-components/content-modules/`

Esta es la carpeta más versátil. Aquí viven los bricks que más se combinan según las necesidades del mail.

### Los 5 módulos

| Archivo | Descripción |
|---------|-------------|
| `modulo-titulo.html` | Único módulo SIN contenedor de fondo. Solo un título destacado. |
| `modulo-3-columnas.html` | Tres columnas con imagen + texto cada una |
| `modulo-2-columnas.html` | Dos columnas: una con textos, otra con imagen. Incluye versión escritorio y mobile. |
| `modulo-logos.html` | Grid de logos en bloques de 3, 4 o 6 |
| `modulo-contenido.html` | El más versátil: imagen + componentes (bullet logo, bullet icono, bullet numerado) |

### Reglas comunes a los 5 módulos

- Cada módulo es `role="module"` (excepto el de título que no tiene contenedor).
- Entre dos módulos consecutivos siempre va un `<div class="separador">`.
- No modificas la estructura interna, solo las URLs de imágenes y los textos.

### Foco · módulo contenido

Este es el más complejo y el que más se usa. Su estructura interna:

```
modulo-contenido
├── imagen full (opcional)
├── divcomponentes
│   ├── componente 1
│   ├── componente 2
│   └── componente 3
├── imagen full (opcional, si va abajo)
└── divcomponentes (si hay componentes debajo de la imagen)
```

Dentro del `divcomponentes` van los **3 tipos de bullet**:

#### Bullet Logo (`role="componente"`)
Logo de 50px + subtítulo + texto al lado. Para destacar partners o productos con marca.

#### Bullet Icono (`role="componente"`)
Ícono pequeño de 25px + subtítulo + texto. Para listar features o beneficios sin marca.

#### Bullet Numerado (`role="componente"`)
Número grande con borde derecho + subtítulo + texto. Para pasos secuenciales (1, 2, 3...).

**Cualquier combinación de estos 3 tipos puede ir dentro de un mismo módulo contenido**, separados por `<div class="separador-M">`.

### Foco · módulo 2 columnas

Tiene una particularidad: **hay versión escritorio y versión mobile separadas**. Las clases `mobile_hide` y `desktop_hide` controlan cuál se muestra en cada dispositivo. Cuando lo uses, **inserta ambas versiones**, no solo una.

### Foco · módulo logos

El alto del contenedor cambia según la cantidad de logos:
- **2 o 3 logos** → `height: auto`
- **4 logos** → `height: 295px;`
- **5 o 6 logos** → `height: 200px;`

Esto está documentado dentro del archivo como comentario.

---

## 9. Closing · la imagen de cierre

📁 `02-components/closing/`

### El único archivo: `cierre.html`

Es una tabla simple con una imagen de cierre (típicamente la firma "Rappi" en versión imagen).

### Regla #1 · NO va en Pro ni ProBlack
**Esta es la regla más importante del sistema.** Si el KV es Pro o ProBlack, ELIMINAS la tabla completa. No la dejes con `display: none`, no la dejes vacía: la borras del HTML.

### Regla #2 · NO va si la fuente dice "sin cierre"
Si la columna "Pide img" de la fuente trae el valor "sin cierre", también eliminas la tabla.

### Regla #3 · La URL de la imagen depende del KV
Para Genérico, Turbo y Neutro, la URL de la imagen viene de la base de datos de assets:

| KV | Tipo de imagen de cierre |
|----|-------------------------|
| Genérico | Firma RappiFirma |
| Turbo | Firma RappiTurboFirma |
| Neutro | Firma neutra |

La URL exacta se busca en la TAXONOMÍA ASSETS (Google Sheets).

### Regla #4 · El cierre va al final del body
El cierre va después del último módulo/CTA y antes del footer. **No** va dentro de los módulos.

### Regla #5 · No insertes módulos debajo del cierre
Después de la tabla de cierre **no debe haber más CTAs ni módulos de contenido**. Si la fuente trae algo después del cierre, es probable que esté mal estructurada y deba reorganizarse.

---

## 10. Footer · el pie del mail

📁 `02-components/footer/`

### El único archivo: `footer.html`

Es un bloque Liquid con 5 variables:

```liquid
{% assign cond = '' %}
{% assign font_style_look = 'negro' %}
{% assign show_legal_tyc = true %}
{% assign show_legal_turbo = true %}
{% assign show_legal_liquor = true %}
{{content_blocks.${FOOTER_q1_2024_legales}}}
```

### Regla #1 · El footer SIEMPRE va completo
**Nunca se omite.** Aunque la fuente no traiga información, el footer queda como está en la base.

### Regla #2 · Las 5 variables siempre se evalúan

| Variable | Qué hace | Cómo se llena |
|----------|----------|---------------|
| `cond` | Texto de legales adicionales | Si la fuente trae "Legales adicionales", se inserta. Si no, queda vacío `''`. |
| `font_style_look` | Estilo visual del footer | `'negro'` para Genérico/Turbo/Neutro, `'pro'` para Pro/ProBlack |
| `show_legal_tyc` | Mostrar términos y condiciones | `true` si fuente trae "Legal promos = TRUE", si no `false` |
| `show_legal_turbo` | Mostrar legal Turbo | `true` si fuente trae "Legal turbo = TRUE", si no `false` |
| `show_legal_liquor` | Mostrar legal licores | `true` si fuente trae "Legal licores = TRUE", si no `false` |

### Regla #3 · Hay dos versiones de footer
La línea `{{content_blocks.${FOOTER_q1_2024_legales}}}` cambia según el tipo de footer:

| Si "Tipo de Footer" es... | Esa línea queda como... |
|---------------------------|------------------------|
| General | `{{content_blocks.${FOOTER_q1_2024_legales}}}` (como en la base) |
| Sin amor | `{{content_blocks.${FOOTER_VERSION2}}}` |

El resto del footer se conserva idéntico.

### Regla #4 · Links dentro de "Legales adicionales"
Si el texto de `cond` trae un link, se envuelve en una etiqueta `<a>` con estilo específico:

```html
<a href="linkaqui" style="text-decoration: none; color:#7D8188">linkaqui</a>
```

---

## 11. Orden recomendado de uso

Cuando armas un mail desde cero, el flujo siempre es el mismo. **Sigue este orden y no te equivocas:**

```
PASO 1 → un header de headers/                      (siempre, 1 solo)
PASO 2 → un banner de banners/                      (siempre, 1 solo)
PASO 3 → [zona libre del cuerpo]:
           - CTAs                                   (0 a N)
           - deals (max 4)                          (0 a 4)
           - coupons (en pares)                     (0, 2, 4...)
           - benefits                               (0 a N)
           - content-modules                        (0 a N)
PASO 4 → cierre.html                                (solo si el tema NO es Pro/ProBlack)
PASO 5 → footer.html                                (siempre)
```

### Reglas de espaciado dentro del paso 3

Mientras armas la zona libre del cuerpo, recuerda los separadores:

| Entre... | Va... |
|----------|-------|
| Dos módulos (`role="module"`) consecutivos | `<div class="separador"></div>` |
| Un módulo y un CTA | `<div class="separador"></div>` |
| Después de un CTA | `<div class="separador"></div>` (excepto si va el cierre debajo) |
| Antes o después de un deal | NADA (los deals tienen su propio aire) |
| Entre cupones del mismo módulo | va dentro de la misma tabla, no separador |
| Entre dos beneficios consecutivos | `<div class="separador"></div>` |

---

## Hoja de ruta para nuevos miembros del equipo

Si acabas de entrar al equipo y vas a producir tu primer mail, sigue estos pasos en este orden:

1. **Lee el README principal** del repo (el archivo `README.md` en la raíz)
2. **Lee `GUIA-DE-TEMAS.md`** completa. Es la que más importa.
3. **Lee esta guía** completa.
4. **Lee `COMO-ARMAR-UN-MAIL.md`** para tener el paso a paso en mente.
5. **Mira ejemplos reales** en `06-examples/` cuando existan.
6. **Tu primer mail**: pídele al equipo un mail real que ya esté producido y armálo desde cero usando el sistema. Compara el resultado con el original — si coincide, ya entendiste J.A.R.V.I.S.

---

## Referencias cruzadas

- Reglas detalladas de temas: `05-docs/GUIA-DE-TEMAS.md`
- Flujo paso a paso: `05-docs/COMO-ARMAR-UN-MAIL.md`
- Índice de componentes con líneas exactas: `05-docs/INDICE-DE-COMPONENTES.md`
- Cómo contribuir al sistema: `05-docs/CONTRIBUTING.md`
