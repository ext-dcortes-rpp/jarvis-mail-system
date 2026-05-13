# 04 · Variants

> Las skins. Los estilos visuales que se aplican encima de los componentes.

Un mismo componente puede verse de 5 formas distintas según el "Tipo de KV" del mail. Esta carpeta contiene esas 5 variantes como archivos separados.

## Los 5 KV types

| Variante | Cuándo se usa | Características clave |
|----------|---------------|----------------------|
| `generico.css` | Mails generales de Rappi | Background `#040404`, gradiente Neon |
| `turbo.css` | Mails de RappiTurbo | Verde oscuro, sin background-image en el banner |
| `neutro.css` | Mails neutros sin marca dominante | Negro semitransparente |
| `pro.css` | Mails de RappiPro | Background `#ECEFF3`, gradiente claro, separadores dorados |
| `pro-black.css` | Mails de RappiPro Black | Background `#2A2B2B`, separadores dorados |

## Estado actual

> **Por construir.** Las reglas de KV están hoy comentadas dentro de cada componente. El siguiente paso es extraerlas y convertirlas en archivos CSS reales que se apliquen como capa encima del HTML base.

Reglas especiales para Pro/ProBlack que aparecen repetidamente:
- En el módulo de título, agregar `padding:15px` y background gris claro (Pro) u oscuro (ProBlack)
- Agregar el separador dorado debajo del subtítulo: `border-top: 1px solid #DAA868; width: 50px;`
- En los bullets numerados, cambiar el `border-right` a `#DAA868`
- En el value prop de cupones, usar color `#DAA868`
- En el footer, usar `font_style_look = 'pro'`
- **Eliminar la tabla de cierre completa** (no aplica para Pro/ProBlack)

## Por qué esto importa

Hoy, cuando el equipo necesita producir un mail Pro:
1. Toma el HTML base
2. Lee TODOS los comentarios condicionales tipo "si Tipo de Kv = Pro..."
3. Cambia manualmente cada valor

Con esta carpeta funcionando, el flujo sería:
1. Toma el HTML base
2. Aplica `pro.css` encima
3. Listo

Los componentes no cambian. Las skins se aplican como una capa adicional.
