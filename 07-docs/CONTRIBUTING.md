# Cómo contribuir al sistema

Este sistema vive porque el equipo lo cuida. Cualquier persona puede proponer cambios, pero hay reglas que se respetan para mantener la coherencia.

## Antes de cambiar algo

1. Lee el README principal y entiende la metáfora del LEGO.
2. Identifica qué tipo de cambio quieres hacer:
   - ¿Es un nuevo brick? → carpeta `03-components/`
   - ¿Es un tema nuevo o un ajuste de tono? → sección Liquid TEMAS en `01-foundations/global-styles/head-meta-tags.html`
   - ¿Es un nuevo template combinando bricks existentes? → carpeta `05-templates/`
   - ¿Es un cambio a las reglas globales? → STOP. Esto requiere discusión en equipo.

## Reglas

### Para componentes
- Cada componente vive en su propio archivo HTML.
- Los comentarios `INICIO` / `FIN` son obligatorios.
- Las instrucciones internas (los comentarios `<!-- -->` con reglas) son parte del componente y se conservan.
- No se agregan estilos inline sin coordinarlo con foundations.

### Para nombres de archivos
- Todo en kebab-case: `mi-nuevo-modulo.html`.
- Prefijos numéricos en carpetas para mantener orden: `01-foundations`, `02-base-template`...
- Prefijo `_` para archivos auxiliares que no son componentes finales: `_header-wrapper.html`.

### Para commits
- Mensajes en español, en imperativo: "Agrega módulo cupones", "Corrige padding del deal small".
- Un commit por cambio lógico.

## Proceso de cambio
1. Crea una rama desde `main`: `git checkout -b feat/nuevo-modulo`
2. Haz tus cambios.
3. Actualiza el README de la carpeta donde cambiaste algo.
4. Actualiza `07-docs/INDICE-DE-COMPONENTES.md` si agregaste un brick.
5. Abre un Pull Request.

## Decisiones que requieren consenso
- Cambios en `01-foundations/`
- Cambios en `02-base-template/`
- Eliminación de cualquier componente
- Renombrado de archivos
- Cambios en la estructura de carpetas
