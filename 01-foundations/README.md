# 01 · Foundations

> Las reglas del LEGO.

Aquí viven las reglas que cualquier brick respeta: qué es el sistema, qué nunca se puede romper, los tokens (paleta, tipografía, separadores, radios, padding) y los 12 temas que los consumen. **Nadie debería tocar esta carpeta sin coordinarlo con el equipo de diseño**, porque cualquier cambio aquí afecta a TODOS los mails.

Este README refleja 1:1 las 3 hojas de Figma **Doc-DS-Mails**: **Foundations**, **Tokens** y **Temas**. Si hay diferencia entre el HTML y cualquiera de los dos (Figma o este archivo), **gana el HTML** — toda esta documentación existe para reflejarlo, no al revés.

---

## 1 · Foundations — los principios

*(Figma → hoja "Foundations")*

### 1.1 · ¿Qué es J.A.R.V.I.S.?

J.A.R.V.I.S. es el sistema operativo de los mails de Rappi. Convierte el proceso fragmentado de hacer emails (Figma suelto → interpretación manual → HTML a mano) en un sistema modular, escalable y colaborativo.

**La metáfora LEGO:** los **tokens** son las reglas de color y forma. Los **átomos** son los bricks básicos (un `h1`, un swatch, un separador). Las **moléculas** combinan bricks (un bullet con logo). Los **organismos** son ensambles más grandes (un Big Banner completo). Las **plantillas** son los modelos terminados. Cualquier persona puede combinar las piezas para construir mails sin empezar de cero.

### 1.2 · El HTML maestro es la fuente única de verdad

**Regla de oro:** cuando hay diferencia entre Figma y el HTML, gana el HTML. El sistema de Figma existe para reflejar y documentar el HTML — no al revés. Esto evita drift y mantiene a Braze como destino confiable.

```
Figma DS  ─────────►  HTML maestro  ─────────►  Braze
(documentación         (fuente única            (destino: inbox
y prototipado)          de verdad)                del usuario)
```

⚠ Si modificás un token o componente en Figma sin actualizar el HTML, estás introduciendo drift. Documentá el cambio en el HTML primero, luego reflejalo en Figma.

### 1.3 · Atomic Design aplicado a mails

El sistema sigue las 5 capas de Atomic Design de Brad Frost, adaptadas a la realidad de email marketing:

| Capa | Descripción | Ejemplos |
|---|---|---|
| **Tokens** | Las variables CSS: colores, tipografía, espaciado. No son visibles solos. | `mail/bg-body`, `h4`, separador |
| **Atoms** | El componente más pequeño visible. Un texto h4, un tag, un swatch, un CTA aislado. | Tag, h4 título, separador 16px |
| **Molecules** | Combinación de átomos que cumple una micro-función. No tiene contexto de página todavía. | Bullet con logo + texto, cupón |
| **Organisms** | Bloques completos que viven en el HTML como `<table role="module">`. Aquí ya hay contexto. | Big Banner, Big Deal, Módulo Beneficios |
| **Templates** | El mail completo ensamblado, una variación por tema (de los 12 en `tema_general_mail_general`). Es la salida final. | Template Pro, Template Dark Turbo, Template Beige 100 |

Ver la versión ampliada de esta clasificación, pieza por pieza, en `05-docs/ATOMIC-DESIGN.md`.

### 1.4 · Lo que NUNCA se puede modificar

Reglas extraídas directamente del HTML maestro. Romperlas rompe Braze, rompe el render en clientes de mail viejos, o desalinea el sistema.

