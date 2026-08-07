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
- Si necesitas un color, tamaño, radio o padding nuevo, primero revisa si ya existe un token que encaje (ver Figma Tokens y `GUIA-DE-TEMAS.md`) antes de crear uno.

### Aplicar el tema
Las variables del tema (`bg_solid_mail_general`, `background-image` de `.gradmobile`, background del header, etc.) se aplican en las zonas correspondientes del mail según `GUIA-DE-TEMAS.md`. Consulta esa guía para los valores exactos y qué falta por migrar (sección "Estado actual / pendientes").

---

## 2. Headers · la identidad del remitente

📁 `02-components/01_headers/`

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

Los 4 grupos de tamaño de header (`#HEADER1`-`#HEADER4`, ver `01-foundations/global-styles/global-styles.html`) tienen su propio valor de `cobranding-l`. Actualizado (+5%) el 2026-08-04:

| Grupo | Marcas | `cobranding-l` escritorio | `cobranding-l` mobile |
|---|---|---|---|
| HEADER1 | Rappi, SoyRappi, RappiTravel | ~~39px~~ → **41px** | ~~36px~~ → **38px** |
| HEADER2 | RappiPro, RappiTurbo, RappiProBlack, Defensoría | ~~33px~~ → **35px** | ~~31px~~ → **33px** |
| HEADER3 | RappiTurbo Restaurantes | ~~45px~~ → **47px** | ~~42px~~ → **44px** |
| HEADER4 | RappiEntregador, Contenido aliado | ~~28px~~ → **29px** | ~~26px~~ → **27px** |

Estos son los valores de referencia a llevar al sistema de diseño en Figma (tokens de `cobranding-l` por grupo de header).

### El wrapper compartido
El archivo `_header-wrapper.html` (con guion bajo) es la **envolvente común a todos los headers**. Cuando armas un mail, el flujo es: insertas el wrapper, y dentro del wrapper insertas el `<tr>` de uno de los 40 archivos específicos (10 marcas × claro/oscuro × centrado/columnas).

---

## 3. Banners · la cabecera visual

📁 `02-components/02_banners/`

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

### Regla #3 · Las piezas internas del banner viven en `banner_moleculas/`
📁 `02-components/02_banners/banner_moleculas/` — piezas que se combinan dentro de cada banner. La mayoría vienen en pareja horizontal/vertical porque los tamaños de escritorio se aplican inline según en qué banner se insertan:

Piezas fijas (MODULOS, se conservan en `big-banner-*.html` tal cual, no son MOLECULAS):
1. **`modulo_tags_horizontal.html`** / **`modulo_tags_vertical.html`** — Tag/etiqueta superior. Si la fuente no trae tag, se omite.
2. **`modulo_img_altofijo_horizontal.html`** / **`modulo_img_altofijo_vertical.html`** — Columna de imagen de alto fijo.
3. **`modulo_img_automatica_horizontal.html`** — Celda alternativa a `modulo_img_altofijo_horizontal.html` en el horizontal (solo se usa una de las dos). No confundir con `molecula_img_automatica_*`.

Piezas de `MODULO MOLECULAS` (MOLECULAS, se combinan libremente dentro de esa tabla) — ya con nombre `molecula_*` para ambos banners:
4. **`molecula_creditos_horizontal.html`** / **`molecula_creditos_vertical.html`** — Texto vivo de créditos ("$XXX" + "DE REINTEGRO"), usa las clases `bnr-*`.
5. **`molecula_promo_horizontal.html`** / **`molecula_promo_vertical.html`** — Módulo de promo ("Ahora" + cifra).
6. **`molecula_textoxl_horizontal.html`** / **`molecula_textoxl_vertical.html`** — Texto vivo XL adicional, mismo comportamiento de tamaño que la molécula de promo.
7. **`molecula_textom_horizontal.html`** / **`molecula_textom_vertical.html`** — Texto vivo `.bnr-md`, tamaño fijo inline.
8. **`molecula_img_automatica_horizontal.html`** / **`molecula_img_automatica_vertical.html`** — Imagen automática dentro del banner.
9. **`molecula_cta_interno_horizontal.html`** (`cta_alineado: 'left'`) / **`molecula_cta_interno_vertical.html`** (`cta_alineado: 'center'`) — CTA embebido dentro del banner.
10. **`molecula_texto_complementario_horizontal.html`** / **`molecula_texto_complementario_vertical.html`** — Texto de body (`<h4>`) que acompaña al texto destacado del banner, distinto por orientación. Reemplazan al viejo `modulo_texto_complementario.html` (sin sufijo, ya eliminado); contenido pendiente de insertar manualmente en cada uno. (`modulo_img_variable.html` y `modulo_texto_secundario.html` ya se eliminaron.)

