# CLAUDE.md — J.A.R.V.I.S. Mail System

Contexto vivo del sistema de correos de Rappi. Aquí se registra **lo que no se deduce leyendo el código**: por qué las cosas son como son, qué decisiones ya se tomaron, qué trampas cuestan horas si se redescubren, y qué queda abierto.

Si vas a tocar colores, temas, componentes o el Figma del sistema, lee esto antes.

> **Cómo mantenerlo:** cada tanda de cambios agrega su entrada en la [§9 Bitácora](#9--bitácora) y actualiza las secciones que corresponda. Si un cambio invalida algo escrito aquí, se corrige en el sitio, no se acumulan versiones contradictorias.

---

## 1 · El repo de un vistazo

| Carpeta | Qué hay |
|---|---|
| `01-foundations/` | `global-styles/head-meta-tags.html` — **la definición de los 12 temas en Liquid**. `global-styles.html` — el `<head>` y las clases responsive. `README.md` — tokens y paleta. |
| `02-components/` | Átomos y moléculas por familia: `01_headers/` (10 marcas × 4 archivos), `02_banners/banner_moleculas/`, `03_ctas/`, `04_content-modules/`, `05_closing/`, `06_footer/`. |
| `03-templates/` | Plantillas armadas. |
| `04-assets/` | Imágenes y referencias. |
| `05-docs/` | `ATOMIC-DESIGN.md` (la especificación), `USO-DE-CADA-PARTE.md` (reglas de uso), `GUIA-DE-TEMAS.md`, `COMO-ARMAR-UN-MAIL.md`, `INDICE-DE-COMPONENTES.md`, `CHANGELOG.md`. |
| `06-examples/` | `template_maestro_original.html` — **el mail completo de referencia**. Trae su propia copia embebida de los temas y del `<head>`. `estructura_general.html` — **el esqueleto**: la estructura del mail con comentarios marcando dónde entra cada pieza, sin contenido real. |

**Dos archivos definen los temas y deben cambiarse siempre juntos:** `01-foundations/global-styles/head-meta-tags.html` y `06-examples/template_maestro_original.html`. El resto de componentes solo consume las variables.

### 1.1 · Estructura del mail — HERO y CONTENTS

Refactor iniciado el 2026-09-12. El mail se organiza en dos contenedores: **HERO** (parte superior) y **CONTENTS** (interior).

**HERO** es la tabla `role="HERO-SECTION"` de 600px, con `background-image` propio, y agrupa en orden: **header · banner · imagen full width** (la imagen es opcional).

```html
<a role="horizontal" href="AQUIELLINKDELBANNER" style="text-decoration: none; display: block; ">
<div style="display:contents;">        <!-- contents para no romper el layout de tablas -->
  <table role="HERO-SECTION" width="600" …>
    …  1 · header
       2 · banner  (dentro de <div class="mobile_paading">)
       3 · imagen full width  (sin mobile_paading)
  </table>
</div>
</a>
```

**Tres reglas que se desprenden de esto:**

1. **Un solo `<a>` para todo el HERO.** Ningún componente lleva link propio. `big-banner-horizontal.html` y `big-banner-vertical.html` tenían el suyo y se les quitó, junto con su `margin-top: 15px`. Dos `<a>` anidados no son válidos.
2. **El padding lateral en mobile lo dan los componentes**, no el contenedor, mediante la clase `mobile_paading` (con la errata en el nombre — respetarla):
   ```css
   .mobile_paading { padding-left: 15px!important; padding-right: 15px!important; }
   ```
   Vive en las dos media queries de `global-styles.html` y en la copia embebida del maestro. Va en la tabla interna de los 40 headers, en el `<div>` que envuelve cada banner y en el `<tr>` de `modulo_img_automatica_horizontal.html`. La imagen full width **no la lleva** a propósito: debe ocupar los 600px completos.
3. **El `paddedcontainer` general pasó a `padding:0px`** (antes `20px 15px 0px 15px`).

**Medidas:** el banner vertical creció de 480px a 600px y ganó `border-collapse: collapse;`. El horizontal sigue en 480px. Los 40 headers comparten la misma tabla — `width:100%; max-width: 480px; margin:0 auto;` (32) o eso más `border-radius: 10px; overflow: hidden;` (8) — y su `div id="HEADERn"` lleva `padding: 0px 0px 15px 0px`.

**CONTENTS arrancó el 2026-09-13**, pero todavía **no es una tabla propia**: por ahora es el marcador `<!-- INICIO SECCIÓN CONTENTS -->` y su contenido. **Abre con el CTA reglamentario**, que dejó de ir pegado debajo del banner. Cuando se cree la tabla contenedora en el maestro, replicarla en `estructura_general.html`. **No inventarle estructura antes de que exista allí.**

---

## 2 · Cómo trabajamos

**Superficies del sistema.** Un cambio de diseño vive en cuatro sitios a la vez:

1. El código Liquid/HTML de este repo.
2. Los `.md` de `05-docs/` y `01-foundations/README.md`.
3. El Figma **`Doc-DS-Mails`** — fileKey `7Rtnl6O6XVdhKjm3Kf8cxo`.
4. El Figma **`PLAYBOOK_MAILS_2026`** — fileKey `RpZ1t207BNfDmlqi2DU1Ic`, página `59359:8658`.

**La regla:** la superficie donde nace el cambio es la fuente de verdad y se propaga a las demás. Código y Figma no pueden divergir en silencio. Ha pasado varias veces y siempre cuesta caro descubrirlo tarde — ver [§8](#8--pendientes-y-decisiones-abiertas).

**Manual en Notion:** `powerful-author-808.notion.site/J-A-R-V-I-S-Mail-System-…`. El conector da 401, así que **nada de lo que sigue está reflejado allí**.

---

## 3 · El sistema de temas (light)

12 temas en tres familias:

| Familia | Temas |
|---|---|
| **Pastel** (7) | Beige 100, Beige 150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Gris 100 |
| **Invertidos** (3) | Dark neon, Dark Turbo, Dark Neutro |
| **Premium** (2) | Pro, ProBlack |

> Gris 100 **es pastel**, aunque algunos docs viejos digan "6 temas pastel". El criterio real es `padd_banner_mail_general = '0px 0px'`, que cumplen 7. La línea de `padd_banner` en `GUIA-DE-TEMAS.md` sigue sin corregirse.

### 3.1 · Valores por tema

| Tema | Fondo | Texto | Acento 1 | Acento 2 |
|---|---|---|---|---|
| beige100 | `#FFF0DD` | `#633D11` | `#D89950` | `#FF441F` |
| beige150 | `#F9DFC6` | `#633D11` | `#D89950` | `#FF441F` |
| rosa100 | `#FBE8FD` | `#4F145E` | `#B451C0` | `#FF441F` |
| purpura100 | `#E8E2FB` | `#0B1066` | `#7C52D8` | `#FF441F` |
| celeste100 | `#C8E9FE` | `#0F3749` | `#4DA5CB` | `#FF441F` |
| verde100 | `#CBFCD9` | `#00453E` | `#248F63` | `#FF441F` |
| gris100 | `#ECEFF3` | `#191919` | `#7D8188` | `#FF441F` |
| darkneon | `#040404` | `#E2E2E2` | `#FFEBC2` | `#FF441F` |
| darkturbo | `#040404` | `#E2E2E2` | `#F2ED93` | `#FF441F` |
| darkneutro | `#040404` | `#E2E2E2` | `#FFEBC2` | `#FF441F` |
| pro | `#121212` | `#EEEEEE` | `#DAA868` | `#A2A2A2` |
| problack | `#ECEFF3` | `#191919` | `#D89950` | `#919AAA` |

### 3.2 · Descuento y créditos ya no son constantes universales

Hasta el 2026-09-11 eran fijos para todo el sistema (`#FBDB20` amarillo y `#29D884` verde; dorados `#F8D263`/`#CC984E` en premium). **Ahora, dentro de cada tema, descuento y créditos comparten fondo y texto**, y se distinguen solo por su contenido — y por la corona en el badge de Deal.

**La regla:** el fondo es `bg_tag_fondo` del tema **con alfa 1.0 en vez de 0.5**, y el texto es `color_texto` del tema. Tres temas son la excepción, con color propio semitransparente que no deriva del tag.

| Tema | `bg_descuento` = `bg_creditos` | `color_descuento` = `color_creditos` | Contraste |
|---|---|---|---|
| beige100 / beige150 | `#E5B67F` | `#633D11` | 5.14:1 |
| rosa100 | `#CA80D2` | `#4F145E` | 4.72:1 |
| purpura100 | `#9F80E5` | `#0B1066` | 5.23:1 |
| celeste100 | `#7DBFDC` | `#0F3749` | 6.23:1 |
| **verde100** | `rgba(52,200,90,0.4)` ⚠ | `#003832` ⚠ | 6.90–9.08:1 |
| gris100 | `#C9CDD2` | `#191919` | 11.01:1 |
| darkneon / darkneutro | `#2A2B2B` | `#E2E2E2` | 10.96:1 |
| darkturbo | `#003A34` | `#E2E2E2` | 9.80:1 |
| **pro** | `rgba(204,152,78,0.5)` ⚠ | `#FEE4C0` ⚠ | 5.16–6.30:1 |
| **problack** | `rgba(204,152,78,0.5)` ⚠ | `#000000` ⚠ | 12.45:1 |

Los 12 pasan AA; 7 llegan a AAA. En los tres con alfa el contraste es un rango porque el fondo compone distinto según la superficie que tenga debajo.

**Excepciones al `color_texto` del tema:** verde100 usa `#003832` (su `color_tag_tipografia` es `#CDFAD6`, pensado para el contenedor oscuro y no sirve sobre este tono claro); pro usa el crema `#FEE4C0`; problack usa negro puro.

**Fallbacks hex ya compuestos** para los tres temas con alfa, por si hace falta un color sólido: verde100 sobre `#CBFCD9` = `#8FE7A6` · pro sobre `#121212` = `#6F5530` · problack sobre `#ECEFF3` = `#DCC4A1`.

---

## 4 · Restricciones técnicas del HTML de correo

### 4.1 · `bgcolor` no acepta `rgba()`

El atributo HTML `bgcolor` solo entiende hex o nombres de color. Si le pasas `rgba()` lo ignora y el elemento **sale sin fondo** — y lo mismo hace Outlook de escritorio en Windows (motor Word) incluso con `background-color` en CSS.

Esto importa porque tres temas usan alfa en los badges (verde100, pro, problack).

**La solución adoptada (2026-09-12):** sacar el fondo del atributo y ponerlo en un `<div>` que envuelve la tabla.

```html
<div style="background:{{bg_descuento_mail_general}}; border-radius: 7px; width: auto;
            padding: 3px 6px; display: table; margin-bottom: 7px;">
  <table style="width: auto; font-family:arial,helvetica,sans-serif;">
    …
  </table>
</div>
```

- **Horizontal:** `margin-bottom: 7px`.
- **Vertical:** `margin: 0px auto 7px auto` — **el centrado lo da el div, no la tabla**.
- El `border-radius`, el `padding` y el `display: table` se mueven al div con el fondo.

Aplicado en `template_maestro_original.html` y en las 4 moléculas de banner (`molecula_promo_horizontal|vertical`, `molecula_creditos_horizontal|vertical`).

**Siguen sin migrar** 3 usos de `bgcolor` con estos tokens: `template_maestro_original.html` líneas 1329 / 1437 / 1446, y los tags de `molecula_tag_promo.html` / `molecula_tag_verde.html`. En esos, verde100 / pro / problack renderizan el badge sin fondo.

> **Contraste:** `bg_tag_fondo` sí puede ser rgba sin problema, porque se usa exclusivamente en CSS (`background:`, 22 usos) y nunca en un atributo.

### 4.2 · Dark mode no está implementado en el HTML

El `<head>` declara `color-scheme: light only` a propósito: el auto-dark de Apple Mail reinterpretaba los colores de marca. Los valores dark de la [§5](#5--dark-mode) viven **solo en Figma**, como especificación de diseño.

---

## 5 · Dark mode

> Esta es la sección que referencian los comentarios de `head-meta-tags.html` y `template_maestro_original.html` (línea 110).

Dark existe como especificación en Figma — colección de variables `Temas`, modos `<Tema> · Dark` — pero **no está implementado en el HTML** (ver [§4.2](#42--dark-mode-no-está-implementado-en-el-html)).

### 5.1 · Valores por tema

| Tema · Dark | Fondo | Texto | Acento 1 | Contenedor 1 | Tag · fondo | Tag · texto |
|---|---|---|---|---|---|---|
| Beige 100 | `#30281B` | `#E3D9CB` | `#D89950` | `#483823` @50% | `#2C1E13` @50% | `#E3D9CB` |
| Beige 150 | `#633D11` | `#E3D9CB` | `#D89950` | `#674414` @50% | `#332A1A` @50% | `#E3D9CB` |
| Rosa 100 | `#4F145E` | `#FBE8FD` | `#B451C0` | `#EFACF4` @40% | `#756174` @50% | `#FBE8FD` |
| Púrpura 100 | `#0B1066` | `#E8E2FB` | `#7C52D8` | `#E8CCFF` @40% | `#655E77` @50% | `#E8E2FB` |
| Celeste 100 | `#0F3749` | `#C8E9FE` | `#4DA5CB` | `#9CE2FF` @40% | `#526168` @50% | `#C8E9FE` |
| Verde 100 | `#00453E` | `#CDFAD6` | `#34936B` | `#38856B` @30% | `#526168` @50% | `#00453E` |
| Gris 100 | `#1D1D1D` | `#F5F5F5` | `#B8BCC2` | `#3A3A3A` @50% | `#2A2A2A` @50% | `#F5F5F5` |
| Dark neon | `#FBFBFB` | `#1D1D1D` | `#42331E` | `#E2E2E2` | `#D8D9D9` | `#1D1D1D` |
| Dark Turbo | `#FBFBFB` | `#1D1D1D` | `#27421E` | `#E2E2E2` | `#78BEB6` | `#1D1D1D` |
| Dark Neutro | `#FBFBFB` | `#1D1D1D` | `#42331E` | `#E2E2E2` | `#D8D9D9` | `#1D1D1D` |
| Pro | `#121212` | `#191919` | `#71440A` | `#E2E2E2` | `#71440A` @50% | `#191919` |
| ProBlack | `#ECEFF3` | `#EEEEEE` | `#71440A` | `#040404` | `#71440A` @50% | `#EEEEEE` |

`contenedor/2` es `#000000` @50% en los 12 (pero ver [§8](#8--pendientes-y-decisiones-abiertas): hay sospecha de que sea un rellenado en bloque). `acento/2` mantiene `#FF441F` salvo Pro `#7F7F7F` y ProBlack `#919AAA`. `legales` es `#7D8188` salvo los pastel, que usan su propio texto.

### 5.2 · Descuento y créditos en dark

Mismo criterio que en light: dentro de cada tema comparten fondo y texto.

| Tema · Dark | Fondo | Texto | Contraste |
|---|---|---|---|
| Beige 100 | `#3C301F` | `#E3D9CB` | 9.21:1 |
| Beige 150 | `#654113` | `#E3D9CB` | 6.49:1 |
| Rosa 100 | `#773A84` | `#FBE8FD` | 6.63:1 |
| Púrpura 100 | `#423F8C` | `#E8E2FB` | 7.20:1 |
| Celeste 100 | `#326277` | `#C8E9FE` | 5.25:1 |
| Verde 100 | `#11584C` | `#CDFAD6` | 7.23:1 |
| Gris 100 | `#2C2C2C` | `#F5F5F5` | 12.81:1 |
| Dark neon / Dark Neutro | `#E2E2E2` | `#1D1D1D` | 13.01:1 |
| Dark Turbo | `#78BEB6` | `#1D1D1D` | 7.90:1 |
| Pro | `#6F5530` | `#FEE4C0` | 5.66:1 |
| ProBlack | `#DCC4A1` | `#000000` | 12.45:1 |

**Cómo se derivaron** (reusar esta regla si aparece un tema nuevo): el fondo del badge es la **superficie elevada del tema en dark** — `contenedor/1` compuesto sobre `fondo` y aplanado a hex opaco — y el texto es el `texto` dark del tema. Es el inverso de la regla de light, y sigue el principio de Material de que en oscuro una superficie que sobresale se aclara en vez de proyectar sombra.

Excepciones: en Rosa, Púrpura y Celeste se bajó el alfa del contenedor de 0.40 a 0.25 antes de aplanar, porque al 0.40 quedaban tonos medios saturados que vibran contra el fondo (Celeste fallaba con 3.66:1). Dark Turbo usa su teal de tag `#78BEB6` para no perder identidad — con la regla general los tres invertidos compartirían `#E2E2E2`. Pro y ProBlack conservan el dorado, igual que en light.

### 5.3 · Particularidades que NO son errores

- **Los temas invertidos tienen el modo dark claro** (`fondo #FBFBFB`). Es coherente: su modo light ya es oscuro.
- **En los premium el texto se lee sobre el contenedor, no sobre el fondo.** Pro dark tiene `texto #191919` sobre `fondo #121212` (sin contraste) pero `contenedor/1 #E2E2E2`; ProBlack es al revés. No lo "corrijas" sin mirarlo renderizado.
- El `fondo` dark de varios pastel coincide con la tipografía light **vieja** de ese tema (Beige150 `#3D2C1A`, Rosa `#312334`, Púrpura `#2F2C3F`, Celeste `#123344`, Verde `#102E14`). Es una convención de diseño invertido en el Playbook, no un valor obsoleto — pero **en `Doc-DS-Mails` sí se actualizaron** a los valores de la tabla de §5.1. Si ves ambos, no son la misma cosa.

---

## 6 · Componentes con reglas propias

### 6.1 · Header

10 marcas × 2 estructuras (centrado / columnas) × 2 fondos (claro / oscuro) = 40 archivos en `02-components/01_headers/`, más el `_header-wrapper.html` común.

**El tamaño lo determina la marca**, no se elige. Px de Figma, escritorio / mobile:

| Grupo | Marcas | Logo | Cob S | Cob M | Cob L | Cob XL |
|---|---|---|---|---|---|---|
| 1 | Rappi, Travel, SoyRappi | 70/63 | 77/69 | 84/76 | 95/86 | 107/97 |
| 2 | Turbo, Pro, ProBlack, Defensoría | 60/54 | 66/59 | 72/65 | 82/75 | 93/87 |
| 3 | Turbo Rest | 80/72 | 88/79 | 96/86 | 109/100 | 124/116 |
| 4 | RappiEntregador, Contenido aliado | 50/45 | 55/50 | 60/54 | 67/61 | 75/69 |

La razón cobranding/logo es constante — ×1.1 (S), ×1.2 (M), ×1.36 (L), ×1.55 (XL) — y sirve para derivar cualquier marca nueva. En HTML son 20 clases (`logo-base1..4` + `cobranding-s|m|l|xl` por `#HEADER1..4`); desktop inline en los 40 archivos, mobile en `global-styles.html`.

**Los números del cobranding son topes, no medidas fijas** (2026-09-14). El cobranding va `width: auto; height: auto` dentro de `max-width: 180px` × `max-height: Npx`, para que un logo aliado apaisado baje de alto en vez de deformarse. Antes `height`/`max-height`/`min-height` tenían el mismo valor clavado y la imagen se aplastaba al topar los 180px. La corrección tiene dos mitades y **ambas son necesarias**: el inline en los 160 `<img>` de los 40 archivos más el maestro, y los 32 bloques `.cobranding-*` de `global-styles.html` — que llevan `!important` y, sin tocar, pisaban el arreglo en mobile. Cada `<img>` conserva el atributo HTML `height="N"` como respaldo para Outlook de escritorio, que ignora `max-width`/`max-height`. Los `logo-base*` **no** se tocaron: son logos de marca, de proporción conocida, y ahí el alto clavado es correcto.

**El divider** tiene dos reglas que no se deducen de nada:

1. **Solo existe cuando hay cobranding**, y solo en `centrado-*`. En HTML vive dentro de la celda del cobranding — de ahí el comentario `SEPARADOR REGLAMENTARIO SIEMPRE QUE HAYA COBRANDING`. Los `columnas-*` no lo traen en ninguna marca.
2. **Su color lo define la marca, no el tema.** Hay 3 assets en total:

| Fondo | Asset | Marcas |
|---|---|---|
| Claro | Degradado coral/rojo (el del logo Rappi) | Rappi, RappiTravel, SoyRappi, Turbo, Turbo Rest, RappiEntregador |
| Claro | Sólido oscuro | Defensoría, Pro, ProBlack, Contenido aliado |
| Oscuro | Sólido blanco | las 10 |

**No es un token de tema y no debe modelarse como variable**: no cambia al pasar de Beige 100 a Rosa 100, y en 6 de 10 marcas es un degradado, que una variable COLOR de Figma no puede almacenar.

---


### 6.2 · CTA

Component set `CTA` (`1371:87`), en la sección `Ds` de `04 · Atoms`. **10 variantes**: `Color` (Tema · neon · verde · blanco · negro) × `Tamaño` (Big · Small).

**El componente es el contenedor, no el botón.** Cada variante es el frame `CALL TO ACTION`, con auto-layout vertical y su **padding inferior**, y dentro el pill. Se hizo así a propósito: ese padding separa el CTA de lo que viene debajo y tiene que viajar con el componente.

```
COMPONENT  (auto-layout VERTICAL · ancho FIXED · alto HUG · padding-bottom)
  └─ CTA   (el pill)
       Big   → layoutSizingHorizontal = FILL   (toma el ancho del contenedor)
       Small → layoutSizingHorizontal = HUG    (abraza su texto)
```

**Por qué Big usa FILL y no un ancho fijo:** si el pill tuviera 960 grabados, al pasar a Small y volver a Big no recuperaba el ancho. Con FILL, Big deriva su ancho del contenedor, así que el ciclo Big → Small → Big es reversible. Verificado.

> ⚠️ **El contenedor debe tener ancho fijo, nunca hug.** Un contenedor hug con un hijo en FILL colapsa al mínimo — es exactamente el bug que tuvo el preview de escritorio, que se encogió de 960 a 224.

El valor **`Tema`** tiene sus rellenos vinculados a `cta/fondo` y `cta/texto`, así que **sigue el modo del frame** donde vive la instancia. Los otros cuatro son overrides manuales de color fijo, equivalentes a `style_Look` en `cta-template.html`. Por eso bastan 10 variantes y no 128: los 12 temas los resuelve la variable.

**Un solo set sirve para escritorio, mobile y dark.** No hacen falta componentes separados: mobile se resuelve redimensionando la instancia, y dark lo resuelve la variable, porque `Tema` sigue el modo del frame y los 12 modos dark ya tienen su valor.

Cómo se dimensiona cada instancia — y no es igual en los tres, porque sus contenedores difieren:

| Preview | Ancho | Cómo | Padding |
|---|---|---|---|
| DESK | 960 | `FIXED` (su `CONTENIDO` mide 1200 y **no tiene padding**, así que FILL daría 1200) | 30 |
| MOBILE | 640 | `FILL` (su `CONTENIDO` mide 700 con padding 30 a cada lado) | 20 |
| DARK | 640 | `FILL` (igual que mobile) | 20 |

El padding va como override de instancia porque difiere entre dispositivos.

**Falta la propiedad `Alineado` (Left/Center).** Está bloqueada — ver pendiente #13.

**Contraste del CTA por tema:** los valores light salen de `cta-template.html`; los dark del `tag/fondo` dark sin alfa con el `texto` dark del tema encima. Dos excepciones: **Pro en dark** usa `#FFFFFF` en vez de su `texto` dark (`#191919` daba 2.12:1 sobre `#71440A`), y **Verde 100 en claro** usa `#003832` (5.93:1) porque no está definido en el código y el blanco daba 2.20:1.

---

## 7 · Figma — mapa y trampas

### 7.1 · `Doc-DS-Mails` (`7Rtnl6O6XVdhKjm3Kf8cxo`)

14 páginas. **`get_metadata` sin nodeId solo lista "🪐 Cover"** — hay que usar `use_figma` con `figma.root.children` para ver las 14.

**La colección de variables `Temas`** (`VariableCollectionId:1270:2`) es la fuente más limpia para cambiar tokens: 20 variables × **24 modos** (12 light + 12 `<Tema> · Dark`). Cambiar un token son 4 llamadas, no un barrido de nodos.

Nombres actuales: `fondo`, `texto`, `acento/1`, `acento/2`, `contenedor/1`, `contenedor/2`, `tag/fondo`, `tag/contenedor`, `tag/texto`, `legales`, `imagen/1`, `imagen/2`, `descuento/fondo`, `descuento/texto`, `creditos/fondo`, `creditos/texto`, `fondo-body/100`, `fondo-body/50`, `cta/fondo`, `cta/texto`.

**`cta/fondo` y `cta/texto`** (creadas el 2026-09-13) son las que hacen que el CTA de los previews cambie con el tema. Su valor **no es el mismo que el del badge**: coincide en 9 temas, pero Verde 100 va sin alfa (`#34C85A`), y Pro y ProBlack usan blanco y negro en vez del dorado. En los 12 modos dark el fondo es el `tag/fondo` dark sin alfa y el texto es el `texto` dark del tema — salvo Pro, que necesita `#FFFFFF` porque su `texto` dark (`#191919`) daba 2.12:1 sobre `#71440A`. La fuente de los valores light es `02-components/03_ctas/cta-template.html`.

**Convención de ubicación:** cada componente que se crea vive **junto a su hoja de documentación**, dentro de una sección llamada `Ds` en esa misma página. El header, documentado en `5.1 · Header`, tiene sus component sets en la sección `Ds` de `05 · Molecules`.

**Nodos clave** (verificados el 2026-09-12 — el archivo se reorganiza seguido, confirma antes de confiar en un id):

| Nodo | Página | Qué es |
|---|---|---|
| `568:24535` | `03 · Temas` | `TEMAS · Sistema actualizado (12)` — las 12 tarjetas de tema, **fuente de verdad de color** |
| `600:151` | `05 · Molecules` | `5.1 · Header (Logo + Cobranding)` — la guía de tamaños y composición |
| `1344:2` | `05 · Molecules` | Sección `Ds` — contenedor de los componentes de esta página |
| `1339:3113` / `1339:6164` | `05 · Molecules` → `Ds` | Component sets `Header · Desktop` / `Header · Mobile` |
| `1371:87` | `04 · Atoms` → `Ds` | Component set `CTA` (10 variantes) |
| `1333:783` / `1333:798` / `1333:813` | `07 · Templates` | `PREVIEW DESK` / `PREVIEW_MOBILE` / `PREVIEW_DARK` |

> **Mover entre páginas cambia los ids.** Los previews pasaron de `03 · Temas` a `07 · Templates` y sus ids cambiaron por completo (`1315:78/91/104` → `1333:783/798/813`). Mover por script con `appendChild` sí conserva el id — así se movieron los component sets, y por eso sus instancias no se rompieron. Si un id de esta tabla devuelve `null`, busca por nombre antes de darlo por perdido.

**Estructura de una tarjeta de tema:** 3 columnas hermanas — `[TOKEN, LIGHT, DARK]`. La de TOKEN tiene celdas de 1 hijo TEXT (el nombre de la fila); LIGHT y DARK tienen celdas de 2 hijos `[swatch, TEXT con el hex]`. **Mapea por la etiqueta de TOKEN, nunca por índice**: el número de filas varía por tema. Las tarjetas **no llevan el nombre del tema como texto** — se identifican por la tríada fondo/texto/acento1 de las celdas 1/2/3.

**La hoja `TEMAS_PRVIEW`** (auditada en septiembre, ver §9) **fue eliminada del archivo**, igual que las dos hojas `MODULO` de 28511px con el arte de headers del que se cosecharon los 10 logos. El arte sobrevive dentro de los component sets; si hace falta el original hay que recuperarlo del historial de versiones de Figma.

**Los component sets de header son los primeros componentes del archivo.** Antes no había ni un COMPONENT ni un COMPONENT_SET en ninguna página: todo eran frames sueltos. Si buscas "el componente de X" y no aparece, es por eso.

### 7.2 · Trampas que ya costaron tiempo

- **Busca por color de relleno, no por contenido de texto.** Las tarjetas por tema pintan *todo* su texto descriptivo con la tipografía de ese tema. `characters.includes(hex)` no encuentra casi nada; hay que escanear `fills[0].color` de cada TEXT. ~52-55 nodos por tarjeta.
- **Audita con tolerancia amplia, muta con hex exacto.** Un barrido con tolerancia marcó `#2a2a2a` como si fuera `#2A2B2B`.
- **Un hijo `BODY` puede tapar el frame que acabas de corregir.** En los previews mobile del Playbook, los frames `LIGHT`/`DARK` tienen un hijo `BODY` del mismo tamaño con su propio fill. Recolorear solo el padre se ve bien en el árbol de capas y no cambia nada en pantalla.
- **Redimensionar una instancia con `resize()` deja un override que rompe el cambio de variante.** Pasó con el CTA: la instancia de mobile, redimensionada de 960 a 640, arrastraba un override de ancho en el texto; al pasar a `Small` el pill no podía abrazar y quedaba en 652px, más ancho que su contenedor. La cura es `instance.resetOverrides()` y después dejar que el ancho venga del contenedor (`layoutSizingHorizontal='FILL'`) o reafirmarlo explícitamente. Ojo: `resetOverrides()` también borra el padding y el nombre, hay que volver a ponerlos.
- **Las medidas leídas justo después de mutar salen en caliente y mienten.** Tras un `setProperties` o un cambio de layout, `width` puede devolver el valor viejo dentro de la misma ejecución. Al leerlo en una llamada nueva aparece el valor real. Costó un rato creer que un wrapper se estiraba a 1200 cuando en frío estaba en 960. Si una medida no cuadra, vuelve a leerla en otra ejecución antes de "arreglarla".
- **Tras `setExplicitVariableModeForCollection`, la primera captura puede salir con el render viejo.** Verifica con `variable.resolveForConsumer(node)` antes de concluir que el cambio falló.
- **No todo lo amarillo o dorado es un badge.** En `07 · Templates`, `chip` y `credit-tag` sí; `col-icon` (10 nodos en Pro/ProBlack) y el `block` de `cupon-ticket` no. En `04 · Atoms`, las dos `Ellipse` `#F8D263` de las preview rows tampoco.
- **Beige 100 y Beige 150 se diferencian en solo dos colores** — Fondo (`#FFF0DD` vs `#F9DFC6`) y Contenedor 1 (`#F2D3AE`@50% vs `#E5B67F`@50%) — más 4 imágenes. Como su tipografía ahora es idéntica, una confusión entre ambos es invisible a cualquier chequeo de tipografía.
- **`#E5B67F` es legítimo dentro de Beige 100** como Tag·fondo. Un reemplazo ciego rompe los tags: clasifica por rol antes de mutar.

### 7.3 · `PLAYBOOK_MAILS_2026` (`RpZ1t207BNfDmlqi2DU1Ic`)

Página `59359:8658`. Recibió los cambios 1, 2 y 3 (ver [§9](#9--bitácora)). **No tiene aún la unificación de badges.**

Cabos sueltos marcados y no resueltos: `61927:18241` (fondo dark de la leyenda Beige100 en `#30281B`, que no cumple ninguna convención) · `60134:40716` (un `IMG2` en DARK en `#E5B67F`, fuera de patrón) · MODULO `59403:11884` (una instancia "Beige Pastel 150" con tonos lavanda que no corresponden a ningún tema beige, y dos previews "New Beige" con estructura de exploración, probablemente WIP).

---

## 8 · Pendientes y decisiones abiertas

| # | Qué | Dónde | Estado |
|---|---|---|---|
| 1 | Unificación de badges sin propagar | `PLAYBOOK_MAILS_2026` | Pendiente |
| 2 | `tag/texto` desactualizado en las variables de Figma vs. el código: Beige100 `#2B2316`, Beige150 `#3D2C1A`, Rosa `#312334`, Púrpura `#2F2C3F`, Celeste `#123344`, Verde `#102E14`, Pro `#191919` — el código dice `#633D11`, `#633D11`, `#4F145E`, `#0B1066`, `#0F3749`, `#CDFAD6`, `#EEEEEE` | `Doc-DS-Mails` | **Requiere decisión** |
| 3 | `contenedor/2` dark: la hoja `TEMAS_PRVIEW` dice `#D8D9D9` / `#FBFBFB` / `#040404` en invertidos y premium; la variable dice `#000000` @50% en los 12. Sospecha: rellenado en bloque en las tarjetas | `Doc-DS-Mails` | **Requiere decisión** |
| 4 | Los 3 usos restantes de `bgcolor` con tokens rgba (maestro 1329/1437/1446 y los dos `molecula_tag_*`) | Repo | Pendiente |
| 5 | En `molecula_creditos` horizontal del maestro, el monto usa las variables de **promo** (`banner_copy_modulo_prom_class`, `_promo_fontsize`, `_promo_lineheight`, `color_descuento_mail_general`). Debería usar las de créditos: esas clases se calculan por el largo del texto | `template_maestro_original.html` | Detectado, sin corregir |
| 6 | Renombrado de variables de Figma a `fondo_*` / `texto_*` / `acento_*` que propone `sistema-temas-mails.md` §3. `variable.name = nuevo` conserva el ID, así que no rompe vinculaciones | `Doc-DS-Mails` | Propuesto, no hecho |
| 7 | Contenido aliado: su logo está dibujado a 31px, no a los 50px del grupo 4. Es un wordmark de texto y escalarlo cambiaría el diseño | Figma + docs | **Requiere decisión** |
| 8 | La línea de `padd_banner` dice "6 temas pastel"; son 7 | `GUIA-DE-TEMAS.md` | Pendiente |
| 9 | `CHANGELOG.md` no tiene entradas de nada de esto | Repo | Deliberado hasta ahora |
| 10 | `CONTENTS` existe como marcador y ya contiene el CTA reglamentario, pero **aún no es una tabla contenedora** como sí lo es `HERO-SECTION`. Cuando se cree en el maestro, replicarla en `estructura_general.html` | `template_maestro_original.html` | En curso |
| 11 | El `<a>` que envuelve el HERO conserva `role="horizontal"`, que era el rol del banner horizontal. Si dentro van a convivir header y ambos tipos de banner, ese atributo queda describiendo algo que ya no es | `template_maestro_original.html` | A definir al meter los banners |
| 13 | **Al componente `CTA` le falta la propiedad `Alineado` (Left/Center)**: el arte de referencia (`FORMATO`, `1358:1017`) usa Helvetica y esa familia no existe en el entorno del MCP, lo que bloquea `textAlignHorizontal` y el re-medido del texto. Se desbloquea duplicando en esa hoja un CTA big con el texto alineado a la izquierda, para clonar de ahí | `Doc-DS-Mails` | **Bloqueado** |
| 14 | Contraste del CTA: Púrpura 100 en claro da 3.29:1 (`#9F80E5` + `#4C2B8C`), por debajo de AA. El valor viene de `cta-template.html`, así que corregirlo implica tocar el código. Su `texto` de tema (`#0B1066`) daría 5.23:1 | `cta-template.html` + Figma | **Requiere decisión** |
| 12 | En el header de ejemplo del maestro, el primer cobranding perdió su `class="cobranding-s"` (las otras tres sí la tienen). Confirmado como error; **no se replicó** a los 40 archivos, que la conservan | `template_maestro_original.html` | Sin corregir en el maestro |


---

## 9 · Bitácora

### 2026-09-14 · El cobranding deja de deformarse

Un logo aliado más ancho de `max-width: 180px` se aplastaba: el alto estaba clavado tres veces (`height` + `max-height` + `min-height` al mismo número), así que al topar el ancho el alto no podía ceder. Pasa a `height: auto` + `max-height`, y se le añade el atributo HTML `height="N"` como respaldo para Outlook de escritorio.

Probado primero en el maestro y, confirmado por el usuario, replicado a **los 160 `<img>` de los 40 headers** y a **los 32 bloques `.cobranding-*` de `global-styles.html`** — esta segunda mitad es imprescindible: esas reglas llevan `!important` y sin tocarlas el arreglo inline se perdía en mobile.

Los `logo-base*` se dejaron con alto fijo a propósito: son logos de marca, de proporción conocida.

**El mismo defecto estaba en la firma del footer** (`02-components/06_footer/footer_general.html`, el `<img>` de `{{img-firma}}`): `height`/`min-height`/`max-height` clavados en 25px contra un `max-width: 200px`, así que las firmas anchas —Turbo Colombia, por ejemplo— se aplastaban. Corregido igual, aunque aquí bastó el inline: `.altofooter1` afecta al `<td>`, no a la imagen, así que no hay ninguna regla con `!important` que pisar. `footer_rts.html` ya estaba bien; `footer_sinamor.html` asigna `img-firma` pero nunca la pinta.

**Y en el "Logo pastilla" de Deals**, 4 instancias con la misma forma (`height: 23px; max-height: 23px; min-height: 23px` contra `max-width: 150px`): `deal_columnas.html` y el maestro, dos en cada uno. Era el caso más expuesto —una pastilla es apaisada por definición y 150px es un tope estrecho—. **El `max-width: 150px` se dejó tal cual a pedido del usuario**: solo se liberó el alto.

**Regla general que sale de esta tanda:** una imagen con `max-width` **nunca** debe llevar el alto clavado. El patrón correcto es `width: auto; height: auto` + los dos topes + el atributo `height="N"` para Outlook. Tras el barrido del 2026-09-14 **no queda ningún caso** en el repo con la forma vieja; si aparece uno nuevo, es un error de copia.

Un alto clavado **sin** `max-width` sí es legítimo y no se tocó: no puede toparse con nada, por eso el logo de WhatsApp del footer y los `logo-base*` siguen igual.

Documentado en `05-docs/ATOMIC-DESIGN.md` §5.1, `05-docs/USO-DE-CADA-PARTE.md` (Regla #3) y §6.1 de este archivo.

### 2026-09-14 · El CTA pasa a ser componente

Nace el component set `CTA` (`1371:87`) en la sección `Ds` de `04 · Atoms`: `Color` (Tema · neon · verde · blanco · negro) × `Tamaño` (Big · Small) = 10 variantes. Los tres CTA de los previews se reemplazaron por instancias.

El componente es el contenedor `CALL TO ACTION` con su padding inferior, no solo el pill — ver §6.2. Reconstruido el mismo día tras detectar que con el pill de ancho fijo el ciclo Big → Small → Big no era reversible, y que el contenedor hug de escritorio colapsaba a 224.

El valor `Tema` está vinculado a `cta/fondo` y `cta/texto`, así que sigue el modo del frame; los otros cuatro son overrides fijos. Eso evitó tener que crear un valor por tema: 10 variantes en vez de 128.

Un solo set sirve para escritorio y mobile — la instancia se redimensiona (960 / 640) y el texto FILL la sigue.

### 2026-09-13 · El CTA de los previews sigue al tema

Nacen las variables `cta/fondo` y `cta/texto` en la colección `Temas`, pobladas en los 24 modos (48 valores), y los tres CTA de los previews (`PREVIEW DESK`, `PREVIEW_MOBILE`, `PREVIEW_DARK`) quedan vinculados a ellas. Cambiar el modo del frame ya cambia el color del botón. Verificado de punta a punta con 6 temas.

Los valores light salen de `cta-template.html`; los dark del `tag/fondo` dark sin alfa, con el `texto` dark del tema encima.

**El componente de CTA no se pudo construir**: el arte de referencia usa Helvetica y esa familia no existe en el entorno de Figma del MCP, lo que bloquea `textAlignHorizontal` y el re-medido del texto. Ver pendiente #13.

### 2026-09-13 · Arranca CONTENTS y se mueve el CTA reglamentario

El maestro suma el marcador `<!-- INICIO SECCIÓN CONTENTS -->` y el comentario `<!-- COMPONENTE IMAGEN FULL WIDTH -->`, y se limpian los comentarios sobrantes del banner que habían quedado tras el refactor del HERO.

**Cambia una regla del sistema:** el CTA reglamentario ya no va pegado debajo del banner — ahora es el **primer elemento de CONTENTS**. Actualizado en `05-docs/USO-DE-CADA-PARTE.md` (nueva Regla #1 de la sección 4, con las otras tres renumeradas), `05-docs/COMO-ARMAR-UN-MAIL.md`, `05-docs/ATOMIC-DESIGN.md` §6.0 y `06-examples/estructura_general.html`.

CONTENTS todavía **no es una tabla contenedora** como `HERO-SECTION`: es el marcador y su contenido.

### 2026-09-13 · HERO completo: banner e imagen full width

El HERO pasa de contener solo el header a contener **header · banner · imagen full width**. Los dos banners se insertan dentro de un `<div class="mobile_paading">`; el vertical creció a 600px con `border-collapse: collapse`. Nace `02-components/02_banners/imagen-full-width.html`.

Propagado a: los 40 headers (`div id="HEADERn"` a `padding: 0px 0px 15px 0px` y se les quitó el `bgcolor=""` de la tabla), los dos archivos de banner, `modulo_img_automatica_horizontal.html` (clase en su `<tr>`), `estructura_general.html` (HERO con los tres huecos comentados) y los docs: `02-components/README.md`, `05-docs/ATOMIC-DESIGN.md` (nueva §6.0), `05-docs/COMO-ARMAR-UN-MAIL.md` y `05-docs/INDICE-DE-COMPONENTES.md`.

`global-styles.html` no necesitó cambios: el CSS del maestro y el del foundation son idénticos.

### 2026-09-12 · Refactor de estructura: HERO

Nace el contenedor `HERO-SECTION` y el `<a>` del banner pasa a envolverlo (ver §1.1). Propagado a los 40 headers (clase `mobile_paading` + anchos unificados), a los dos archivos de banner (se les quitó el `<a>` propio y el `margin-top`), a `global-styles.html` (la clase en las dos media queries) y a `estructura_general.html` (HERO completo + `paddedcontainer` a `padding:0px`).

`CONTENTS` queda pendiente de crear en el maestro.

### 2026-09-12 · Reorganización del Figma

Los previews pasaron a `07 · Templates` (`PREVIEW DESK` `1333:783`, `PREVIEW_MOBILE` `1333:798`, `PREVIEW_DARK` `1333:813`) y los dos component sets del header a `05 · Molecules`, dentro de una sección nueva llamada **`Ds`** (`1344:2`) — junto a su hoja de documentación, que es la convención a seguir de aquí en adelante.

Los sets se movieron por script con `appendChild`, así que conservaron sus ids y las 2 instancias de los previews siguen vinculadas. Los previews, movidos a mano, sí cambiaron de id.

**Se eliminaron del archivo** la hoja `TEMAS_PRVIEW` y las dos hojas `MODULO` de 28511px con el arte de headers. El arte de los 10 logos sobrevive clonado dentro de los component sets.

### 2026-09-12 · Moléculas de banner con fondo en `<div>`

Las 4 moléculas de promo y créditos (horizontal y vertical) pasan de `<table bgcolor>` a un `<div>` con `background` en CSS, para que el `rgba()` de verde100 / pro / problack se vea. Ver [§4.1](#41--bgcolor-no-acepta-rgba). De paso se corrigieron `font-siaze` → `font-size`, llaves mal cerradas en dos comentarios y declaraciones duplicadas.

### 2026-09-11 · Header como componente en Figma

Dos component sets, `Header · Desktop` (`1339:3113`) y `Header · Mobile` (`1339:6164`), 200 variantes cada uno: `Logo` (10) × `Estructura` (2) × `Fondo` (2) × `Cobranding` (Sin/S/M/L/XL). El arte se cosechó de las hojas `1330:11481` y `1330:2738`. El cobranding es un frame vacío con relleno sólido, como marcador. Instancias colocadas en los slots `HEADERS` de ambos previews.

Documentado el comportamiento del divider, que no estaba escrito en ningún sitio — ver [§6.1](#61--header). Corregido el divider de Defensoría, que en Figma tenía un degradado sobre el sólido siendo que en HTML usa el asset sólido.

Contenido aliado no tiene versión oscura dibujada: la suya se derivó clonando la clara y pasando los fills a blanco.

### 2026-09-11 · Modos dark en variables

La colección `Temas` pasó de 12 a 24 modos, con los 12 `<Tema> · Dark` poblados en las 18 variables (216 valores). Se eligió ampliar la colección existente en vez de crear una paralela para no recablear ningún nodo. `PREVIEW_DARK` quedó apuntando a `Púrpura 100 · Dark`. Ver [§5](#5--dark-mode).

### 2026-09-11 · Auditoría de `TEMAS_PRVIEW`

408 filas revisadas contra las variables: 143 discrepancias, 133 corregidas. Los tipos de error, por si reaparecen: etiquetas hex copiadas de otro tema, etiquetas con el color ya compuesto en vez del crudo, y `Fondo general` dark con valores de la convención vieja. Quedaron 10 filas sin resolver (pendiente #3).

También se corrigió la variable `fondo` de Verde 100, de `#C0FDD3` a `#CBFCD9`: aquí la hoja y el código tenían razón y la variable estaba desactualizada.

> La hoja `TEMAS_PRVIEW` fue eliminada del archivo el 2026-09-12. Las correcciones siguen válidas en las variables y en las tarjetas de tema, que son la fuente de verdad.

### 2026-09-11 · Unificación de descuento y créditos

El cambio descrito en [§3.2](#32--descuento-y-créditos-ya-no-son-constantes-universales) y [§5.2](#52--descuento-y-créditos-en-dark). Propagado a código, a `01-foundations/README.md`, `05-docs/ATOMIC-DESIGN.md`, `05-docs/GUIA-DE-TEMAS.md` y a `Doc-DS-Mails` completo (variables + 5 páginas).

En `02 · Tokens` las primitivas que dejaron de existir (`system/descuento-bg`, `system/creditos-bg`, etc.) se marcaron como obsoletas en vez de borrarse; `system/creditos-bg-pro` se reconvirtió en `system/gold-pro-badge`.

### Anteriores

1. **Fondo de Pro `#2A2B2B` → `#121212`** — completo en todas las superficies.
2. **Tipografía pastel** — `color_texto`, `color_textos_legales` y `color_tag_tipografia` a los valores de [§3.1](#31--valores-por-tema). El tag de Verde 100 es su propio `#CDFAD6` y no se toca. Completo salvo las variables de Figma (pendiente #2).
3. **Fondo de Verde 100 `#C0FDD3` → `#CBFCD9`** — completo. Ese verde lo comparte la representación *light* de Turbo; el tema "Dark Turbo" no se tocó.