| Regla | Detalle |
|---|---|
| **Cambios de estilo: global-styles y head-meta-tags** | Si se agrega o modifica un estilo, va en `global-styles.html` o `head-meta-tags.html` — nunca suelto en un componente. Los estilos de escritorio se mantienen en su mayoría inline en los propios componentes; no se migran a la hoja global. El `<script type="application/ld+json">` ya no va después de `</html>` — hoy vive dentro del `<head>`, al inicio de `global-styles.html`. |
| **Estructura de tablas y divs** | El esqueleto del mail (filas, columnas, módulos) se mantiene siempre en tablas (`<table>/<tr>/<td>`) — es lo que garantiza el render en Outlook y clientes de mail viejos. Los `<div>` se usan solo en casos puntuales: separadores, tags, contenedores redondeados, decoraciones. Nunca reemplazan la estructura de tablas. |
| **Cero inserción autónoma** | Ya no es una prohibición total: si necesitás un módulo nuevo, partí siempre de la estructura de los módulos existentes — ya están probados y funcionan en la mayoría de dispositivos y clientes de mail. No se inventa desde cero; se adapta lo que ya existe. |
| **No optimizar el código** | Mantener espacios en blanco, tabulaciones, comentarios y condicionales de Outlook exactamente como están. No "embellecer" el código. |
| **Padding ya definido — no se inventa** | La tabla general (`role="paddedcontainer"`, padding `20px 15px 0px 15px`) ya alinea todos los módulos entre sí. Cada módulo además tiene su propio padding según tenga o no fondo (`body_container_background_padding`, ver 2.6). No se agregan márgenes/padding ad-hoc por fuera de estos dos sistemas. |
| **Separadores obligatorios** | Entre dos `role="module"` consecutivos, `<div class="separador"></div>` (16px) — obligatorio. Dentro de un módulo, `<div class="separador-M"></div>` (10px) separa moléculas/componentes y `<div class="separador-S"></div>` (4px) da aire mínimo entre átomos. |
| **Imágenes desde la TAXONOMÍA** | Las URL de imágenes siempre vienen del Google Sheet TAXONOMÍA ASSETS. No inventar URLs. |
| **Cierre en Pro/ProBlack** | Si `tema_general_mail_general = 'pro'` o `'problack'`, el cierre (firma RappiFirma) no debería mostrarse — no ocultar con `display:none`, borrar la tabla del HTML. ⚠ Auditoría de código: `template_maestro_original.html` hoy NO implementa esta exclusión — el CIERRE se renderiza igual para los 12 temas, sin condicional. Pendiente de confirmar si la regla sigue vigente o si hay que actualizar el HTML maestro. |

### 1.5 · Quién mantiene este sistema

Cualquier cambio al sistema sigue un orden: primero el HTML maestro, luego Figma, luego este archivo.

| Rol | Responsabilidad |
|---|---|
| **Equipo de mails** (designers) | Construyen los mails diarios usando los componentes del sistema. Reportan inconsistencias o necesidades nuevas. |
| **Lead del sistema** (Team EVA Neón) | Mantiene el HTML maestro y el archivo Figma. Aprueba nuevos componentes y refactors. |
| **Reactor J.A.R.V.I.S.** (producción) | Genera HTML diario a partir de la fuente. Aplica las reglas del sistema en cada mail entregado. |
| **Claude** (construcción) | Asiste en construir y refactorizar el sistema. Documentación, refactors, nuevos componentes. |
| **Braze** | Plataforma final. Renderiza el HTML producido por la jarvis. No conoce el sistema — solo recibe HTML. |

---

## 2 · Tokens

*(Figma → hoja "Tokens")*

### 2.1 · Paleta primitiva

Los colores universales del sistema — los que **NO** cambian entre temas. Los tonos específicos de cada tema (Beige, Rosa, Púrpura, Celeste, Verde, Pro, ProBlack, etc.) no están acá — viven en su card de la sección 3 · Temas.

**Marca Rappi** — colores oficiales de identidad:

| Token | Hex | Uso |
|---|---|---|
| `brand/rappi-red` | `#FF441F` | Rojo Rappi. `color_acento2` en TODOS los temas. |
| `brand/neon-orange` | `#FF7A4D` | Stop 1 del gradiente Dark neon. |
| `brand/neon-red` | `#FF2526` | Stop 2 del gradiente Dark neon. |
| `brand/neon-pink` | `#FF4583` | Stop 3 del gradiente Dark neon. |
| `brand/neon-tono` | `#FE3F23` | `bg_banner_tono` en Dark neon. |

**Descuento y créditos · Pastel/Dark** — constantes universales, no cambian por tema:

| Token | Hex | Uso |
|---|---|---|
| `system/descuento-bg` | `#FBDB20` | `bg_descuento` en Pastel/Dark. Amarillo Rappi promo. |
| `system/descuento-text` | `#000000` | `color_descuento` en Pastel/Dark. |
| `system/creditos-bg` | `#29D884` | `bg_creditos` en Pastel/Dark. Verde créditos. |
| `system/creditos-text` | `#083410` | `color_creditos` en Pastel/Dark. |
| `system/legales` | `#7D8188` | `color_textos_legales`. Gris legales, universal. |

**Descuento y créditos · Pro/ProBlack** — variante premium dorada:

