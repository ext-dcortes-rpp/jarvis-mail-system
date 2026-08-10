# 04 · Assets

> Imágenes y logos. La biblioteca visual del sistema.

## Dónde viven los assets

**Google Drive es el repositorio de assets** — no este repo. Se alimenta de las imágenes que el equipo de diseño exporta para el diseño de cada mail (logos, íconos, fondos, banners, pantallas, productos, etc.). Ningún archivo de imagen se sube a `jarvis-mail-system`; los componentes HTML solo referencian la **URL pública** del asset (`src="https://lh3.googleusercontent.com/d/..."`).

Todo lo que entra a Drive se organiza bajo una **taxonomía** — un nombre de archivo estandarizado que permite identificar, para cualquier asset, qué tipo es, para qué vertical del app aplica, si es de un país específico o de LATAM, si es de algún aliado/marca, y qué variante de diseño tiene. Esa taxonomía es lo que conecta Drive (dónde vive el archivo) con la fuente del mail (qué URL pegar) — sin ella, un asset no es encontrable ni reutilizable.

## La hoja de taxonomía

[TAXONOMÍA ASSETS](https://docs.google.com/spreadsheets/d/1Fb3UOeDhHnP672M6m2yD3v_Lh3zdBxNsiScUlKHVw78/edit) — un Google Sheet con dos pestañas activas:

| Pestaña | Cubre |
|---|---|
| [**Nuevo Mails**](https://docs.google.com/spreadsheets/d/1Fb3UOeDhHnP672M6m2yD3v_Lh3zdBxNsiScUlKHVw78/edit?gid=1136880940#gid=1136880940) | Íconos 3D, íconos planos, fondos, pantallas, banners, headers, cierres, tags/sellos, producto |
| [**Logos Mail**](https://docs.google.com/spreadsheets/d/1Fb3UOeDhHnP672M6m2yD3v_Lh3zdBxNsiScUlKHVw78/edit?gid=3113695#gid=3113695) | Logos, imágenes de body |

Cada fila de la hoja es un asset: su nombre de taxonomía (`{NOMBREDETAXONOMIA}`) junto a su URL pública (`{urlpublica}`). Cuando un componente necesita una imagen, se busca por taxonomía en la hoja y se copia la URL — nunca se inventa ni se sube una URL nueva por fuera de este flujo.

El detalle completo de cómo se taxa cada tipo de asset vive en dos lugares:
- [PLAYBOOK_MAILS_2026 → Taxonomía + Librería](https://www.figma.com/design/RpZ1t207BNfDmlqi2DU1Ic/PLAYBOOK_MAILS_2026?node-id=59765-9535) — la fuente original del equipo de diseño, con la arquitectura completa de carpetas.
- [Doc-DS-Mails → 12 · Assets](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails?node-id=1097-2) — el mismo contenido reflejado con el diseño del sistema, con un mockup visual por cada variante y el segmento de la fórmula resaltado para que se entienda de un vistazo qué parte del nombre cambia. Esta sección del README es su versión en texto.

Lo que sigue está organizado en el mismo orden que esa página de Figma: fórmula universal primero, luego un bloque por cada tipo de asset.

## Fórmula del nombre

Todo asset se nombra con el mismo patrón de 7 campos, separados por `_`:

```
PAIS_MEDIA_VERTICAL_TIPO_ALIADO_DETALLE_CONTENEDOR
```

| Campo | Qué va | Ejemplo |
|---|---|---|
| **PAIS** | Sigla del país (`CO`, `MX`, `AR`...) o `LATAM` si el asset es compartido entre países | `MX` |
| **MEDIA** | Siempre `MAIL` en esta taxonomía | `MAIL` |
| **VERTICAL** | Categoría del app a la que pertenece el asset (`RESTAURANTES`, `FARMACIA`, `LICORES`, `TURBO`, `PRO`...) o `MULTI` si es transversal | `LICORES` |
| **TIPO** | Palabra clave que determina en qué carpeta de Drive vive — ver tabla de abajo | `LOGO`, `ICONOS_3D`, `BACKGROUND`... |
| **ALIADO** | Nombre de la marca/partner, o `GENERICO` si no aplica a una marca específica | `ELECTROLIT` |
| **DETALLE** | Descripción libre del contenido específico del asset | `HAMBURGUESA`, `PANTALLA_PAGAR_CON_CREDITOS_1` |
| **CONTENEDOR** | Variante de diseño/exportación (`SILUETEADO`, `FOTO`, `PASTILLA`, `OUTLINE`, `1:1`...) — **no** cambia la carpeta, sí las specs de exportación | `SILUETEADO` |

⚠️ **Reglas de naming universales** (todos los tipos de asset):
- MAYÚSCULAS en todo el nombre.
- Separar con guiones — nunca espacios.
- Sin caracteres especiales.
- Exportar a 1x del tamaño de ejemplo indicado por tipo.

## Tipos de asset, carpeta y variantes

Cada tipo de asset vive en su propia carpeta de Drive, identificada por la palabra clave que va en el campo **TIPO** del nombre. Cada bloque de abajo sigue el mismo orden que su card en Figma: carpeta + taxado base, cómo se completa cada campo, y sus variantes de `CONTENEDOR` con export recomendado.

### Logos (`LOGO`) — carpetas por país + genérica

📁 [Carpeta LOGOS](https://drive.google.com/drive/folders/1yHSawTq7f_3nM7oMt6p6mByd-749ynbG) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_ALIADO_LOGO_CONTENEDOR`

La palabra `LOGO` indica que va en la carpeta de logos. Carpetas por país (sigla) o una carpeta genérica si es igual para todo LATAM. `MEDIA` siempre se setea como `MAIL`. `VERTICAL` indica a qué categoría del app pertenece la marca. `ALIADO` contiene el nombre de la marca o producto.

| Variante | Termina en | Export recomendado |
|---|---|---|
| `CONTENEDOR` | `..._CONTENEDOR` | ancho auto × 135px, PNG con borde |
| `1:1` | `..._CONTENEDOR` | 320×320 — solo AR exporta el círculo real, el resto rellena el fondo |
| `PASTILLA` (horizontal M) | `..._PASTILLA` | 320px × alto auto, hasta 3:1 |
| `PASTILLA_L` (horizontal L) | `..._PASTILLA_L` | ancho auto × 135px, superior a 3:1 o cobranding |

### Íconos 3D (`ICONOS_3D`) — sin carpetas por país

📁 [Carpeta ICONOS_3D](https://drive.google.com/drive/folders/1v8c2uu2Z1EdAyVt6a-pnvyMvl0JQiPlw) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_ICONOS_3D_ALIADO_DETALLE_CONTENEDOR` · Biblioteca fuente: [miscellaneous-3D-s](https://www.figma.com/design/8KGCPt99rHzs2gWy9MxM6q/miscellaneous-3D-s?node-id=7858-1091)

Transversales a LATAM. `VERTICAL` = categoría del app relacionada. `ALIADO` suele ser `GENERICO`. `DETALLE` describe el contenido del ícono (`HAMBURGUESA`, `BOWL`, `RAYO`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `CON FONDO` / `FOTO` | `..._FOTO` | 320×320 — el contenedor en HTML tiene el borde redondeado |
| `SIN FONDO` / `SILUETEADO` | `..._SILUETEADO` | 320×320 — el contenedor en HTML tiene el borde redondeado |

### Íconos planos (`ICONOS_FLAT`) — sin carpetas por país

📁 [Carpeta ICONOS_FLAT](https://drive.google.com/drive/folders/16odmaQONgo-6tH6KZyDSyBi5Baao8IVp) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_ICONOS_FLAT_ALIADO_DETALLE_CONTENEDOR` · Biblioteca fuente: [icons](https://www.figma.com/design/kYsnknQmkgVfiawkU6baZb/icons?node-id=1-1065)

Transversales a LATAM, o `MULTI` si es general. `ALIADO` suele ser `GENERICO`. `DETALLE` describe el contenido (`HAMBURGUESA`, `BOWL`, `RAYO`) y agrega el color del ícono (`NEON`, `GRIS`, `DORADO`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `SIN FONDO` / `SILUETEADO` | `..._SILUETEADO` | 90×90 — sin redondeado en el HTML, si lo necesita debe venir en el export |
| `CON FONDO` / `PASTILLA` | `..._PASTILLA` | 90×90 — mismo caso, sin redondeado en el HTML |

### Fondos (`BACKGROUND`) — sin carpetas por país

📁 [Carpeta BACKGROUNDS](https://drive.google.com/drive/folders/1KqSJgWATKR1O-JRgW8aM0bSqghv0Lx4s) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_BACKGROUND_ALIADO_DETALLE_CONTENEDOR`

`VERTICAL` = evento relacionado con el fondo, o `MULTI`. `ALIADO` suele ser `GENERICO`, o el nombre del evento si el fondo es de uno específico. `DETALLE` describe el formato (`DESK`, `MOBILE`) y el diseño (`SOLIDO`, `GRADIENTE`, `ICONOS`, `TEXTURA`...).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `DESK` | `..._DESK_CONTENEDOR` | 1920px × alto auto — cuidar cómo se corta la parte inferior |
| `MOBILE` | `..._MOBILE_CONTENEDOR` | 700px × alto auto — cuidar cómo se corta la parte inferior |

### Pantallas (`PANTALLA`) — sin carpetas por país

📁 [Carpeta PANTALLAS](https://drive.google.com/drive/folders/12GLE3il4Yp_FFShO0gyQbCI5fgWz-fF6) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_PANTALLA_ALIADO_DETALLE_CONTENEDOR`

`ALIADO` suele ser `GENERICO`, salvo que la pantalla resalte una función/banner/logo de un aliado específico. `DETALLE` describe el contenido; si es paso a paso, se numera (`PANTALLA_PAGAR_CON_CREDITOS_1`, `_2`...). Se recomienda exportar sin mockups de celular.

| Variante | Termina en | Export recomendado |
|---|---|---|
| `CORTADA` / `SILUETEADO` | `..._SILUETEADO` | 800px × alto auto |
| `COMPLETA` / `FOTO` | `..._FOTO` | 800px × alto auto |

### Banners (`BANNER`) — sin carpetas por país (salvo contenido exclusivo de un país)

📁 [Carpeta banner](https://drive.google.com/drive/folders/19o_TeNoyZgCACzkli0pDg7UPlEXv2aTz) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_BANNER_ALIADO_DETALLE_CONTENEDOR`

`LATAM` si sirve para varios países; se usa el país específico si el contenido (producto/texto) solo aplica a uno. `ALIADO` suele ser `GENERICO`, salvo producto/beneficio exclusivo de un aliado.

| Variante | Termina en | Export recomendado |
|---|---|---|
| `SILUETEADO` | `..._SILUETEADO` | 1200px × alto auto |
| `FOTO` / completo | `..._FOTO` | 1200px × alto auto |

### Imágenes de body (`IMG_BODY`) — sin carpetas por país (salvo específico de país)

📁 [Carpeta IMG_BODY](https://drive.google.com/drive/folders/14_7XphJFrOg1vq3u-nW_PmmPRDWo8gKZ) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_IMG_BODY_ALIADO_DETALLE_CONTENEDOR`

La `VERTICAL` es la del **contenido** de la imagen, no la del mail donde se usa (una imagen de licores usada en un mail Turbo sigue siendo `LICORES`). `ALIADO`/`DETALLE` describen marcas, productos o contenido lifestyle (`MANOS_BOLSA_RAPPI`, `CAJA_REGALO`); si no hay aliado, se agrega el formato en `DETALLE` (`CUPON`, `BENEFICIO`...).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `MODULO CUPONES` | `..._CONTENEDOR` | 800×350, sin bordes redondeados |
| `MODULO BENEFICIOS` | `..._FOTO` | 1200×720, sin bordes redondeados — exportar siempre con fondo |
| `IMAGENES LIBRES PEQUEÑAS` | `..._CONTENEDOR` | 800px × alto auto |
| `IMAGENES LIBRES GRANDES` | `..._CONTENEDOR` | 1200px × alto auto |

> ⚠️ Estas 3 últimas variantes comparten el mismo sufijo genérico (`_CONTENEDOR`) en el Playbook original — a diferencia de los demás tipos, acá el sufijo no distingue una variante de otra por sí solo.

### Headers (`HEADER`) — sin carpetas por país (salvo header específico de país)

📁 [Carpeta HEADERS](https://drive.google.com/drive/folders/1jWeGW8AdTJTczi1qwQGfRyf3idYj0B9g) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_HEADER_ALIADO_DETALLE_CONTENEDOR`

Logos y elementos que componen los headers. `VERTICAL` indica a qué submarca pertenece el logo, o `MULTI` para las generales. `ALIADO` suele ser `GENERICO`, salvo header específico de un aliado (ej. `TURBO_MI_COMISARIATO`). `DETALLE` indica el texto si es tipográfico, y la variante de fondo/uso (`BLANCO`, `OSCURO`, `NEONYVERDE`, `FONDO_F9F9F9`, `BORDEBLANCO`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| Tamaño general | `..._SILUETEADO` | ancho auto × 150px, recomendado sin fondo |

### Cierres (`CIERRES`) — sin carpetas por país (salvo versión de país)

📁 [Carpeta CIERRES](https://drive.google.com/drive/folders/1n4KiJVyu-oDkqZnk5vWKm7nTX_ezvVXv) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_CIERRES_ALIADO_DETALLE_CONTENEDOR`

Se usa para la firma de los mails Genérico y Turbo. `VERTICAL` se usa para `MULTI` y `TURBO`. `ALIADO` suele ser `GENERICO` salvo cierre específico de un aliado. `DETALLE` indica el texto si es tipográfico, y el color (`NEON`, `BLANCO`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| Tamaño general | `..._SILUETEADO` | ancho auto × 150px, sin fondo |

> ⚠️ **Estos assets están establecidos, no se re-exportan** — a diferencia del resto de tipos de esta lista.

### Tags y sellos (`TAG` / `SELLOS`) — sin carpetas por país (salvo mensaje específico)

📁 [Carpeta TAGSYSELLOS](https://drive.google.com/drive/folders/14WtjCQ-XEZnsg7xTMBLFJ98t4GT45mzR) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_TAG_ALIADO_DETALLE_CONTENEDOR` / `PAIS_MEDIA_VERTICAL_SELLOS_ALIADO_DETALLE_CONTENEDOR`

Se usan para value props o eventos que pueden aplicar a varias verticales/países — aunque a veces se usen en headers, no van en esa carpeta. `VERTICAL` indica la categoría del value prop/evento (`FARMAWEEK`→farmacia, `PIZZAWEEK`→restaurantes, `PROWEEK`→pro), o `MULTI`. `ALIADO` suele ser `GENERICO`, o palabras como `EVENTO`/`TEXTO`/`BENEFICIO` para ser más puntuales. `DETALLE` indica el texto si es tipográfico y la variante de fondo (`FONDO_BLANCO`, `FONDO_NEON`, `GRIS`, `DORADO`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `TAG` / `PASTILLA` | `..._PASTILLA` | ancho auto × 125px, con borde redondeado — los tags suelen venir en formato pastilla |
| `SELLO` / `SILUETEADO` | `..._SILUETEADO` | 400px × alto auto, sin redondeado — cuidar legibilidad en dark mode |
| `SELLO` / `OUTLINE` | `..._OUTLINE` | 400px × alto auto, sin redondeado — el borde ayuda a la legibilidad en dark mode |

### Producto (`ASSET`) — carpetas por país + `LATAM` genérica

📁 [Carpeta DEAL_ASSETS](https://drive.google.com/drive/folders/1VbVi92pQcVsBOpUQfbWi2NTaajjrd8Ws) · 🧾 Taxado base: `PAIS_MEDIA_VERTICAL_ASSET_ALIADO_DETALLE_CONTENEDOR`

Carpeta por país, o `LATAM` si el producto no es exclusivo de un país (frutas, licores multi-país, productos sin etiqueta). La `VERTICAL` es la del producto en el app — **no** la del mail donde se usa; `MULTI` si aplica a varias. `ALIADO` = `GENERICO` si no tiene marca o es bodegón mixto, o la marca (`ELECTROLIT`, `MODELO`, `LG`) si la tiene o es exclusivo de una tienda. `DETALLE` nombra el producto (`VINO_FLORES_CHOCOLATES_CAJA`, `MC_FLURRY`) y sus especificaciones (`2_HAMBURGUESAS`, `SIX_PACK`).

| Variante | Termina en | Export recomendado |
|---|---|---|
| `SIN FONDO` / `SILUETEADO` | `..._SILUETEADO` | 650×500 fijo — productos grandes, con sangrados |
| `CON FONDO` / `FOTO` | `..._FOTO` | 650×500 fijo — con el fondo real del producto, nunca fondos de evento ni colores neón/pastel |

Ambas variantes tienen además un área de respeto desk/mobile que varía por pantalla.

## Estructura de este repo

Este repo **no almacena imágenes**. Las carpetas `images/` y `logos/` que documentaban versiones anteriores de este README nunca se poblaron — Drive + la taxonomía de arriba son la fuente real. Lo único que vive acá son las referencias por URL dentro de cada componente HTML.

## Reglas

- Las URLs de imágenes están en los componentes como `src="https://..."`.
- Cuando se cree un mail, el creador NO sube imágenes nuevas ni las exporta a mano. Las solicita al equipo de diseño, que las taxa y publica en la hoja de TAXONOMÍA ASSETS siguiendo la fórmula de arriba.
- Si una URL no existe en la taxonomía, el mail no se entrega hasta que la imagen esté disponible.
- El campo CONTENEDOR (la variante de diseño) no determina la carpeta de Drive — solo afecta las specs de exportación. No confundir "está en la carpeta correcta" con "tiene la variante correcta".
