# 05 · Templates

> Los modelos terminados. Combinaciones predefinidas listas para usar.

Mientras los `components/` son las piezas individuales, los `templates/` son combinaciones armadas que cubren los casos de uso más frecuentes.

## Subcarpetas

### `full-templates/`
Plantillas completas y genéricas, identificadas por su composición:
- `solo-banner.html` — Mail mínimo: header + banner + footer
- `banner-cta.html` — Header + banner + CTA + cierre + footer
- `banner-cta-deals.html` — Mail con deals
- `mail-con-cupones.html` — Mail con módulo de cupones
- `mail-con-beneficios.html` — Mail con beneficios
- `completo.html` — Plantilla con todos los módulos posibles (referencia)

### `by-vertical/`
Plantillas específicas por vertical de negocio:
- `turbo/` — Plantillas estándar de RappiTurbo
- `pro/` — Plantillas de RappiPro
- `travel/` — Plantillas de RappiTravel
- `restaurants/` — Plantillas de Restaurantes

## Estado actual

> **Por construir.** Esta carpeta queda vacía como punto de partida. A medida que el equipo identifique mails que se repiten con frecuencia, se irán agregando aquí como plantillas oficiales del sistema.
