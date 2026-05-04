# 04 · Variants

> Las skins. Los estilos visuales que se aplican encima de los componentes.

Un mismo mail puede verse de 5 formas distintas según su "Tipo de KV". Esta carpeta contiene esos 5 estilos visuales como archivos separados. Las piezas del mail son siempre las mismas; lo que cambia es el "look" visual que se aplica encima.

## Los 5 tipos de KV

| Variante | Cuándo se usa | Qué lo distingue visualmente |
|----------|--------------|------------------------------|
| `generico.css` | Mails generales de Rappi | Fondo muy oscuro, gradiente de colores Neon |
| `turbo.css` | Mails de RappiTurbo | Fondo verde oscuro, sin imagen de fondo en el banner |
| `neutro.css` | Mails sin marca dominante | Fondo negro semitransparente |
| `pro.css` | Mails de RappiPro | Fondo gris claro, gradiente suave, separadores dorados |
| `pro-black.css` | Mails de RappiPro Black | Fondo oscuro grisáceo, separadores dorados |

## Estado actual

> **En construcción.** Hoy, las instrucciones de qué cambiar según el tipo de KV están escritas como comentarios dentro de cada componente. Se ven así:
>
> ```
> si Tipo de KV = Pro      → el color de fondo debe ser gris claro
> si Tipo de KV = ProBlack → el color de fondo debe ser gris oscuro
> ```
>
> El próximo paso es **extraer esas instrucciones y convertirlas en archivos de estilos reales** (uno por tipo de KV) que se apliquen automáticamente encima del mail base.

Cuando esto esté listo, generar un mail Pro será simplemente:

```
Armar el mail con los componentes normales
   ↓
Aplicar el estilo "pro" encima
   ↓
Listo — todo queda con el look Pro automáticamente
```

En lugar de tener que leer decenas de comentarios condicionales y cambiar cada valor manualmente.

## Por qué esto importa

Hoy, para producir un mail Pro:
1. Se toma el mail base
2. Se leen TODOS los comentarios del tipo "si Tipo de KV = Pro..."
3. Se cambia manualmente cada valor en cada componente

Con esta carpeta funcionando, el flujo sería:
1. Se toma el mail base
2. Se aplica el archivo `pro.css` encima
3. Listo

**Los componentes no cambian.** El estilo visual se aplica como una capa adicional. Esto mantiene las piezas limpias y reutilizables para cualquier tipo de KV.