| Token | Hex | Uso |
|---|---|---|
| `system/descuento-bg-pro` | `#F8D263` | `bg_descuento` en Pro/ProBlack. Dorado suave. |
| `system/descuento-text-pro` | `#000000` | `color_descuento` en Pro/ProBlack. |
| `system/creditos-bg-pro` | `#CC984E` | `bg_creditos` en Pro/ProBlack. Dorado tostado. |
| `system/creditos-text-pro` | `#FEE4C0` | `color_creditos` en Pro/ProBlack. Crema. |
| `system/gold-pro` | `#DAA868` | Dorado premium. Separador Pro, acento decorativo. |

**Neutros base** — fondos, textos y contenedores reutilizados por varios temas:

| Token | Hex | Uso |
|---|---|---|
| `neutral/950` | `#040404` | Negro profundo. `bg_solid` en Dark neon/Turbo/Neutro. |
| `neutral/900` | `#2A2B2B` | Gris muy oscuro. `bg_contenedor2` en Darks. |
| `neutral/925` | `#121212` | Gris casi negro. `bg_solid` en Pro (fijo). |
| `neutral/850` | `#1D1D1D` | Gris oscuro. `bg_contenedor1` en Darks. `bg_contenedor2` en Pro. |
| `neutral/200` | `#E2E2E2` | Gris muy claro. `color_texto` en Darks (sobre fondo negro). |
| `neutral/100` | `#ECEFF3` | Casi blanco frío. `bg_solid` en ProBlack. |

### 2.2 · Variables Liquid del tema (índice)

Las variables Liquid que arma cada tema (light mode) están definidas en `head-meta-tags.html`. Todas terminan en `_mail_general`. La variable maestra `tema_general_mail_general` dispara los valores del resto. **Esta sección es el índice de qué variables existen y para qué sirven — los valores concretos por tema viven en la sección 3 · Temas.**

| Categoría | Variable | Tipo | Para qué se usa |
|---|---|---|---|
| **Estructura visual** | `bg_solid_mail_general` | COLOR | Fondo del body del mail. Sólido. |
| | `bg_rgb_mail_general` | COLOR | Mismo tono que `bg_solid_mail_general`, en formato `rgba(x,x,x,0.7)`. Variable de definición — hoy no se consume en ningún HTML del sistema, preparada para usos futuros que necesiten transparencia sobre el fondo sólido. ◀ NUEVO |
| | `bg_img_mail_general` | IMAGE | Imagen de fondo del mail (solo Dark neon/Turbo/Neutro y Pro/ProBlack; los pastel no la usan). |
| | `bg_img_size_mail_general` | SPACING | Tamaño de `bg_img`. Dark: `"100% auto"`. Pro/ProBlack: `"100% 100%"`. |
| | `bg_header_mail_general` | IMAGE | Imagen del header superior (banda con logo Rappi). |
| **Texto** | `color_texto_mail_general` | COLOR | Color del texto del cuerpo. Contraste sobre `bg_solid`. |
| | `color_tag_tipografia_mail_general` | COLOR | Color del texto dentro de los tags/pills. |
| **Acentos** | `color_acento1_mail_general` | COLOR | Acento principal del tema — cambia por tema (dorado en Beige, púrpura en Púrpura, verde en Verde...). |
| | `color_acento2_mail_general` | COLOR | Acento universal Rappi: SIEMPRE `#FF441F` en TODOS los temas. |
| **Contenedores** | `bg_contenedor1_mail_general` | COLOR | Fondo del contenedor principal de módulos (rgba con opacidad en pastel; sólido en dark/premium). |
| | `bg_contenedor2_mail_general` | COLOR | Fondo del contenedor secundario (celdas internas, capas anidadas). |
| **Banner** | `bg_bannertono_mail_general` | COLOR | Tono de color sobre el banner (rgba). En pastel es transparente. |
| | `bg_bannerimg_mail_general` | IMAGE | Imagen de fondo del banner. Solo Dark neon la usa. |
| | `padd_banner_mail_general` | SPACING | Padding del banner. Pastel: `'0px 0px'`. Dark/Pro: `'15px 10px'`. |
| | `bg_banner_tono_mail_general` / `_opacity_` | COLOR/SPACING | Tono base + opacidad del gradiente del banner (solo dark/premium). ⚠ No usadas en ningún HTML real — ver nota abajo. |
| | `banner_gradiente_stop1/2/3_mail_general` / `_opacity_` | COLOR/SPACING | Los 3 stops + opacidad del gradiente hero. Solo Dark neon. ⚠ No usadas en ningún HTML real — ver nota abajo. |
| **Tags** | `bg_tag_fondo_mail_general` | COLOR | Fondo principal del tag (rgba con opacidad usualmente). |
| | `bg_tag_contenedor_mail_general` | COLOR | Fondo del contenedor exterior del tag (capa detrás). |
| **Imágenes overlay** | `img_overlay_1_mail_general` / `img_overlay_2_mail_general` | IMAGE | Overlays principal/secundaria del banner. |
| | `img_fondo_especial_mail_general` | IMAGE | Imagen de fondo especial (decoración adicional). |
| **Descuentos y créditos** | `bg_descuento_mail_general` / `color_descuento_mail_general` | COLOR | Fondo/texto del tag de descuento. |
| | `bg_creditos_mail_general` / `color_creditos_mail_general` | COLOR | Fondo/texto del tag de créditos. |
| **Legales y footer** | `color_textos_legales_mail_general` | COLOR | Color del texto legal. |
| | `color_footer_mail_general` | ENUM | `"negro"` (pastel/dark) o `"pro"` (pro/problack). |

