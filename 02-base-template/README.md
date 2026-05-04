# 02 · Base Template

> El esqueleto. El tablero donde se montan los bricks.

Esta carpeta contiene la estructura del mail que **nunca cambia de un mail a otro**: el inicio, la apertura de la zona de contenido, el cierre de esa zona y el final. Si modificas algo de aquí, rompes todos los mails.

## Archivos

### `opening.html`
El inicio obligatorio de todo mail. Siempre va primero, antes de cualquier otra pieza. Contiene:

- La configuración técnica del mail (idioma, caracteres, compatibilidad con Outlook)
- Todos los estilos visuales del sistema (tamaños, colores, fuentes)
- La apertura del cuerpo del mail
- El contenedor general que envuelve todo

Termina justo antes de donde empieza el header.

### `body-wrapper-open.html`
Se pega **después del banner** y **antes de empezar a poner CTAs, deals o módulos**. Abre la zona de contenido central del mail.

Adentro tiene un recordatorio importante:

> Cuando dos bloques de contenido van uno debajo del otro, hay que poner entre ellos el separador correspondiente.

### `body-wrapper-close.html`
Se pega **después del último bloque de contenido** (CTA, deal o módulo) y **antes del footer**. Cierra la zona de contenido central.

### `closing.html`
El final obligatorio de todo mail. Siempre va último, después del footer. Cierra correctamente el mail para que se vea bien en todos los clientes de correo.

## Cómo se usa — el orden de ensamblaje

```
opening.html
   ↓
[un header de 03-components/headers/]
   ↓
[un banner de 03-components/banners/]
   ↓
body-wrapper-open.html
   ↓
[CTAs, deals, módulos en el orden que necesites]
   ↓
[cierre.html de 03-components/closing/ — si aplica]
   ↓
body-wrapper-close.html
   ↓
[footer de 03-components/footer/]
   ↓
closing.html
```

## Regla de oro

Si sientes que necesitas cambiar algo de esta carpeta, detente. Casi siempre lo que necesitas cambiar está en otro lugar: en un componente (`03-components/`), en una variante visual (`04-variants/`), o en las reglas base (`01-foundations/`).

**El esqueleto no se toca.**
