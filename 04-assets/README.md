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

El detalle completo de cómo se taxa cada tipo de asset (fórmula, carpeta de Drive, variantes, tamaños de exportación) vive en el Playbook de Figma: [PLAYBOOK_MAILS_2026 → Taxonomía + Librería](https://www.figma.com/design/RpZ1t207BNfDmlqi2DU1Ic/PLAYBOOK_MAILS_2026?node-id=59765-9535). Lo que sigue es un resumen operativo de esa página.

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

Cada tipo de asset vive en su propia carpeta de Drive, identificada por la palabra clave que va en el campo **TIPO** del nombre. La mayoría son transversales a LATAM (sin subcarpetas por país); Logos y Producto sí tienen carpeta por país + una carpeta genérica.

| Tipo (palabra clave) | Carpeta Drive | ¿Carpetas por país? | Variantes (CONTENEDOR) y export recomendado |
|---|---|---|---|
| **Logos** (`LOGO`) | [LOGOS](https://drive.google.com/drive/folders/1yHSawTq7f_3nM7oMt6p6mByd-749ynbG) | Sí, + carpeta genérica | `CONTENEDOR` (ancho auto×135px, PNG con borde) · `1:1` (320×320 — solo AR exporta el círculo real, el resto rellena el fondo) · `PASTILLA`/horizontal M (320px×alto auto, hasta 3:1) · `PASTILLA_L`/horizontal L (ancho auto×135px, superior a 3:1 o cobranding) |
| **Íconos 3D** (`ICONOS_3D`) | [ICONOS_3D](https://drive.google.com/drive/folders/1v8c2uu2Z1EdAyVt6a-pnvyMvl0JQiPlw) | No | `CON FONDO`/`FOTO` (320×320) · `SIN FONDO`/`SILUETEADO` (320×320) — biblioteca fuente: [miscellaneous-3D-s](https://www.figma.com/design/8KGCPt99rHzs2gWy9MxM6q/miscellaneous-3D-s?node-id=7858-1091) |
| **Íconos planos** (`ICONOS_FLAT`) | [ICONOS_FLAT](https://drive.google.com/drive/folders/16odmaQONgo-6tH6KZyDSyBi5Baao8IVp) | No | `SIN FONDO`/`SILUETEADO` (90×90, sin redondeado — si lo necesita debe venir en el export) · `CON FONDO`/`PASTILLA` (90×90). El DETALLE incluye color (`NEON`, `GRIS`, `DORADO`) — biblioteca fuente: [icons](https://www.figma.com/design/kYsnknQmkgVfiawkU6baZb/icons?node-id=1-1065) |
| **Fondos** (`BACKGROUND`) | [BACKGROUNDS](https://drive.google.com/drive/folders/1KqSJgWATKR1O-JRgW8aM0bSqghv0Lx4s) | No | `DESK` (1920px×alto auto) · `MOBILE` (700px×alto auto). Cuidar cómo se corta la parte inferior en ambos |
| **Pantallas** (`PANTALLA`) | [PANTALLAS](https://drive.google.com/drive/folders/12GLE3il4Yp_FFShO0gyQbCI5fgWz-fF6) | No | `CORTADA`/`SILUETEADO` (800px×alto auto) · `COMPLETA`/`FOTO` (800px×alto auto). Sin mockups de celular. Si es paso a paso, se numera en el DETALLE (`_1`, `_2`...) |
| **Banners** (`BANNER`) | [banner](https://drive.google.com/drive/folders/19o_TeNoyZgCACzkli0pDg7UPlEXv2aTz) | No (salvo contenido exclusivo de un país) | `SILUETEADO` (1200px×alto auto) · `FOTO`/completo (1200px×alto auto) |
| **Imágenes de body** (`IMG_BODY`) | [IMG_BODY](https://drive.google.com/drive/folders/14_7XphJFrOg1vq3u-nW_PmmPRDWo8gKZ) | No (salvo específico de país) | `MODULO CUPONES` (800×350) · `MODULO BENEFICIOS` (1200×720, siempre con fondo) · `IMAGENES LIBRES PEQUEÑAS` (800px×alto auto) · `IMAGENES LIBRES GRANDES` (1200px×alto auto). La VERTICAL es la del contenido de la imagen, no la del mail donde se usa (una imagen de licores usada en un mail Turbo sigue siendo `LICORES`) |
| **Headers** (`HEADER`) | [HEADERS](https://drive.google.com/drive/folders/1jWeGW8AdTJTczi1qwQGfRyf3idYj0B9g) | No (salvo header específico de país) | Tamaño general: ancho auto×150px, recomendado sin fondo (`SILUETEADO`). El DETALLE indica texto (si es tipográfico) y variante de fondo/uso (`BLANCO`, `OSCURO`, `NEONYVERDE`, `FONDO_F9F9F9`, `BORDEBLANCO`) |
| **Cierres** (`CIERRES`) | [CIERRES](https://drive.google.com/drive/folders/1n4KiJVyu-oDkqZnk5vWKm7nTX_ezvVXv) | No (salvo versión de país) | Tamaño general: ancho auto×150px, sin fondo. Uso: firma de mails Genérico y Turbo. ⚠️ **Están establecidos, no se re-exportan** — a diferencia del resto de tipos |
| **Tags y sellos** (`TAG` / `SELLOS`) | [TAGSYSELLOS](https://drive.google.com/drive/folders/14WtjCQ-XEZnsg7xTMBLFJ98t4GT45mzR) | No (salvo mensaje de país) | `TAG`/`PASTILLA` (ancho auto×125px, borde redondeado) · `SELLO`/`SILUETEADO` (400px×alto auto, cuidar legibilidad en dark mode) · `SELLO`/`OUTLINE` (400px×alto auto, el borde ayuda a la legibilidad en dark mode). VERTICAL = categoría del value prop/evento (`FARMAWEEK`→farmacia, `PIZZAWEEK`→restaurantes, `PROWEEK`→pro) |
| **Producto** (`ASSET`) | [DEAL_ASSETS](https://drive.google.com/drive/folders/1VbVi92pQcVsBOpUQfbWi2NTaajjrd8Ws) | Sí, + carpeta `LATAM` genérica | `SIN FONDO`/`SILUETEADO` (650×500 fijo, sangrados) · `CON FONDO`/`FOTO` (650×500 fijo, con el fondo real del producto — nunca fondos de evento ni colores neón/pastel). La VERTICAL es la del producto en el app, no la del mail. ALIADO = marca si la tiene, `GENERICO` si es bodegón mixto o sin marca |

## Estructura de este repo

Este repo **no almacena imágenes**. Las carpetas `images/` y `logos/` que documentaban versiones anteriores de este README nunca se poblaron — Drive + la taxonomía de arriba son la fuente real. Lo único que vive acá son las referencias por URL dentro de cada componente HTML.

## Reglas

- Las URLs de imágenes están en los componentes como `src="https://..."`.
- Cuando se cree un mail, el creador NO sube imágenes nuevas ni las exporta a mano. Las solicita al equipo de diseño, que las taxa y publica en la hoja de TAXONOMÍA ASSETS siguiendo la fórmula de arriba.
- Si una URL no existe en la taxonomía, el mail no se entrega hasta que la imagen esté disponible.
- El campo CONTENEDOR (la variante de diseño) no determina la carpeta de Drive — solo afecta las specs de exportación. No confundir "está en la carpeta correcta" con "tiene la variante correcta".
