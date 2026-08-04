# Átomos, Moléculas y Organismos

Este documento define cómo J.A.R.V.I.S. usa las tres primeras escalas de Atomic Design (Átomos → Moléculas → Organismos) para clasificar cada pieza del sistema. Es el equivalente en repo a las páginas `04 · Atoms`, `05 · Molecules` y `06 · Organisms` del Figma del sistema de diseño (`Doc-DS-Mails`) — ambos deben decir lo mismo.

> **Estado:** este doc define las reglas. La clasificación pieza por pieza (qué carpeta/archivo es átomo, cuál es molécula, cuál es organismo) todavía no está hecha — se va a ir completando a medida que se confirme cada caso. Hasta que eso pase, la estructura de carpetas numeradas de `02-components/` (`01_headers` → `06_footer`) sigue siendo la referencia operativa para producir mails.

---

## Átomos

**Elementos sueltos.** La pieza visual mínima: no tiene contenedor propio ni contexto — es un texto, una imagen, un ícono, un tag, un separador, un CTA. Por sí solo no impone reglas de tamaño o posición; esas reglas las adquiere cuando se combina dentro de una molécula.

## Moléculas

Hay dos formas de ser molécula:

1. **Átomos dentro de un contenedor**, donde el contenedor le impone sus propias reglas al mismo átomo según dónde vive:
   - Un logo tiene reglas de tamaño/posición/redondeado distintas si está en el banner o en un deal.
   - Un frame de texto tiene reglas distintas si está en un banner horizontal o en uno vertical.
   - Un frame de texto tiene reglas distintas si está en un banner o en un deal.
2. **Átomos unidos que forman un elemento simple con sus propias reglas** — ej: bullets, tags, módulos de promo, módulos de tags.

Una molécula todavía no tiene contexto de página completa — eso es lo que la distingue del organismo.

## Organismos

**La pieza de LEGO con estructura fija**, compuesta de varias moléculas combinadas — ej: banners, deals, módulos en columnas, cupones. Cada organismo es autocontenido: tiene su propio padding, su propia lógica, y vive como bloque completo (`table role="module"`) dentro del HTML.

---

## Clasificación pieza por pieza

Pendiente — se completa a medida que se confirme cada pieza existente de `02-components/`.

| Pieza actual | Carpeta hoy | Clasificación |
|---|---|---|
| `molecula_tag_promo.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_tag_verde.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_tag_basico.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_separador_s.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_icono.html` | `04_content-modules/content_moleculas/` | Molécula (agrupa 4 tamaños: S/M/L/XL) |
| `molecula_tag_icono.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_franja_logos.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_img_automatica.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_texto_pastilla.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_link_interno.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_bullet_numerado.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_bullet_icono_s.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_bullet_icono_m.html` | `04_content-modules/content_moleculas/` | Molécula |
| `molecula_bullet_icono_l.html` | `04_content-modules/content_moleculas/` | Molécula |
| `modificadores-texto.html` | `04_content-modules/content_moleculas/` | Sin clasificar — es una referencia de variantes de texto (tamaño/bold/italic/etc.), no combina átomos en un elemento nuevo |
| _resto por definir_ | | |

## Referencias cruzadas

- Figma — `Doc-DS-Mails`: página `04 · Atoms`, página `05 · Molecules`, página `06 · Organisms`.
- Inventario de archivos actual: `05-docs/INDICE-DE-COMPONENTES.md`.
- Guía operativa (mientras no exista la reclasificación): `05-docs/USO-DE-CADA-PARTE.md`.
