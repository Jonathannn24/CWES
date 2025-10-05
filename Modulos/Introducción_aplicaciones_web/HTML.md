# HTML — Introducción

## Resumen (importante)
- **HTML** (HyperText Markup Language) es el componente principal del frontend: estructura títulos, párrafos, imágenes, formularios y otros elementos.
- Los navegadores **interpretan** HTML y muestran la página al usuario.
- HTML se organiza en un **árbol DOM** (document → html → head/body → elementos).
- Las **etiquetas** abren y cierran elementos (`<p>...</p>`); pueden llevar `id` y `class`.
- **Codificación de URL**: caracteres no ASCII se codifican con `%` seguido de dos hex (ej. espacio → `%20`, `'` → `%27`).
- Elementos importantes dentro de `<head>`: `<title>`, `<style>`, `<script>`.
- Conocer el DOM ayuda en pruebas y explotación (ej. XSS) para localizar y manipular elementos.

---

## Contenido completo

El primer y más dominante componente del frontend de las aplicaciones web es **HTML** (Lenguaje de Marcado de Hipertexto). HTML está en el centro de cualquier página web que veamos en Internet. Contiene los elementos básicos de cada página, incluidos títulos, formularios, imágenes y muchos otros elementos. El navegador web, a su vez, interpreta estos elementos y los muestra al usuario final.

### Ejemplo básico
```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
    </head>
    <body>
        <h1>A Heading</h1>
        <p>A Paragraph</p>
    </body>
</html>
```

Esto mostraría lo siguiente: Ventana del navegador con título de página 'Título de página', URL 'www.example.com', encabezado 'Un encabezado' y párrafo 'Un párrafo'.

### Estructura y árbol
Los elementos HTML se muestran en forma de árbol, similar a XML:

```
document
 - html
   -- head
      --- title
   -- body
      --- h1
      --- p
```

Cada elemento puede contener otros elementos HTML, mientras que la etiqueta principal `<html>` debe contener todos los demás elementos dentro de la página.

Ejemplo en etiquetas:
```html
<html>
  <head>
    <title>Título de la página</title>
  </head>
  <body>
    <h1>Un encabezado</h1>
    <p>Un párrafo</p>
  </body>
</html>
```

Las etiquetas también pueden contener el `id` o la `class` del elemento, por ejemplo:
```html
<p id="para1" class="red-paragraphs">Texto</p>
```

### Codificación de URL (percent-encoding)
En las URL solo se permiten ciertos caracteres; otros deben codificarse con `%` seguido de dos dígitos hexadecimales:

- Ejemplo: `'` → `%27`
- Espacio → `%20` (o `+` en algunos contextos)

Tabla parcial:
| Carácter | Codificación |
|---|---|
| espacio | `%20` |
| ! | `%21` |
| " | `%22` |
| # | `%23` |
| $ | `%24` |
| % | `%25` |
| & | `%26` |
| ' | `%27` |
| ( | `%28` |
| ) | `%29` |

### Uso de `<head>` y `<body>`
- `<head>`: elementos que no se muestran directamente (ej. `<title>`, `<meta>`, `<style>`, `<script>`).
- `<body>`: contenido visible de la página.

### DOM (Document Object Model)
El DOM permite acceder y modificar dinámicamente la estructura, el contenido y el estilo del documento desde scripts (ej. `document.head`, `document.querySelector()`).

El estándar DOM se divide en:
- Core DOM
- XML DOM
- HTML DOM

Conocer la estructura del DOM ayuda a:
- Encontrar elementos en la página por `id`, `class` o etiqueta.
- Manipular elementos para pruebas o explotación (ej. **XSS**), inyección de nuevos elementos, etc.

---

## Consejos prácticos
- Usa las herramientas de desarrollo del navegador (DevTools) para inspeccionar el DOM y ver código fuente de elementos específicos.
- Practica codificación/decodificación de URL para entender cómo se envían parámetros.
- Aprende a localizar elementos por `id`, `name` o `class` para automatizar interacciones o pruebas.

---
