# 02 · Base Template

> El esqueleto. El tablero donde se montan los bricks.

Esta carpeta contiene la estructura HTML que **nunca cambia entre un mail y otro**. Doctype, head, body, los wrappers que envuelven todo. Si tocas esto, rompes todos los mails.

## Archivos

### `opening.html`
Apertura completa del HTML hasta el inicio del header. Incluye:
- `<!doctype html>` y la etiqueta `<html>`
- Meta tags (charset, viewport, conditional comments para Outlook)
- El bloque `<style>` completo (importado desde `01-foundations/global-styles/`)
- Apertura del `<body>`
- El `<center class="wrapper">` con el background del KV
- La tabla wrapper general
- El `<!-- CONTENEDOR GENERAL -->` y la apertura del banner

Termina justo antes de `<!-- INICIO HEADER GENERAL -->`.

### `body-wrapper-open.html`
Después del banner y antes de los CTAs/deals/cupones/módulos, hay una tabla que envuelve la zona de contenido del mail. Esta apertura está aquí. Contiene los comentarios sobre cómo separar bloques entre sí:

> cuando se inserte un contenedor con `role="module"` y debajo se encuentre uno con el mismo role, debes insertar entre uno y otro la div: `<div class="separador"></div>`

### `body-wrapper-close.html`
Cierre de la tabla del cuerpo. Va justo después del cierre y antes del footer.

### `closing.html`
Cierres finales del HTML: el cierre del wrapper, los conditional comments de Outlook, `</body>`, `</html>`.

## Cómo se usa

El orden de ensamblaje siempre es:

```
opening.html
   ↓
[un header de 03-components/headers/]
   ↓
[un banner de 03-components/banners/]
   ↓
body-wrapper-open.html
   ↓
[CTAs, deals, cupones, beneficios, módulos en orden libre]
   ↓
[cierre.html de 03-components/closing/ — opcional]
   ↓
body-wrapper-close.html
   ↓
[footer de 03-components/footer/]
   ↓
closing.html
```

## Regla de oro

Si te encuentras cambiando algo de esta carpeta, para. Casi siempre el cambio que necesitas hacer está en otro lado: en un componente (`03-components/`), en una skin (`04-variants/`), o en los foundations (`01-foundations/`).

El esqueleto es lo único que no se toca.
