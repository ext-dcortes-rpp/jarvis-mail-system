# J.A.R.V.I.S. — Design System de mails Rappi

Sistema de diseño operativo para producción de emails en Braze. Convierte fuentes editoriales en HTML consistente y modular, anclado a un design system documentado en Figma y versionado en este repo.

**Figma (fuente única de verdad):** [Doc-DS-Mails](https://www.figma.com/design/7Rtnl6O6XVdhKjm3Kf8cxo/Doc-DS-Mails)

**Versión actual:** v1.1

---

## Qué es este repo

Este repo contiene los **archivos HTML de los componentes del sistema** más su documentación. No es el template maestro — el template maestro (con todos los componentes ensamblados) vive en producción de Braze. Acá están las piezas individuales y sus reglas.

### Estructura

```
vision-mail-system/
├── README.md                         ← este archivo
├── 01-foundations/                   Reglas de color y forma
├── 02-base-template/                 El esqueleto base
├── 03-components/                    Los bricks individuales
│   ├── ctas/
│   │   ├── cta-template.html
│   │   └── README.md                 ← anatomía + variables + reglas del CTA
│   ├── deals/
│   │   ├── deal-large.html
│   │   ├── deal-small.html
│   │   ├── README-big-deal.md        ← Big Deal
│   │   └── README-small-deal.md      ← Small Deal
│   └── footer/
│       ├── footer.html
│       └── README.md                 ← Footer
├── 04-variants/                      Skins por KV
├── 05-templates/                     Modelos armados
├── 06-assets/                        Imágenes y logos
├── 07-docs/                          Documentación del sistema
└── 08-examples/                      Ejemplos reales
```

---

## El contrato del sistema

J.A.R.V.I.S. tiene **dos capas de variables** que NO mapean 1:1 y es crítico entender esto antes de tocar un componente.

### Capa 1 — KV editorial (lo que dice la fuente)

El editor escribe en la fuente "Tipo de KV: X". Los 6 valores posibles:

| KV | Familia | Cuándo se usa |
|---|---|---|
| **Genérico** | Standard | Default editorial, mails sin tema específico |
| **Turbo** | Standard | Mails con foco en RappiTurbo (groceries, conveniencia) |
| **Neutro** | Standard | Mails sobrios, sin highlight de marca |
| **Pro** | Premium | Mails de la membresía Rappi Pro (luminoso, dorado) |
| **ProBlack** | Premium | Mails de la membresía Rappi Pro (oscuro, dorado) |
| **Cafe** | Editorial cálido | KV experimental para mails con paleta cálida (agregado en v1.1) |

### Capa 2 — Valores Liquid (lo que dispara cada KV en cada componente)

Cada KV dispara 3 variables Liquid distintas:

| KV | `style_Look` (CTA) | `deal_style_look` (Deals) | `font_style_look` (Footer) |
|---|---|---|---|
| Genérico | `neon` | `generico` | `negro` |
| Turbo | `neon` | `neon` | `negro` |
| Neutro | `negro` | `generico` | `negro` |
| Pro | `pro` | `pro` | `pro` |
| ProBlack | `problack` | `problack` | `pro` |
| Cafe | `blanco` (fallback) | `generico` (fallback) | `cafe` |

**Por qué la separación importa:** si vas a agregar un componente nuevo, tenés que decidir explícitamente qué valor Liquid recibe en cada uno de los 6 KVs. Si vas a agregar un KV nuevo, tenés que asignarle sus 3 valores Liquid existentes. Es contrato, no convención.

📐 **Referencia visual:** Figma → página `03 · KVs` (sección de mapeo) y `08 · HTML Bridge`.

---

## Tokens semánticos

El sistema usa 9 tokens semánticos para color, 7 para border-radius, y 2 para tipografía/spacing. Toda la lista vive en Figma → `02 · Tokens`.

### Colores principales (mail/*) por KV

| Token | Genérico | Turbo | Neutro | Pro | ProBlack | Cafe |
|---|---|---|---|---|---|---|
| `mail/bg-body` | `#040404` | `#040404` | `#040404` | `#2A2B2B` | `#ECEFF3` | `#FFFFFF` |
| `mail/bg-module` | `#202020` | `#202020` | `#202020` | `#1D1D1D` | `#040404` | `#F4ECDA` |
| `mail/text-body` | `#E2E2E2` | `#E2E2E2` | `#E2E2E2` | `#E2E2E2` | `#FFFFFF` | `#633D11` |
| `mail/text-banner` | `#FFFFFF` | `#FFFFFF` | `#FFFFFF` | `#FBFBFB` | `#040404` | `#633D11` |
| `mail/text-accent` | `#FFEBC2` | `#F2ED93` | `#FFEBC2` | `#D6AB76` | `#D6AB76` | `#A66D2F` |
| `mail/cta-bg` | `#FFFFFF` | `#FFFFFF` | `#000000` | `#FFFFFF` | `#000000` | `#FFFFFF` |
| `mail/cta-text` | `#000000` | `#000000` | `#FFFFFF` | `#000000` | `#FFFFFF` | `#000000` |
| `mail/cta-bg-neon` | `#E34145` | `#E34145` | `#E34145` | `#E34145` | `#E34145` | `#E34145` |
| `mail/border-pro` | `#DAA868` | `#DAA868` | `#DAA868` | `#DAA868` | `#DAA868` | `#DAA868` |

### Banner backgrounds — caso especial

El banner es el único organismo que **no usa** `mail/bg-module`. Tiene su propio gradiente lineal por KV:

| KV | Gradiente del banner |
|---|---|
| Genérico | `#FE3F23 → #FF7A4D` (naranja Rappi) |
| Turbo | `#003A34 → #005F50` (verde Turbo) |
| Neutro | `#0A0A0A → #2A2A2A` (negro) |
| Pro | `#2A2B2B → #3A3B3B` (gris oscuro premium) |
| ProBlack | `#E4E8EE → #D0D5DC` (gris perla premium) |
| Cafe | `#F4ECDA → #E8DBB8` (beige cálido) |

### Border-radius (escala semántica)

```css
:root {
  --mail-radius-chip:       3px;   /* tag inline casi cuadrado */
  --mail-radius-inner-s:    6px;   /* chip pequeño interno */
  --mail-radius-inner-m:    8px;   /* subdivisión dentro de módulo */
  --mail-radius-module-m:  12px;   /* contenedor de organismo estándar */
  --mail-radius-module-l:  16px;   /* contenedor "hero" (banner, Big Deal) */
  --mail-radius-pill-cta:  50px;   /* CTA interno (deal) */
  --mail-radius-pill:      55px;   /* CTA principal del mail */
}
```

**Regla de oro:** las imágenes NUNCA llevan border-radius propio. El redondeo viene del contenedor con `overflow: hidden` (Outlook ignora `border-radius` en `<img>`).

📐 **Referencia visual:** Figma → `02 · Tokens` (secciones 2.5 Banner backgrounds y 2.6 Tokens de radio).

---

## Reglas globales del sistema

### Estructura del HTML (intocable)
- NO agregar etiquetas HTML, meta tags, estilos globales o contenedores que no existan en la plantilla base
- NO optimizar/embellecer: mantener espacios, tabs, saltos de línea, comentarios y condicionales Outlook tal cual
- El `<script type="application/ld+json">` después del `</html>` nunca se mueve ni se borra
- La sección `<!-- inicio head -->` hasta `<!-- fin head -->` se mantiene exactamente igual

### Separadores entre módulos
- Entre dos `role="module"` consecutivos: SIEMPRE `<div class="separador"></div>` (16px)
- Excepción: entre un módulo y un deal contiguo no se inserta separador
- Entre dos `role="componente"` del mismo módulo: `<div class="separador-M"></div>` (10px)

### Banner y deals
- Big Banner Deal Destacado: siempre horizontal
- Big Banner con Logos: siempre vertical
- Máximo 4 deals por mail
- Máximo 2 jerarquías de texto en el banner (h1+h4, h2+h4 o h3+h4)

### Pro y ProBlack
- **Eliminar la tabla de cierre por completo** (no `display:none`, borrar del HTML)
- Footer siempre con `font_style_look = 'pro'` (activa `show_hr` y bloque membresía)

### Mantenimiento del sistema
- **Auditar tokens contra HTML real antes de publicar versión nueva.** No inferir valores por lógica editorial — leer los archivos.
- HTML maestro = fuente única. Si Figma y HTML difieren, gana HTML; se corrige Figma.
- Cada cambio mayor abre entrada en Changelog (Figma → `10 · Changelog`).
- Mapeo KV → Liquid es contrato: KV nuevo necesita los 3 valores Liquid asignados.
- Cafe es excepción documentada, no patrón a replicar para futuros KVs.

📐 **Referencia visual:** Figma → `09 · Reglas globales`.

---

## Responsive

Dos breakpoints, contenido casi idéntico (por compatibilidad con distintos clientes de email):

```css
@media (max-width: 480px) { /* mobile devices: iPhone, Android, Gmail app, Apple Mail mobile */ }
@media (max-width: 620px) { /* clientes desktop estrechos: Outlook con panel de lectura, Yahoo Mail web */ }
```

### Clases utility de visibilidad
- `.mobile_hide` → se ve en desktop, se oculta en mobile
- `.desktop_hide` → se ve en mobile, se oculta en desktop
- `.alto-auto` → override `height: auto !important` (cancela altura fija desktop)
- `.altobanner1` → override `height: 85vw !important` (banner proporcional al viewport)

**Regla crítica del Módulo Dos Columnas:** se DUPLICA la tabla — una versión con `class="mobile_hide"` (horizontal desktop) y otra con `class="desktop_hide"` (vertical mobile). Contenido idéntico. Si hay N módulos en la fuente, hay 2N en el HTML.

### Overrides de tipografía en mobile

| Tag | Desktop | Mobile |
|---|---|---|
| h1 | 50/50 | 48/49 |
| h2 | 35/37 | 35/37 (sin cambio) |
| h3 | 27/28 | 27/28 (sin cambio) |
| h4 | 17/19 | 16/18 |
| h5 | 16/17 | 15/16 |
| h6 | 14/15 | 13/14 |
| .txts | 13/14 | 11/12 |
| .txtl | 25/26 | 20/21 |

📐 **Referencia visual:** Figma → `11 · Responsive`.

---

## Cómo trabajar con este repo

### Para producir un mail nuevo (operación diaria)
1. Identificar el KV editorial en la fuente (Genérico, Turbo, Neutro, Pro, ProBlack, Cafe)
2. Convertir el KV en los 3 valores Liquid usando la tabla del contrato
3. Para cada componente del mail, abrir su `README.md` y verificar variables/reglas
4. Ensamblar el HTML respetando las reglas globales (separadores, eliminación de cierre Pro, etc.)
5. Validar con el checklist mobile antes de entregar

### Para agregar un componente nuevo (mantenimiento)
1. Crear `03-components/[nombre]/` con su HTML
2. Crear `03-components/[nombre]/README.md` siguiendo el formato de los existentes
3. Asignar valores Liquid para cada uno de los 6 KVs
4. Documentar en Figma (organismo nuevo en `06 · Organisms` + entrada en HTML Bridge)
5. Abrir entrada en Changelog
6. Auditar contra los demás componentes para evitar duplicación

### Para modificar un componente existente
1. Editar el HTML respetando la cabecera Liquid
2. Actualizar el `README.md` del componente
3. Si cambian tokens/variables, actualizar Figma (`02 · Tokens`, `03 · KVs`, `08 · HTML Bridge`)
4. Entrada en Changelog con tipo MODIFICADO y descripción específica

---

## Componentes

| Componente | Tipo | Archivo | README |
|---|---|---|---|
| CTA | Atom | [`cta-template.html`](03-components/ctas/cta-template.html) | [03-components/ctas/README.md](03-components/ctas/README.md) |
| Big Deal | Organism | [`deal-large.html`](03-components/deals/deal-large.html) | [03-components/deals/README-big-deal.md](03-components/deals/README-big-deal.md) |
| Small Deal | Organism | [`deal-small.html`](03-components/deals/deal-small.html) | [03-components/deals/README-small-deal.md](03-components/deals/README-small-deal.md) |
| Footer | Organism | [`footer.html`](03-components/footer/footer.html) | [03-components/footer/README.md](03-components/footer/README.md) |

Los demás organismos (Header, Big Banner, Módulos de contenido, Cierre) viven en el template maestro de Braze y están documentados completamente en Figma → `06 · Organisms`.

---

## Stack

- **HTML + Liquid** — para producción en Braze
- **Tablas + inline styles** — compatibilidad email-client universal
- **Figma** — fuente única de verdad para diseño, tokens y reglas
- **Gemini Gem** — generación diaria de mails a partir de la fuente editorial
- **Claude / Claude Code** — mantenimiento del sistema (componentes, docs, repo)
