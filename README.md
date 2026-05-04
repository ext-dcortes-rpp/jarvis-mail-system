# Vision Mail System

Sistema para armar mails de Rappi. Convierte piezas sueltas de Figma en bloques organizados, reutilizables y listos para enviar por Braze.

> Esto no es una colección de código complicado. Es una caja de bricks de LEGO.
> Cada archivo es una pieza. Cada pieza tiene una función clara. Combinándolas se arman los mails.

**No necesitas saber programación para usar este sistema.** Solo necesitas saber copiar, pegar y reemplazar textos e imágenes.

## La metáfora

Si abres una caja de LEGO encuentras tres cosas: las **reglas** de qué formas y colores existen, el **tablero base** donde construyes encima, y los **bricks** que combinas libremente. Este repositorio funciona igual.

| LEGO | Vision | Qué contiene |
|------|--------|--------------|
| Las reglas de color y forma | `01-foundations/` | Los colores y tamaños de letra del sistema |
| El tablero base | `02-base-template/` | La estructura fija del mail (no se toca) |
| Los bricks individuales | `03-components/` | Los bloques visuales: headers, banners, CTAs, deals... |
| Las skins (el "look") | `04-variants/` | Los estilos visuales: Pro, Turbo, Neutro... |
| Los modelos ya armados | `05-templates/` | Mails completos listos para personalizar |

## Cómo se arma un mail

Un mail siempre se arma en este orden, pieza por pieza:

```
opening.html  → El comienzo obligatorio del mail
   ↓
header        → La identidad de la marca (elige 1 de 6)
   ↓
banner        → La imagen principal del mail (elige 1 de 3 formatos)
   ↓
body-wrapper-open.html  → Abre la zona de contenido
   ↓
[ CTAs · deals · módulos ]  ← acá decides qué piezas pones y en qué orden
   ↓
cierre        → Imagen de cierre (opcional)
   ↓
footer        → Pie de mail (siempre va)
   ↓
closing.html  → El cierre obligatorio del mail
```

Lo que está entre corchetes `[ ]` es tu zona de decisión. Todo lo demás es estructura fija que no se modifica.

## Estructura de carpetas

```
vision-mail-system/
│
├── 01-foundations/            Las reglas de diseño del sistema
│
├── 02-base-template/          El esqueleto del mail (no se toca)
│   ├── opening.html           Inicio del mail
│   ├── body-wrapper-open.html Abre la zona de contenido
│   ├── body-wrapper-close.html Cierra la zona de contenido
│   └── closing.html           Fin del mail
│
├── 03-components/             Los bricks — aquí pasa la mayoría de las cosas
│   ├── headers/               6 headers (uno por marca: Rappi, Travel, Turbo...)
│   ├── banners/               3 banners (horizontal, vertical, editorial)
│   ├── ctas/                  El botón de acción
│   ├── deals/                 Bloques de promociones (grande y small)
│   ├── content-modules/       Bloques de contenido (título, columnas, logos...)
│   ├── closing/               Imagen de cierre
│   └── footer/                Pie de mail
│
├── 04-variants/               Los estilos visuales por tipo de mail
│
├── 05-templates/              Mails completos listos para usar
│
├── 06-assets/                 Imágenes y logos del sistema
│
├── 07-docs/                   Guías y documentación
│
└── 08-examples/               Ejemplos de mails reales ya construidos
```

## Reglas de oro

1. **No se inventan piezas nuevas.** Si un bloque que necesitas no existe en este sistema, se solicita al equipo — no se crea sobre la marcha.
2. **Las piezas no se modifican internamente.** Lo que cambia de un mail a otro son las imágenes, los textos y qué piezas se incluyen. La estructura de cada pieza es fija.
3. **Los comentarios de INICIO y FIN dentro de cada archivo se conservan siempre.** Son parte de la pieza, no son decoración.
4. **Los estilos visuales se aplican encima, no se mezclan con las piezas.** Un mail Pro usa el estilo Pro; no se modifican los componentes para que "parezcan Pro".

## Para el equipo de mails

- Este repositorio es la fuente única de verdad. Si algo no está aquí, no existe.
- El Gem de Gemini sigue funcionando para producción diaria; este sistema es la base de la que se alimenta.
- Cuando se agregue un nuevo bloque (un nuevo header, un nuevo módulo), se registra acá primero y luego se actualiza Gemini.

---

Sistema de diseño Rappi · Colores Neon: naranja · rojo · rosa · fucsia