⚠ **Variables huérfanas detectadas en auditoría:** `bg_banner_tono_mail_general`, `bg_banner_tono_opacity_mail_general` y `banner_gradiente_stop1/2/3_mail_general` están asignadas para los temas dark/premium con los mismos valores que su equivalente `bg_bannertono_mail_general`, pero **nunca se interpolan** en ningún componente ni en el template maestro — son código muerto (o una funcionalidad de gradiente real todavía no conectada). Se documentan igual porque el objetivo de este índice es saber cuántos tonos hay que crear para un tema nuevo, más allá de si hoy se aplican como CSS literal o como asset de imagen.

Variables adicionales no incluidas en el índice original de Figma pero sí en el HTML (ver 2.6 y `GUIA-DE-TEMAS.md`): `padd_deal_mail_general`, `coronapro_mail_body`, `bg_solid_generico100_mail_body` / `_50_`, `icon_link_generico_mail_body`, y toda la familia `body_container_background*` (toggle `'Fondo'`/`'Sinfondo'` + padding/radius/border/img_dots).

**Cómo se dispara un tema:**

```liquid
<!-- Al inicio del mail, se setea la variable maestra: -->
{% assign tema_general_mail_general = 'beige100' %}

<!-- head-meta-tags.html detecta el valor y setea el resto: -->
{% if tema_general_mail_general == 'beige100' %}
  {% assign bg_solid_mail_general = '#FFF0DD' %}
  {% assign color_texto_mail_general = '#633D11' %}
  {% assign color_acento1_mail_general = '#D89950' %}
  {% assign color_acento2_mail_general = '#FF441F' %}
  {% assign bg_contenedor1_mail_general = 'rgba(242,211,174,0.5)' %}
  ... (20+ variables más)
{% elsif tema_general_mail_general == 'darkneon' %}
  ...
{% endif %}

<!-- Cada componente usa las variables sin saber qué tema es: -->
<table style="background-color: {{ bg_solid_mail_general }};">
  <span style="color: {{ color_acento1_mail_general }};">40% OFF</span>
</table>
```

### 2.3 · Tamaños de texto por módulo

Family: Arial/Helvetica sans-serif. `body`, `p` y `div` heredan `14px`. Los tamaños de `h1`-`h6` y `.legal` en **mobile son 2px menores que en escritorio** (font-size y line-height, ambos), declarados con `!important` en los dos `@media` (`max-width: 480px` y `620px` — valores idénticos entre ambos):

| Elemento | Desktop (font / line-height) | Mobile (font / line-height) | Dónde se usa |
|---|---|---|---|
| `h1` | 26px / 29px | **24px / 27px** | Cupones (título grande) · precios destacados |
| `h2` | 21px / 23px | **19px / 21px** | Complemento · Contenido · Columnas (encabezados de sección) |
| `h3` | 16px / 18px | **14px / 16px** | Título · Logos · 2 Columnas (subtítulo) · Bullet numerado · Pastilla/Tag · Beneficios (headline) |
| `h4` | 14px / 16px | **12px / 14px** | Deals (copy y CTA) · Tag con ícono · Banner (tags) · Bullet · 3 Columnas · Cupones |
| `h5` | 12px / 14px | **10px / 12px** | Deals (% off, precio, categoría, rating) · Cupones (pills) |
| `h6` | 10px / 12px | **8px / 10px** | Reservado en la escala — sin uso actual en los módulos del código |
| `.legal` | 8px / 10px | **6px / 8px** | Legales (módulo LEGAL · Deals · Cupones) |

