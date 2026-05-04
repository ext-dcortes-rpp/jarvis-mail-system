# Guía: Cómo armar un mail desde cero

Esta guía es para diseñadores y miembros del equipo que quieren entender el flujo completo, **sin necesidad de saber programación ni HTML**.

## La idea básica

Armar un mail es exactamente como armar un set de LEGO:

1. Empiezas con el **tablero base** (dos archivos fijos que siempre van al inicio y al final).
2. Eliges **una cabeza** para el muñeco (un header de la marca).
3. Eliges **un torso** (un banner: el bloque visual principal del mail).
4. Le agregas **accesorios** al gusto (botones de acción, deals, módulos de contenido).
5. Le pones **los zapatos** (imagen de cierre + footer).

Cada pieza encaja con cualquier otra porque todas siguen las mismas reglas de diseño. No necesitas saber por qué encajan — solo combinarlas.

---

## Los pasos

### Paso 1 — Define el tipo de mail

Antes de abrir cualquier archivo, responde estas tres preguntas:

**¿Qué KV?** (el "look" visual del mail)
- Genérico, Turbo, Neutro, Pro o Pro Black
- Esto define los colores, fondos y separadores del mail

**¿Qué marca?**
- Rappi, Travel, Turbo, Turbo Rest, Pro o Pro Black
- Esto define qué header vas a usar

**¿Qué contenido tiene el cuerpo?**
- ¿Solo un banner con botón de acción?
- ¿También lleva deals o módulos de contenido?
- Esto define qué tipo de banner usar y qué piezas agregar al cuerpo

---

### Paso 2 — Abre con el archivo de inicio

Toma `02-base-template/opening.html` y pégalo al comienzo. Es el inicio obligatorio de todo mail. No se modifica.

---

### Paso 3 — Agrega el header

De la carpeta `03-components/headers/`, elige el archivo que corresponde a la marca:

| Marca | Archivo |
|-------|---------|
| Rappi general | `rappi.html` |
| RappiTravel | `rappi-travel.html` |
| RappiTurbo | `rappi-turbo.html` |
| RappiTurbo Restaurantes | `rappi-turbo-rest.html` |
| RappiPro | `rappi-pro.html` |
| RappiPro Black | `rappi-pro-black.html` |

El header va dentro del archivo `_header-wrapper.html`, que es la envoltura común a todos. Primero pega el wrapper, luego dentro pega el header elegido.

**¿Hay cobranding con otra marca?** Dentro del archivo del header, hay instrucciones (escritas como comentarios) para elegir entre tres modos:
- **Sin cobranding** — solo el logo de Rappi
- **Modo "Tag"** — si el partner te da una imagen tipo etiqueta
- **Modo "1:1"** — si el partner te da un logo cuadrado

Lee los comentarios del archivo: te dicen exactamente qué conservar y qué eliminar.

---

### Paso 4 — Agrega el banner

De la carpeta `03-components/banners/`, elige UNO según el contenido del mail:

| Si el mail tiene... | Usa este banner |
|--------------------|-----------------|
| Módulos de contenido en el cuerpo (además del CTA) | `big-banner-horizontal.html` |
| Solo CTA y cierre, o banner con logos | `big-banner-vertical.html` |
| Solo una imagen grande, sin texto encima | `banner-editorial.html` |

**Dentro del banner que elegiste:**
1. Reemplaza la URL de la imagen de fondo por la que corresponde al KV del mail
2. Si la fuente trae una etiqueta (TAG) encima del banner, consérvala y cambia el texto; si no, elimina esa sección
3. Completa los textos: título principal, subtítulo, textos de apoyo según la jerarquía de la fuente
4. Agrega el logo si aplica; si no, elimina esa sección
5. Agrega el texto de refuerzo si aplica; si no, elimina esa sección

Cada sección dentro del banner tiene comentarios que te dicen exactamente qué hacer con ella.

---

### Paso 5 — Abre la zona de contenido

Pega `02-base-template/body-wrapper-open.html`. Esto abre el área donde van los botones de acción, los deals y los módulos de contenido.

---

### Paso 6 — Arma el cuerpo del mail

Aquí decides qué piezas pones y en qué orden. Tus opciones son:

| Pieza | Archivo | Notas |
|-------|---------|-------|
| Botón de acción (CTA) | `03-components/ctas/cta-template.html` | Puedes poner varios |
| Deal grande | `03-components/deals/deal-large.html` | Máx. 4 deals en total |
| Deal small | `03-components/deals/deal-small.html` | Versión compacta del deal |
| Módulo de título | `03-components/content-modules/modulo-titulo.html` | Solo un título destacado |
| Módulo 3 columnas | `03-components/content-modules/modulo-3-columnas.html` | Tres columnas de imagen + texto |
| Módulo 2 columnas | `03-components/content-modules/modulo-2-columnas.html` | Dos columnas con imagen y texto |
| Módulo de logos | `03-components/content-modules/modulo-logos.html` | Grilla de logos |
| Módulo de contenido | `03-components/content-modules/modulo-contenido.html` | El más versátil |

**Regla de espaciado entre piezas:**

Entre una pieza y la siguiente, hay que poner un separador. Copia esta línea y pégala entre bloques de contenido:

```html
<div class="separador"></div>
```

Las excepciones:
- Entre un CTA y la imagen de cierre → no va separador
- Entre dos deals → no va separador (los deals tienen su propio aire interno)

---

### Paso 7 — Agrega la imagen de cierre (si aplica)

De `03-components/closing/cierre.html`.

**¿Cuándo se omite?**
- Si el tipo de KV es Pro o Pro Black → no va cierre
- Si la fuente del mail dice explícitamente "sin cierre" → no va cierre

En cualquier otro caso, se conserva y se reemplaza la URL de la imagen con la que corresponde al KV.

---

### Paso 8 — Cierra la zona de contenido

Pega `02-base-template/body-wrapper-close.html`.

---

### Paso 9 — Agrega el footer

De `03-components/footer/footer.html`. **El footer siempre va, en todos los mails.** Solo se cambian las variables según lo que indique la fuente:

| Variable | Qué define | Valores posibles |
|----------|-----------|-----------------|
| `cond` | Texto de legales adicionales | El texto que venga en la fuente (si no hay, va vacío) |
| `font_style_look` | El estilo visual del footer | `negro` para Genérico/Turbo/Neutro · `pro` para Pro/ProBlack |
| `show_legal_tyc` | Si muestra el legal de términos y condiciones | `true` o `false` según la fuente |
| `show_legal_turbo` | Si muestra el legal de Turbo | `true` o `false` según la fuente |
| `show_legal_liquor` | Si muestra el legal de bebidas alcohólicas | `true` o `false` según la fuente |

---

### Paso 10 — Cierra el mail

Pega `02-base-template/closing.html`. Es el cierre obligatorio de todo mail. No se modifica.

---

## El mail terminado

Si seguiste todos los pasos, tu mail tiene esta estructura:

```
[opening.html]                          ← inicio obligatorio
   ↓
[_header-wrapper.html → header elegido] ← identidad de marca
   ↓
[banner elegido]                         ← imagen principal
   ↓
[body-wrapper-open.html]                ← abre zona de contenido
   ↓
[CTAs · deals · módulos en orden libre] ← el cuerpo del mail
   ↓
[cierre.html — si aplica]               ← imagen de cierre
   ↓
[body-wrapper-close.html]               ← cierra zona de contenido
   ↓
[footer.html]                           ← pie del mail
   ↓
[closing.html]                          ← fin obligatorio
```

Eso es todo. Cada pieza encaja con las demás porque todas fueron diseñadas para trabajar juntas.