### Regla #4 · El banner cambia mucho según el tema
El banner es donde más reglas de tema se aplican: background-color, background-image, color de textos, bgcolor del tag, border-radius. Antes de armar el banner, consulta `GUIA-DE-TEMAS.md` para los valores exactos (los comentarios internos del banner todavía usan la nomenclatura anterior; los valores de referencia son los de esa guía).

---

## 4. CTAs · el botón de acción

📁 `02-components/03_ctas/`

### Dos archivos: `cta-llamado.html` + `cta-template.html`

> **Cambio v1.2:** el botón ya no se llama directo. `cta-llamado.html` define 4 variables y luego invoca `{{content_blocks.${CTA-template}}}` (el botón en sí, vive como content block de Braze):

```liquid
{% assign cta_alineado = 'center' %}
{% assign text_cta = 'Súper completo en 10 min' %}
{% assign deeplink_cta = '#' %}
{% assign style_Look = 'neon' %}
{{content_blocks.${CTA-template}}}
```

### ¿Qué cambia entre un CTA y otro?

El contenido de las 4 variables:
- **`cta_alineado`** — `'left'` o `'center'`
- **`text_cta`** — el texto del botón (máx. 35 caracteres, se trunca automático)
- **`deeplink_cta`** — la URL a la que lleva el botón
- **`style_Look`** — el estilo visual del botón. Hay **8 variantes reales**: `'neon'` (default), `'blanconeon'`, `'negroneon'`, `'verde'`, `'blancogris'`, `'negrogris'`, `'problack'`, `'pro'`.

> ⚠️ **`style_Look='blanco'` es un alias legacy** idéntico a `'blanconeon'` — sigue existiendo en el archivo pero **no se usa en código nuevo**. Ver `05-docs/ATOMIC-DESIGN.md`, Átomos 4.6, para el detalle de cada variante (fondo, ícono de flecha, comportamiento mobile).

### Regla #1 · Puede haber varios CTAs en un mail
Un mail puede tener 1, 2 o 3 CTAs intercalados a lo largo del body. La fuente te dice cuántos y dónde.

### Regla #2 · Separadores alrededor del CTA
- **Después de un CTA** siempre va un `<div class="separador"></div>` ANTES del siguiente componente.
- **Excepción:** si justo debajo del CTA va el cierre, NO se inserta el separador.

### Regla #3 · El CTA siempre va con el `<div class="separador">` antes
Si el componente anterior es un módulo (`role="module"`), insertas el separador entre módulo y CTA.

---

## 5. Deals · promociones de productos

📁 `02-components/04_content-modules/deals/`

### El archivo activo: `deal_columnas.html`

Los deals vienen de a **PARES** en una grilla de 2 celdas (50/50). Cada celda tiene un bloque de imagen (overlay + producto + logo opcional) y un bloque de texto (título, descuento, rating, tags, CTA). Pensado para promociones frecuentes en la app: da espacio para destacar tanto la promo como el restaurante/comercio.

### Regla #1 · Los deals siempre van en pares
Por cada 2 deals, una tabla completa nueva (misma lógica que Coupons).

### Regla #2 · Cantidad impar = celda derecha vacía
Cuando el número de deals es impar, se elimina **todo el contenido** de la celda derecha (imagen, texto, legal) — la celda permanece vacía, pero la grilla nunca se rompe en una sola columna. No se reemplaza por ningún tipo de celda especial.

### Regla #3 · Piezas internas de cada celda
- **Imagen** — overlay + imagen de producto (reemplazable) + logo opcional (se elimina la etiqueta si no hay logo).
- **Línea 1 / Línea 2** — título y descripción, se eliminan si no hay texto.
- **MARKDOWN** — descuento destacado con ícono Corona Pro togglable.
- **COMPLEMENTO 1 / COMPLEMENTO 2** — texto adicional (ej. "99% OFF" / "| Antes $999"), cada uno independiente.
- **TEXTOS RATING** — CATEGORIA + RATING + TIEMPO, cada uno independiente y removible.
- **TAG1 / TAG2** — hasta 2 tags con ícono removible.
- **CTA** — texto editable (ej. "Pide ahora ⤍").
- **Legales** — fila aparte, desactivada por defecto.