> ◀ Ajuste: se sumó +1px de line-height a las 7 filas de arriba (solo interlineado, el font-size no cambió), tanto en el bloque base como en los dos `@media` de `global-styles.html`.
>
> ◀ Ajuste (2026-08-20): mobile deja de ser igual a escritorio — pasa a ser **-2px en font-size y line-height** en las 7 filas, en los dos `@media` de `global-styles.html` (y su copia embebida en `template_maestro_original.html`). El desktop no cambió. Reflejado también en Figma (`Doc-DS-Mails` → hoja de Foundations, "2.3 · Tamaños de texto por módulo"), donde de paso se corrigieron los line-height de escritorio del bloque CSS de referencia (estaban desalineados en -1px respecto al HTML real).

Mobile ya no repite el mismo valor: `@media (max-width: 480px)` y `(max-width: 620px)` re-declaran `h1`-`h6`/`.legal` con `!important`, 2px menores que su equivalente de escritorio en font-size y line-height. Igual que `bnr-*` (abajo), esta escala **sí** varía por breakpoint.

Las clases `.txts` y `.txtl` ya no existen en el sistema — se quitaron de `global-styles.html`.

**Banner "texto vivo" (`bnr-*`)** — dimensionan el número/copy principal del banner (promocional, créditos, texto XL). El tamaño de **escritorio** va inline en las moléculas de `02-components/02_banners/banner_moleculas/`; `global-styles.html` solo define el override de **mobile**, donde ambas orientaciones convergen al mismo valor:

| Clase | Escritorio horizontal | Escritorio vertical | Mobile (ambas orientaciones) |
|---|---|---|---|
| `.bnr-xl` | 80px / 80px | 125px / 125px | 110px / 111px |
| `.bnr-lg` | 35px / 35px | 62px / 62px | 63px / 64px |
| `.bnr-md` | 30px / 31px | 50px / 51px | 45px / 46px |
| `.bnr-hasta-xl` | 19px / 19px | 25px / 25px | 27px / 28px |
| `.bnr-hasta-lg` | 10px / 10px | 15px / 15px | 16px / 17px |
| `.bnr-sm` | 14px / 15px | 16px / 18px | 17px / 20px |

`.bnr-xl`/`.bnr-lg` se eligen dinámicamente vía Liquid según el largo del texto (variables `*_class`, `*_fontsize`, `*_lineheight` en `head-meta-tags.html`). Ver el detalle en `02-components/README.md`.

> ◀ Ajuste: +1px de line-height en mobile para las 6 clases (font-size sin cambios). De paso se corrigió un bug de sync: `.bnr-md` mobile tenía `font-size: 55px` (copiaba el line-height por error) — el valor correcto es `45px`, igual que documentaba la columna de escritorio vertical.

### 2.4 · Separadores y spacing

Divs vacíos con altura fija. Se insertan entre y dentro de módulos para crear ritmo visual. Esto es distinto del padding del sistema: la tabla general (`role="paddedcontainer"`, padding `20px 15px 0px 15px`) ya alinea todos los módulos, y cada módulo tiene su propio padding según tenga o no fondo (`body_container_background_padding`, ver 2.6) — no se agregan márgenes/padding nuevos por fuera de esos dos sistemas para lograr espaciado; para eso están los separadores.

| Clase | Tamaño | Cuándo se usa | Módulos donde se usa |
|---|---|---|---|
| `.separador` | 16px | Entre dos `role="module"` consecutivos del mismo tipo. Obligatorio. También se usa como separador de nivel superior entre banner y CTA, entre CTA y el wrapper de contenido (doble, 32px), y antes del cierre. | Cierre (05_closing), banner→CTA, CTA→contenido |
| `.separador-M` | 10px | Entre dos `role="componente"` dentro del mismo módulo. | 1 Columna |
| `.separador-S` | 4px | Spacing muy fino para casos especiales. | 3 Columnas, Beneficios, Bullet (+ variantes S/M/L), Bullet numerado, Cupones, Título — 7 módulos |

