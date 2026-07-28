# J.A.R.V.I.S. Mail System

Sistema de diseño para mails de Rappi. Convierte piezas sueltas de Figma en bloques organizados, reutilizables y listos para Braze.

> Esto no es un repositorio de código. Es una caja de bricks de LEGO.
> Cada archivo es una pieza. Cada pieza tiene una función clara. Combinándolas se arman los mails.

## Manual J.A.R.V.I.S
https://powerful-author-808.notion.site/J-A-R-V-I-S-Mail-System-35dc6cf39c6a81c88e23d1463640ab71

## La metáfora

Si abres una caja de LEGO encuentras tres cosas: las **piezas** (los bricks), las **reglas** de cómo encajan, y las **instrucciones** para armar modelos terminados. Este repositorio funciona igual.

| LEGO | J.A.R.V.I.S. |
|------|--------------|
| Las reglas de color y forma | `01-foundations/` |
| El tablero base | `02-base-template/` |
| Los bricks individuales | `03-components/` |
| Las skins (los 11 temas: Beige, Rosa, Púrpura, Celeste, Verde, Dark neon/Turbo/Neutro, Pro, ProBlack) | Liquid en `01-foundations/global-styles/head-meta-tags.html` |
| Los modelos ya armados | `04-templates/` |

## Cómo se arma un mail

Un mail siempre se arma en este orden, pieza por pieza:

```
opening.html  (esqueleto inicial + apertura del banner)
   ↓
header        (un solo header de los 10 disponibles, en su variante claro/oscuro y centrado/columnas)
   ↓
banner        (horizontal, vertical o editorial)
   ↓
body-wrapper-open.html  (abre la zona de contenido)
   ↓
[CTAs, deals, cupones, beneficios, módulos de contenido]   ← bricks combinables
   ↓
cierre        (imagen de cierre — omitido en los temas Pro/ProBlack)
   ↓
body-wrapper-close.html
   ↓
footer
   ↓
closing.html
```

Los corchetes `[ ]` son la zona donde el creador del mail decide qué piezas pone y en qué orden. Todo lo demás es estructura fija.

## Estructura de carpetas

```
jarvis-mail-system/
│
├── 01-foundations/            Las reglas
│   ├── global-styles/         CSS global, media queries, meta tags
│   └── tokens/                Colores, espaciados, radios (a futuro)
│
├── 02-base-template/          El esqueleto
│   ├── opening.html           Doctype + head + apertura del wrapper
│   ├── body-wrapper-open.html Apertura de la zona de contenido
│   ├── body-wrapper-close.html Cierre de la zona de contenido
│   └── closing.html           Cierres finales del HTML
│
├── 03-components/             Los bricks (21 piezas en total)
│   ├── headers/               10 headers de marca, cada uno en claro/oscuro × centrado/columnas
│   ├── banners/               3 banners (horizontal, vertical, editorial)
│   ├── ctas/                  Plantilla del botón de acción
│   ├── deals/                 Deal grande y small
│   ├── coupons/               Módulo de cupones (con title + cupón)  ◀ NUEVO
│   ├── benefits/              Módulo de beneficios                    ◀ NUEVO
│   ├── content-modules/       Título, columnas, logos, contenido
│   ├── closing/               Imagen de cierre
│   └── footer/                Footer general
│
├── 04-templates/              Los modelos armados
│   ├── full-templates/        Combinaciones completas listas para usar
│   └── by-vertical/           Templates por vertical de negocio
│
├── 05-assets/                 Imágenes y logos
│
├── 06-docs/                   Documentación del sistema
│
└── 07-examples/               Ejemplos reales de mails ya construidos
```

## Reglas de oro

1. **Cero Inserción Autónoma.** Nadie inventa módulos nuevos. Si no existe en este repo, no existe.
2. **Los componentes no se modifican.** Se usan tal cual están. Lo que cambia entre un mail y otro son las imágenes, textos y los componentes que se incluyen u omiten.
3. **Los comentarios `INICIO` / `FIN` y las instrucciones internas se conservan SIEMPRE.** Son parte del componente. No son adornos.
4. **El tema se resuelve por Liquid, no se mezcla a mano.** Los 11 temas viven como variables `{% assign %}` en `01-foundations/global-styles/head-meta-tags.html`, condicionadas por `tema_general_mail_general`; los componentes no se modifican para cambiar de tema.

## Documentación clave

Antes de producir tu primer mail, lee estos dos documentos en orden:

1. **[Guía completa de Temas](06-docs/GUIA-DE-TEMAS.md)** — Los 11 temas del sistema, qué variables Liquid define cada uno, y las reglas particulares por grupo (pastel, oscuros/invertidos, premium).
2. **[Uso correcto de cada parte](06-docs/USO-DE-CADA-PARTE.md)** — Guía brick por brick: cuándo usar cada componente, sus reglas internas, las piezas opcionales, y el orden recomendado de ensamblaje.

Documentación complementaria en `06-docs/`:
- `COMO-ARMAR-UN-MAIL.md` — Flujo paso a paso para armar un mail desde cero
- `INDICE-DE-COMPONENTES.md` — Mapa con cada componente y su ubicación en el HTML original
- `CONTRIBUTING.md` — Cómo proponer cambios al sistema
- `CHANGELOG.md` — Historial de versiones

## Para el equipo de mails

- Este repo es la fuente única de verdad. Si algo no está aquí, no existe.
- El Gem de Gemini sigue funcionando para producción diaria; este repo es la base de la que se alimenta.
- Cuando se agregue un nuevo brick (un nuevo header, un nuevo módulo), se hace acá primero y luego se actualiza Gemini.

## Para equipos técnicos

- Cada componente es HTML válido, listo para inyectar en Braze.
- Las variables Liquid (`{% assign %}`, `{{content_blocks.${...}}}`) están preservadas tal cual.
- El sistema está pensado para que cualquier persona pueda producir mails leyendo solo este repo.

---

Sistema de diseño Rappi · Paleta Neon (FF7A4D · FF2526 · FF4583 · EB5583)