Es el **único módulo de contenido con link activo de fábrica** (`href="LINKDEAL"`).

> `deal-large.html` y `deal-small.html` ya no se usan. Se conservan renombrados como `deal-large.backup.html` / `deal-small.backup.html` para no perder el trabajo — **no usar como referencia para mails nuevos**: no tienen el sistema de escalado dinámico por variante que documentaban versiones previas de este archivo, ya no existe en el sistema actual.

---

## 6. Coupons · cupones de descuento

📁 `02-components/04_content-modules/coupons/`

### El único archivo: `cupones-modulo.html`

Es una tabla que contiene **2 celdas por fila**. Cada celda es un cupón, y por defecto ambas lo son.

### Regla #1 · Los cupones siempre van en pares
Por cada 2 cupones, se repite la tabla completa (mismo patrón que Deals).

### Regla #2 · La celda 1 puede convertirse en TÍTULO
En vez de dos cupones, la **celda 1** puede reemplazarse por la celda suelta `celda_cupon_titulo.html` (`role="titulocupon"`), dejando la **celda 2** siempre como un cupón normal. Es una decisión de contenido, no una regla automática de balanceo par/impar. Esta celda de título tiene su **propia estructura** — no es el mismo patrón que `modulo-titulo.html`:
- Línea punteada arriba Y abajo (`{{body_container_img_dots}}`) — ninguna de las dos se puede quitar.
- Tag con ícono (`role="molecula-tag"`, ícono cambiable o removible; si se quita el ícono, se elimina toda la molécula).
- H1 `role="molecula-texto"` — el título grande ("Aca un título").
- Módulo clickeable opcional vía `<a href="LINKTITULO">`.

### Regla #3 · Las piezas internas de cada celda de cupón
- **Imagen de producto** (`role="imagenfull"`) — reemplazable.
- **Línea punteada** (`{{body_container_img_dots}}`) — decorativa, **NO se puede quitar**.
- **Pastilla + texto** (ej. "Solo en" / "Restaurantes") — se puede usar solo una, o ambas, en cualquier orden.
- **MARKDOWN** (h1, color `{{color_acento2_mail_general}}`) — el texto grande del cupón, admite modificadores de texto.
- **Separador** — línea antes del bullet.
- **Bullet** — ícono (removible eliminando el `<td>` completo) + texto editable.

### Regla #4 · El fondo de la celda SIEMPRE está activo
A diferencia de otros módulos de contenido, en Cupones el fondo (`{{bg_contenedor1_mail_general}}`) **no se puede desactivar**, y el alineado es fijo — solo se pueden modificar los pesos de texto.

### Regla #5 · Los legales viven en una fila aparte
Los legales NO van dentro del cupón. Van en una fila separada debajo de la fila principal, desactivada por defecto — si se activa, se activan las dos celdas juntas.

---

## 7. Benefits · beneficios del programa

📁 `02-components/04_content-modules/benefits/`

### El único archivo: `modulo-beneficios.html`

Es una **card horizontal** dividida en 2 columnas:
- Celda 1: imagen (`imagen-auto`, reemplazable)
- Celda 2 (`role="celda2"`): ícono + subtítulo + texto, separados por `separador-S`

### Regla #1 · Por cada beneficio, una tabla nueva
Si la fuente trae 3 beneficios, se insertan **3 tablas de beneficios seguidas**, no se combinan en una sola.

### Regla #2 · Entre beneficios va un separador
Como cualquier módulo (`role="module"`), entre dos beneficios consecutivos va un `<div class="separador">`.

### Regla #3 · La proporción de las celdas CAMBIA entre desktop y mobile
En desktop la celda de imagen es más angosta que la de texto (**40% / 60%**, clase `.beneficios-mob`); en mobile ambas celdas pasan a **50% / 50%**. No es un ajuste manual — el CSS mobile lo hace solo.