Catálogo de referencia (snippet HTML de los 3, con comentario identificador por tamaño) ◀ NUEVO: `02-components/04_content-modules/content_moleculas/molecula_separadores.html` y `02-components/02_banners/banner_moleculas/molecula_separadores.html` — mismo contenido, uno por contexto. No confundir con `content_moleculas/molecula_separador_s.html`, que es una línea decorativa (`role="molecula-separador"`), no un espaciador.

### 2.5 · Tokens de radio

El sistema define **7 tokens semánticos** de `border-radius`. La capa importa: un módulo de primer nivel usa un radio más grande que sus subdivisiones internas. Los CTAs son pills (radio máximo); las imágenes nunca llevan radio propio — siempre clipean por su contenedor.

| Token | Valor | Cuándo se usa |
|---|---|---|
| `mail/radius-chip` | 3px | Tags pequeños inline ("Descuento Pro" en banner, marcas de tag en deals). |
| `mail/radius-inner-s` | 6px | Chips/pills pequeños internos. ⚠ Auditoría: 0 archivos con este valor real hoy — token sin uso vigente. |
| `mail/radius-inner-m` | 8px | Subdivisiones dentro de un módulo: cupón individual, celda de logo, columna de 3 Columnas, tag del deal. |
| `mail/radius-module-m` | 12px | Contenedor de organismo estándar: 3 Columnas, Beneficios, Cupones, Logos, 2 Columnas, Contenido, Small Deal. |
| `mail/radius-module-l` | 16px | Contenedor "hero": Big Banner Deal Destacado, Big Deal. |
| `mail/radius-pill-cta` | 50px | CTA interno del deal ("AL CARRITO"). ⚠ Auditoría: solo sobrevive en `deal-large.backup.html` — el `deal_columnas.html` vigente usa `body_container_background_radius-peq` (8px) en su lugar. |
| `mail/radius-pill` | 55px | CTA principal del mail (las 5 variantes de `style_Look`). |

**Regla de anidamiento:** contenedor de primer nivel → 12 o 16 · contenedor anidado dentro de un módulo → 8 (mitad del padre) · chip/tag dentro de un contenedor anidado → 3 o 6 · CTAs y pills → 50 o 55. Excepción: el Big Banner Deal Destacado usa 16 aunque sea de primer nivel — es "hero" y se distingue del resto.

**Imágenes:** nunca llevan `border-radius` propio — el redondeo viene del contenedor que las clipea con `overflow: hidden`. Única excepción histórica: el Módulo Logos aplica `border-radius: 7px` en el `<td>` de cada celda (no en el `<img>`).

**Auditoría de uso real en código** (barrido de `border-radius` en `02-components/`, excluye `template_maestro` y backups) — valores literales que existen hoy y no forman parte de la escala de 7 tokens:

| Valor real | Nº archivos | Módulos | Estado |
|---|---|---|---|
| 5px | 40 | Headers — cobranding en las 10 marcas | ⚠ Muy recurrente, candidato a nuevo token |
| 7px | 18 | Banners, 3 Columnas, Beneficios, Bullet, Content-moléculas, Deals, Logos — 7 categorías | ⚠ NO es una excepción única de Logos |
| 10px | 11 | Headers, 2 Columnas, Deals, Logos | ⚠ Cercano a `-inner-m` (8px) pero no igual |
| 14px | 7 | Big Banner, tags de Banner, Content-moléculas, Cupones, Deals | ⚠ Recurrente en tags y banners "hero" |
| 0px | 3 | Banners, 1 Columna, Cupones | Caso puntual — reseteo intencional |
| 30px | 3 | Banners (pastilla), Content-moléculas (pastilla), Cupones | Caso puntual — pastillas de texto |
| 20/40/60/100/150px | 1 c/u | Content-moléculas, CTA template, Footer | Casos puntuales, no son tokens del sistema |

### 2.6 · Tokens de padding

El sistema define 3 variables Liquid de padding que cambian según el tema o un toggle — no son valores fijos como el border-radius.

