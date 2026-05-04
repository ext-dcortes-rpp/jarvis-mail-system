# 01 · Foundations

> Las reglas del sistema. Lo que nunca cambia.

Aquí viven las reglas visuales que todos los bloques del sistema respetan: tipografías, colores, tamaños, separadores y cómo se ve el mail en celular. **Nadie debería tocar esta carpeta sin coordinarlo con el equipo de diseño**, porque cualquier cambio aquí afecta a TODOS los mails.

## Archivos

### `global-styles/global-styles.html`
Este archivo contiene todas las reglas visuales del sistema en un solo lugar:

- Tamaños y estilos de los textos (títulos grandes, subtítulos, textos pequeños)
- Los espaciados entre bloques (separador grande, mediano y pequeño)
- Cómo se ve el contenedor principal del mail
- Cómo se adapta el mail cuando se abre desde un celular
- Las clases visuales de los headers y banners
- Las clases de alineación de textos e imágenes

Adentro hay comentarios con instrucciones como:

```
si Tipo de KV = Generico → el fondo debe ser la imagen del KV genérico
si Tipo de KV = Turbo    → el fondo debe ser la imagen del KV Turbo
si Tipo de KV = Pro      → el fondo debe ser color claro
```

Estas instrucciones explican qué cambiar según el "look" del mail. Se materializan en la carpeta `04-variants/`.

### `global-styles/head-meta-tags.html`
Configuración técnica que va al inicio del mail: define el idioma, el tipo de caracteres y cómo se ve en Outlook. Este archivo va primero, antes de los estilos visuales.

**No se toca.** Está fijo para todos los mails.

## Tokens de diseño (próximamente)

La carpeta `tokens/` está reservada para cuando el sistema migre a variables de diseño centralizadas. Por ahora está vacía. Cuando exista, contendrá:

- `colors.css` — Los colores del sistema: naranja, rojo, rosa, fucsia + neutros
- `spacing.css` — Los tamaños de los separadores (grande: 16px, mediano: 10px, pequeño: 4px)
- `radii.css` — Los bordes redondeados que se repiten en los componentes
- `typography.css` — La fuente Trebuchet/Arial y la escala de tamaños de texto

## Por qué esta carpeta existe aparte

Cuando alguien quiere saber "¿cuál es el color naranja del sistema?" o "¿cuánto mide el separador mediano?", no debería tener que abrir un componente y revisar línea por línea. Esa información vive aquí.

Si eres nuevo en el proyecto, empezar por esta carpeta te da la base visual de todo el sistema.