### Regla #4 · Celda 2 está abierta
A diferencia de otros módulos con estructura fija, la celda 2 admite **varias moléculas** (no solo un ícono+subtítulo+texto) — al eliminar una, elimina también su separador correspondiente.

### Regla #5 · El fondo del contenedor es opcional
Se puede usar el módulo **con o sin fondo** (`{{bg_contenedor1_mail_general}}`).

### Regla #6 · No cambies el `vertical-align`
Dentro del archivo hay comentarios que dicen `<!-- no cambies este vertical align -->`. Respétalos. El alineado vertical es parte del diseño y no debe modificarse.

---

## 8. Content Modules · los bricks combinables del cuerpo

📁 `02-components/04_content-modules/`

Esta es la carpeta más versátil. Aquí viven los bricks que más se combinan según las necesidades del mail.

### Los módulos de esta carpeta

| Archivo | Descripción |
|---------|-------------|
| `title/modulo-titulo.html` | Título (H2) + separador opcional + bloque de texto (H3). Sin contenedor de fondo por defecto (encendido por defecto solo en Pro/ProBlack). |
| `bullet/modulo_bullet.html` | Ícono (intercambiable S/M/L/XL) + subtítulo + texto, en su propio contenedor. Se puede usar con o sin fondo. |
| `3columnas/modulo-3-columnas.html` | Tres columnas idénticas, cada una con ícono+texto+imagen full — misma estructura en desktop y mobile |
| `2columnas/modulo-2-columnas.html` | Celda imagen + celda de moléculas, orden intercambiable. Incluye versión escritorio (`mobile_hide`) y mobile (`desktop_hide`) — se duplica la tabla completa |
| `logos/modulo-logos.html` | Mismo patrón que 2 Columnas (tabla duplicada), celda de moléculas + grid de logos de 3, 4 o 6 |
| `1columna/modulo-1columna.html` | El más versátil: uno o varios bloques de moléculas + una imagen full-width opcional, en el orden que se necesite |

Ver `05-docs/ATOMIC-DESIGN.md` (Organismos 6.3–6.11) para la anatomía completa, el HTML real y los "elementos editables" de cada uno.

### Reglas comunes

- Cada módulo es `role="module"` (excepto el de Título, que no lleva contenedor de fondo por defecto).
- Entre dos módulos consecutivos siempre va un `<div class="separador">`.
- No modificas la estructura interna, solo las URLs de imágenes y los textos.

### Foco · módulo 1 columna

Ya **no** embebe tipos de bullet fijos. Es un contenedor genérico: uno o varios bloques `divcomponentes` (moléculas separadas por `separador-M`) y, aparte, una imagen full-width (`imagen-auto`) opcional. Ambos bloques se mueven, duplican u omiten libremente:

```
modulo-1columna
├── divcomponentes (moléculas de content_moleculas/, cualquier combinación)
├── imagen-auto (opcional, se elimina la etiqueta completa si no se usa)
└── divcomponentes (opcional, si hace falta otro bloque de moléculas debajo de la imagen)
```

Combinaciones válidas: Moléculas+Imagen, Imagen+Moléculas, Moléculas+Imagen+Moléculas (o más repeticiones). Si necesitas un ícono+subtítulo+texto en su propio contenedor con fondo propio, ese es **Módulo Bullet** (`bullet/modulo_bullet.html`), no una molécula embebida en 1 Columna.

### Foco · módulo 2 columnas y módulo logos

Ambos comparten el mismo patrón: **se duplica la tabla completa**, una versión con `class="mobile_hide"` (2 columnas lado a lado en desktop) y otra con `class="desktop_hide"` (celdas apiladas en mobile). Cualquier cambio se aplica a **ambas** versiones — si son N módulos en la fuente, se insertan 2N tablas en el HTML.

En Módulo Logos, la celda de logos es más ancha que la de moléculas (60%/40%). Las grillas válidas son 3, 4 o 6 logos (solo una por instancia, según `grilla3/4/6logos.html`); con 5 logos se usa la grilla de 6 y la 6ª celda queda con el fondo placeholder (no se quita ni se modifica).

---

## 9. Closing · la imagen de cierre

📁 `02-components/05_closing/`

### El único archivo: `cierre.html`

Es una tabla simple con una imagen de cierre (típicamente la firma "Rappi" en versión imagen).