| Token | Valor | Nº temas | Módulos donde se usa |
|---|---|---|---|
| `padd_banner_mail_general` | `'0px 0px'` | 7 (pastel) | Banners — `big-banner-horizontal.html`, `big-banner-vertical.html` |
| `padd_banner_mail_general` | `'15px 10px'` | 5 (dark + premium) | Banners — mismos archivos |
| `padd_deal_mail_general` | `'5px 0px'` | 10 (pastel + dark neutro) | Deals — `deal_columnas.html` |
| `padd_deal_mail_general` | `'6px 8px'` | 2 (Pro, ProBlack) | Deals — mismo archivo |
| `body_container_background_padding` | `'10px'` | 12 — estado por defecto `'Fondo'` | Content-modules: 1/2/3 Columnas, Wrapper, Beneficios, Bullet, Logos, Título — 8 módulos |
| `body_container_background_padding` | `'0px'` | 12 — toggle `'Sinfondo'` | Mismos 8 módulos |
| `body_container_background_padding-peq` | `'7px'` | 12 | Content-modules: 3 Columnas (`divcomponentes` de cada una de las 3 celdas) ◀ NUEVO — hermano de `body_container_background_radius-peq` (2.5); se usaba en el HTML sin estar asignado en ningún tema, agregado a los 12 en `head-meta-tags.html` |

---

## 3 · Temas

*(Figma → hoja "Temas")*

### Los 12 temas

| Grupo | Comportamiento | Temas |
|---|---|---|
| **Pastel** (7) | Fondos claros y suaves | Beige 100, Beige 150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Gris 100 |
| **Invertidos** (3) | Fondo oscuro por defecto | Dark neon, Dark Turbo, Dark Neutro |
| **Premium** (2) | Fondo fijo, look editorial | Pro, ProBlack |

### Qué documenta cada card de tema

Cada una de las 12 cards en Figma registra el mismo set de ~19-21 tokens (varía si el tema tiene banner con tono/gradiente propio), en modo LIGHT y DARK:

Fondo · Texto · Acento 1 · Acento 2 · Contenedor 1 · Contenedor 2 (celda) · Tag / fondo · Tag / contenedor · Tipografía tag · *(Banner · tono, solo invertidos/premium)* · *(Banner · gradiente, solo Dark neon)* · Textos legales · Imagen 1 · Imagen 2 · Imagen · fondo especial · Descuento · fondo · Descuento · texto · Créditos · fondo · Créditos · texto · Fondo body · 100% · Fondo body · 50%.

El modo **DARK** de cada card es forward-looking: el HTML actual solo implementa light mode (`head-meta-tags.html` dice explícitamente "Light mode únicamente"). Los valores DARK documentados en Figma son la referencia para cuando el sistema soporte dark mode real.

### Colores por tema (light mode)

**Identidad — fondo, texto y acentos:**

| Tema | Grupo | Fondo | Texto | Acento 1 | Acento 2 |
|---|---|---|---|---|---|
| Beige 100 | Pastel | `#FFF0DD` | `#633D11` | `#D89950` | `#FF441F` |
| Beige 150 | Pastel | `#F9DFC6` | `#633D11` | `#D89950` | `#FF441F` |
| Rosa 100 | Pastel | `#FBE8FD` | `#4F145E` | `#B451C0` | `#FF441F` |
| Púrpura 100 | Pastel | `#E8E2FB` | `#0B1066` | `#7C52D8` | `#FF441F` |
| Celeste 100 | Pastel | `#C8E9FE` | `#0F3749` | `#4DA5CB` | `#FF441F` |
| Verde 100 | Pastel | `#CBFCD9` | `#00453E` | `#248F63` | `#FF441F` |
| Gris 100 | Pastel | `#ECEFF3` | `#191919` | `#7D8188` | `#FF441F` |
| Dark neon | Invertido | `#040404` | `#E2E2E2` | `#FFEBC2` | `#FF441F` |
| Dark Turbo | Invertido | `#040404` | `#E2E2E2` | `#F2ED93` | `#FF441F` |
| Dark Neutro | Invertido | `#040404` | `#E2E2E2` | `#FFEBC2` | `#FF441F` |
| Pro | Premium | `#121212` | `#EEEEEE` | `#DAA868` | `#A2A2A2` |
| ProBlack | Premium | `#ECEFF3` | `#191919` | `#D89950` | `#919AAA` |

`color_acento2_mail_general` (Acento 2) es el rojo Rappi `#FF441F` en TODOS los temas — excepto Pro (`#A2A2A2`, gris) y ProBlack (`#919AAA`, gris), que son premium y usan gris en su lugar.

**Contenedores, descuento y créditos:**

