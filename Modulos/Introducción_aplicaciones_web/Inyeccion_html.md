# Inyección HTML

Otro aspecto importante de la seguridad del frontend es validar y desinfectar las entradas aceptadas por los usuarios. En muchos casos, la validación y desinfección de la entrada del usuario se lleva a cabo en el back-end. Sin embargo, algunas entradas del usuario nunca llegarían al back-end en algunos casos y se procesan y representan completamente en el front-end. Por lo tanto, es fundamental validar y desinfectar la entrada del usuario tanto en el front-end como en el back-end.

**Inyección HTML** ocurre cuando se muestra una entrada de usuario sin filtrar en la página. Esto puede hacerse recuperando código enviado previamente, como recuperar un comentario de usuario de la base de datos del back-end, o mostrando directamente la entrada del usuario sin filtrar a través de JavaScript en la parte delantera.

Cuando un usuario tiene control total de cómo se mostrará su entrada, puede enviar código HTML y el navegador puede mostrarlo como parte de la página. Esto puede incluir un código HTML malicioso, como un formulario de inicio de sesión externo, que se puede utilizar para engañar a los usuarios para que inicien sesión mientras envían sus credenciales de inicio de sesión a un servidor malicioso para recopilarlas para otros ataques.

Otro ejemplo de **HTML Injection** es desfigurar la página web. Esto consiste en inyectar nuevo código HTML para cambiar la apariencia de la página web, insertar anuncios maliciosos o incluso cambiar completamente la página. Este tipo de ataque puede provocar graves daños a la reputación de la empresa que aloja la aplicación web.

---

## Ejemplo

El siguiente ejemplo es una página web muy básica con un solo botón "Click to enter your name." Cuando hacemos clic en el botón, nos solicita que ingresemos nuestro nombre y luego muestra nuestro nombre como "Your name is ...":

> Botón denominado “Haga clic para ingresar su nombre” y texto “Su nombre es usuario”.

Si no se implementa ninguna desinfección de entrada, este es potencialmente un objetivo fácil de **HTML Injection** y **Cross-Site Scripting (XSS)**. Echamos un vistazo al código fuente de la página y no vemos ninguna desinfección de entrada, ya que la página toma la entrada del usuario y la muestra directamente:

```html
<!DOCTYPE html>
<html>

<body>
    <button onclick="inputFunction()">Click to enter your name</button>
    <p id="output"></p>

    <script>
        function inputFunction() {
            var input = prompt("Please enter your name", "");

            if (input != null) {
                document.getElementById("output").innerHTML = "Your name is " + input;
            }
        }
    </script>
</body>

</html>
```

Para probar **HTML Injection**, simplemente podemos ingresar un pequeño fragmento de código HTML como nuestro nombre y ver si se muestra como parte de la página. Probaremos el siguiente código, que cambia la imagen de fondo de la página web:

```html
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```

Una vez que lo ingresamos, vemos que la imagen de fondo de la página web cambia instantáneamente:

> Botón denominado 'Haga clic para ingresar su nombre' y escriba 'Su nombre es' junto al logotipo de 'ACADEMY'.

En este ejemplo, como todo se lleva a cabo en el frontend, actualizar la página web restablecería todo a la normalidad.