### Regla #1 · NO va si el tema es Pro o ProBlack
**Esta es la regla más importante del sistema.** Si `tema_general_mail_general` es Pro o ProBlack, ELIMINAS la tabla completa. No la dejes con `display: none`, no la dejes vacía: la borras del HTML.

> ⚠️ **Auditoría:** esta regla está documentada así en Figma (Moléculas 5.4) pero hoy **no está implementada** en `template_maestro_original.html` — la tabla de cierre se renderiza para los 12 temas sin excepción. Pendiente de confirmar con el equipo si se implementa o se actualiza la regla.

### Regla #2 · NO va si la fuente dice "sin cierre"
Si la columna "Pide img" de la fuente trae exactamente el valor `"sin cierre"`, se elimina la etiqueta `<img>` por completo (la tabla contenedora queda vacía).

### Regla #3 · La URL de la imagen depende del texto "Pide img", no del tema
La base de datos tiene **10 variantes** de firma, cada una asociada a un texto exacto de "Pide img" (ej. "Pide un Rappi", "Pedí un Rappi", "Pídelo por Rappi mx", "Pede um Rappi", y sus 4 equivalentes de RappiTurbo + 2 co-branded con Carulla/MiComisariato). Si "Pide img" coincide con uno de esos 10 textos, se usa la URL correspondiente; si no coincide con nada, se conserva la imagen que ya trae la plantilla base. El detalle completo (los 10 textos y sus URLs) está en `05-docs/ATOMIC-DESIGN.md`, Moléculas 5.4.

### Regla #4 · El cierre va al final del body
El cierre va después del último módulo/CTA y antes del footer. **No** va dentro de los módulos.

### Regla #5 · No insertes módulos debajo del cierre
Después de la tabla de cierre **no debe haber más CTAs ni módulos de contenido**. Si la fuente trae algo después del cierre, es probable que esté mal estructurada y deba reorganizarse.

---

## 10. Footer · el pie del mail

📁 `02-components/06_footer/`

### El orquestador: `footer.html`

Es un bloque Liquid con 5 variables que decide qué content block de legales insertar:

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
| `font_style_look` | Estilo visual del footer | Ya **no se elige a mano** — toma el valor de `{{color_footer_mail_general}}`, definido por el tema activo (ver `GUIA-DE-TEMAS.md`): `'negro'` en la mayoría de los 12 temas, `'pro'` en Pro/ProBlack |
| `show_legal_tyc` | Mostrar términos y condiciones | `true` si fuente trae "Legal promos = TRUE", si no `false` |
| `show_legal_turbo` | Mostrar legal Turbo | `true` si fuente trae "Legal turbo = TRUE", si no `false` |
| `show_legal_liquor` | Mostrar legal licores | `true` si fuente trae "Legal licores = TRUE", si no `false` |

### Regla #3 · Hay TRES variantes de legales, no dos

La línea `{{content_blocks.${...}}}` cambia según cuál de los 3 archivos de footer aplica al mail:

| Variante | Content block | Cuándo se usa |
|---|---|---|
| General (`footer_general.html`) | `{{content_blocks.${FOOTER_q1_2024_legales}}}` | La más usada — toda comunicación dirigida a usuarios |
| Sin amor (`footer_sinamor.html`) | `{{content_blocks.${FOOTER_VERSION2}}}` | Comunicaciones más formales — sin WhatsApp, sin "Hecho con Amor" |
| RTS (`footer_rts.html`) | `{{content_blocks.${FOOTER_RTS_q3_2024_legales}}}` | Predeterminado para comunicaciones a repartidores/colaboradores de delivery — legales y canales propios ("Soy Rappi") |

Lo único que cambia por fuente es cuál de las 3 variantes se referencia y los toggles `show_legal_*`. Detalle completo de cada una (estilos, variables por país, hallazgos de auditoría) en `05-docs/ATOMIC-DESIGN.md`, Organismos 6.12.

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
           - deals (en pares; impar = celda vacía)   (0, 2, 4...)
           - coupons (en pares)                      (0, 2, 4...)
           - benefits                                (0 a N)
           - content-modules                         (0 a N)
PASO 4 → cierre.html                                (debería omitirse si el tema es Pro/ProBlack — ver nota de auditoría en la sección 9)
PASO 5 → footer.html                                (siempre — General, Sin Amor o RTS según el mail)
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
