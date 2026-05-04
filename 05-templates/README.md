# 05 · Templates

> Los modelos terminados. Combinaciones ya armadas listas para usar.

Mientras los `components/` son las piezas individuales, los `templates/` son combinaciones completas que cubren los casos de uso más frecuentes. En lugar de armar un mail desde cero combinando 8 o 10 piezas, usas un template que ya tiene la estructura lista y solo cambias textos e imágenes.

## Subcarpetas

### `full-templates/`
Plantillas completas y genéricas, identificadas por su composición:

- `solo-banner.html` — Mail mínimo: solo header + banner + footer
- `banner-cta.html` — Header + banner + botón de acción + cierre + footer
- `banner-cta-deals.html` — Mail con deals de productos
- `completo.html` — Plantilla con todos los módulos posibles (sirve como referencia visual)

### `by-vertical/`
Plantillas específicas por vertical de negocio. Útiles cuando un equipo produce muchos mails con la misma estructura:

- `turbo/` — Plantillas estándar de RappiTurbo
- `pro/` — Plantillas de RappiPro
- `travel/` — Plantillas de RappiTravel
- `restaurants/` — Plantillas de Restaurantes

## Estado actual

> **En construcción.** Esta carpeta arranca vacía. A medida que el equipo identifique mails que se repiten con frecuencia, se irán guardando aquí como plantillas oficiales del sistema.

## Cómo crear un template

1. Identifica una estructura que se repite (por ejemplo: Turbo siempre usa banner vertical + 2 CTAs + cierre).
2. Arma el mail combinando los componentes correspondientes de `03-components/`.
3. Aplica el estilo visual de `04-variants/` que corresponda.
4. Reemplaza los textos e imágenes específicas por textos de ejemplo genéricos.
5. Guarda el archivo aquí con un nombre descriptivo.
6. Agrega una línea en este README explicando cuándo se usa.

## La diferencia entre un componente y un template

- Un **componente** es una pieza. Un bloque visual individual, sin sentido completo por sí solo.
- Un **template** es una combinación. Un mail casi listo donde solo se cambian textos e imágenes.

Los templates son el atajo: en vez de armar cada mail desde cero, usas uno que ya tiene la estructura correcta y solo personalizas el contenido.