| Tema | Contenedor 1 | Contenedor 2 | Descuento (fondo / texto) | Créditos (fondo / texto) |
|---|---|---|---|---|
| Beige 100 | `#F2D3AE` @50% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Beige 150 | `#E5B67F` @50% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Rosa 100 | `#DFB0E4` @40% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Púrpura 100 | `#C2AEF2` @40% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Celeste 100 | `#7DBFDC` @40% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Verde 100 | `#48846C` @30% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Gris 100 | `#DCDFE3` @50% | `#FFFFFF` @50% | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Dark neon | `#1D1D1D` | `#2A2B2B` | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Dark Turbo | `#1D1D1D` | `#2A2B2B` | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Dark Neutro | `#1D1D1D` | `#2A2B2B` | `#FBDB20` / `#000000` | `#29D884` / `#083410` |
| Pro | `#1D1D1D` | `#040404` | `#F8D263` / `#000000` | `#CC984E` / `#FEE4C0` |
| ProBlack | `#FBFBFB` | `#FBFBFB` | `#F8D263` / `#000000` | `#CC984E` / `#FEE4C0` |

Descuento y créditos son constantes universales para Pastel + Invertidos (amarillo/verde Rappi); Pro y ProBlack son los únicos con su propia variante dorada — coincide 1:1 con la paleta primitiva de la sección 2.1.

Estas tablas cubren los tokens de identidad visual más consultados. Para el resto (Tag/fondo, Tag/contenedor, Tipografía tag, Imágenes, Banner tono/gradiente, y el modo DARK completo) ver la card del tema en Figma → Temas, o `05-docs/GUIA-DE-TEMAS.md`.

### Particularidades por tema

| Tema | Particularidad |
|---|---|
| Beige 100 | Cálido base. Imágenes y gradiente conservan su tono en dark. |
| Beige 150 | Beige más saturado. Gradiente `#D89950`. |
| Rosa 100 | Acento 1 (`#B451C0`) es acento/gradiente, **no** el color de oferta (ofertas = Acento 2). |
| Púrpura 100 | Estructura estándar. Gradiente `#7C52D8`. |
| Celeste 100 | Estructura estándar. Gradiente `#4DA5CB`. |
| Verde 100 | Acento 1 cambia en dark. Tag sobre contenedor oscuro y sólido, con tipografía de tag invertida (clara). Imagen 1 = blanco. |
| Gris 100 | Tono neutro sin dorado — la vía media entre los pasteles de color y los premium. Acento 1 gris (`#7D8188` light / `#B8BCC2` dark). Imagen no invierte en dark — se mantiene `#B8BCC2` en ambos modos. Uso: comunicaciones operativas/informativas donde no aplica ni el color ni el dorado. |
| Dark neon | Invertido: light usa tonos oscuros, dark los invierte a claros. Banner = gradiente neón (documentado, no conectado al HTML aún) + tono de banner. |
| Dark Turbo | Invertido. Banner sin gradiente: solo tono de banner verde. Tags verdes. |
| Dark Neutro | Invertido. Banner neutro sin gradiente. |
| Pro | Premium. Fondo `#121212` fijo en ambos modos → la tipografía se resuelve por superficie. Acento 2 gris. Adicionales dorados. |
| ProBlack | Premium. Fondo `#ECEFF3` fijo. Contenedores claros (light) / negros (dark). Tipografía por superficie. Adicionales dorados. |

Para el detalle variable-por-variable de cada tema (valores exactos, reglas de negocio, qué falta migrar) ver `05-docs/GUIA-DE-TEMAS.md` — esa guía es el complemento operativo de esta sección.

---

## Archivos

### `global-styles/global-styles.html`
Bloque `<style>` completo del HTML base: tipografías (sección 2.3), clases utilitarias `.separador*` (sección 2.4), reglas para `table.wrapper`, las dos media queries (`max-width: 480px` y `620px`), clases de header/banner/cupones/alineación.

### `global-styles/head-meta-tags.html`
La sección Liquid **TEMAS**: el `{% if tema_general_mail_general == '...' %}` que define, para cada uno de los 12 temas, todas las variables de la sección 2.2. (Los meta tags del `<head>` — viewport, charset, conditionals MSO — viven físicamente en `global-styles.html`, ver abajo.)

### `tokens/`
Sigue vacía. Hoy los tokens viven como clases CSS en `global-styles.html` y variables Liquid en `head-meta-tags.html`. Si se migra a archivos CSS dedicados, la referencia de valores es todo lo de arriba (y Figma).

## Por qué esto vive aparte

Cuando un diseñador quiere saber "qué color es #FF7A4D" o "cuánto es un separador-M", no debería tener que abrir un componente. Esa información vive aquí.
