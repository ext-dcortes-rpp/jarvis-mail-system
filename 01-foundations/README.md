# 01 · Foundations

> Las reglas del LEGO.

Aquí viven las reglas que cualquier brick respeta: tipografías, colores, espaciados, separadores, radios, padding, media queries. **Nadie debería tocar esta carpeta sin coordinarlo con el equipo de diseño**, porque cualquier cambio aquí afecta a TODOS los mails.

Todo lo de esta carpeta está registrado y documentado en Figma → **Doc-DS-Mails → hoja "Tokens"** (paleta, variables por tema, tipografía, separadores, radios, padding). Si hay diferencia entre el HTML y Figma, gana el HTML — Figma existe para reflejarlo, no al revés.

## Archivos

### `global-styles/global-styles.html`
Bloque `<style>` completo del HTML base con:
- Tipografías y tamaños (h1 a h6, `.legal`, y la escala `bnr-*` de "texto vivo" del banner) — ver escalas completas abajo
- Clases utilitarias (`.separador`, `.separador-M`, `.separador-S`)
- Reglas para `table.wrapper`
- Las dos media queries: `@media (max-width: 480px)` y `@media (max-width: 620px)`
- Todas las clases de header (`.header-logo`, `.header-logoturbo`, `.header-tag`...)
- Las clases de banner (`.banner-logo1-1`, `.banner-logo-multi`, `.altobanner1`)
- Las clases de cupones (`.cuponmob`)
- Las clases de alineación (`.alineado-center`, `.txtbigbanner`)

#### Escala tipográfica — body/contenido

Family: Arial/Helvetica sans-serif. `body`, `p` y `div` heredan `14px`. Los tamaños de `h1`-`h6` y `.legal` son **iguales en escritorio y en mobile** (`@media max-width: 480px` y `620px` sólo repiten el mismo valor con `!important`, no lo cambian):

| Elemento | Tamaño / interlineado (escritorio y mobile) | Dónde se usa |
|---|---|---|
| `h1` | 26px / 28px | Cupones (título grande) · precios destacados |
| `h2` | 21px / 22px | Complemento · Contenido · Columnas (encabezados de sección) |
| `h3` | 16px / 17px | Título · Logos · 2 Columnas (subtítulo) · Bullet numerado · Pastilla/Tag · Beneficios (headline) |
| `h4` | 14px / 15px | Deals (copy y CTA) · Tag con ícono · Banner (tags) · Bullet · 3 Columnas · Cupones |
| `h5` | 12px / 13px | Deals (% off, precio, categoría, rating) · Cupones (pills) |
| `h6` | 10px / 11px | Reservado en la escala — sin uso actual en los módulos del código |
| `.legal` | 8px / 9px | Legales (módulo LEGAL · Deals · Cupones) |

Las clases `.txts` y `.txtl` ya no existen en el sistema — se quitaron de `global-styles.html`.

#### Escala tipográfica — banner "texto vivo" (`bnr-*`)

Estas clases dimensionan el número/copy principal del banner (promocional, créditos, texto XL). El tamaño de **escritorio** va inline en las moléculas de `02-components/02_banners/banner_moleculas/`; `global-styles.html` solo define el override de **mobile** (`@media max-width:480px`), donde ambas orientaciones convergen al mismo valor:

| Clase | Escritorio horizontal | Escritorio vertical | Mobile (ambas orientaciones) |
|---|---|---|---|
| `.bnr-xl` | 80px / 80px | 125px / 125px | 110px / 110px |
| `.bnr-lg` | 35px / 35px | 62px / 62px | 63px / 63px |
| `.bnr-md` | 30px / 31px | 50px / 51px | 55px / 55px |
| `.bnr-hasta-xl` | 19px / 19px | 25px / 25px | 27px / 27px |
| `.bnr-hasta-lg` | 10px / 10px | 15px / 15px | 16px / 16px |
| `.bnr-sm` | 14px / 15px | 16px / 18px | 17px / 19px |

`.bnr-xl`/`.bnr-lg` se eligen dinámicamente vía Liquid según el largo del texto (variables `*_class`, `*_fontsize`, `*_lineheight` en `head-meta-tags.html`). Ver el detalle en `02-components/README.md`.

### `global-styles/head-meta-tags.html`
Los meta tags del `<head>`: viewport, charset, conditional comments para Outlook (MSO). Se inyecta antes del `<style>`.

Además, aquí vive la sección Liquid **TEMAS**: el `{% if tema_general_mail_general == '...' %}` que define, para cada uno de los 11 temas (Beige 100/150, Rosa 100, Púrpura 100, Celeste 100, Verde 100, Dark neon, Dark Turbo, Dark Neutro, Pro, ProBlack), todas las variables de color/imagen/espaciado del mail (`bg_solid_mail_general`, `color_texto_mail_general`, `color_acento1_mail_general`, `bg_contenedor1_mail_general`, `padd_banner_mail_general`, `body_container_background_padding`, etc.). Ver `05-docs/GUIA-DE-TEMAS.md` para el detalle completo de cada variable.

## Tokens

Los tokens del sistema ya están registrados — en Figma (Doc-DS-Mails → hoja "Tokens") y en el código. No es un plan a futuro: esto es lo que existe hoy.

- **Colores y variables por tema** — 11 temas × ~18 variables base (`bg_solid_mail_general`, `color_acento1/2_mail_general`, `bg_contenedor1/2_mail_general`, tags, descuento, créditos). Ver `05-docs/GUIA-DE-TEMAS.md` y Figma Tokens 2.1/2.2.
- **Tipografía** — escalas `h1`-`h6`/`.legal` y `bnr-*` de arriba. Figma Tokens 2.3.
- **Separadores** — `.separador` (16px, entre módulos), `.separador-M` (10px, entre componentes), `.separador-S` (4px, spacing fino). Figma Tokens 2.4.
- **Border-radius** — escala semántica de 7 tokens (`mail/radius-chip` 3px, `-inner-s` 6px, `-inner-m` 8px, `-module-m` 12px, `-module-l` 16px, `-pill-cta` 50px, `-pill` 55px). Una auditoría contra el código encontró varios valores reales fuera de esta escala y en uso recurrente (5px en los 10 headers, 7px en 7 categorías de módulo, 10px, 14px) — no son "errores" puntuales, son candidatos a nuevos tokens. `-inner-s` (6px) y `-pill-cta` (50px) están documentados pero sin uso vigente en componentes actuales. Ver Figma Tokens 2.5, sección "4 · Auditoría de uso real en código".
- **Padding** — 3 variables Liquid por tema, cada una con 2 valores posibles: `padd_banner_mail_general` (Banners), `padd_deal_mail_general` (Deals), `body_container_background_padding` (8 módulos de Content-modules, según el toggle `body_container_background` = `'Fondo'`/`'Sinfondo'`). Ver Figma Tokens 2.6.

La carpeta `tokens/` (CSS con variables primitivas) sigue vacía — hoy los tokens viven como clases CSS en `global-styles.html` y variables Liquid en `head-meta-tags.html`. Cuando se migre a archivos CSS dedicados, la referencia de valores es la de arriba (y Figma).

## Por qué esto vive aparte

Cuando un diseñador quiere saber "qué color es #FF7A4D" o "cuánto es un separador-M", no debería tener que abrir un componente. Esa información vive aquí.
