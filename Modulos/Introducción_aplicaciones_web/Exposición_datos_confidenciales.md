# Exposición de datos confidenciales

Todos los componentes del front-end que cubrimos interactúan en el lado del cliente. Por lo tanto, si son atacados, no representan una amenaza directa para el núcleo back-end de la aplicación web y normalmente no provocarán daños permanentes. Sin embargo, como estos componentes se ejecutan en el client-side, ponen al usuario final en peligro de ser atacado y explotado si tienen alguna vulnerabilidad. Si se aprovecha una vulnerabilidad de interfaz para atacar a los usuarios administradores, podría provocar acceso no autorizado, acceso a datos confidenciales, interrupción del servicio y más.

Aunque la mayoría de las pruebas de penetración de aplicaciones web se centran en los componentes del back-end y su funcionalidad, también es importante probar los componentes del front-end para detectar posibles vulnerabilidades, ya que este tipo de vulnerabilidades a veces se pueden utilizar para obtener acceso a funcionalidades confidenciales (por ejemplo, un panel de administración), lo que puede comprometer todo el servidor.

**Exposición de datos confidenciales** se refiere a la disponibilidad de datos confidenciales en texto claro para el usuario final. Esto se encuentra generalmente en el _source code_ de la página web o fuente de la página en la interfaz de las aplicaciones web. Este es el código fuente HTML de la aplicación, que no debe confundirse con el código back-end al que normalmente solo se puede acceder en el propio servidor. Podemos ver la fuente de la página de cualquier sitio web en nuestro navegador haciendo clic derecho en cualquier parte de la página y seleccionando *View Page Source* desde el menú emergente. A veces, un desarrollador puede desactivar el clic derecho en una aplicación web, pero esto no nos impide ver el código fuente de la página, ya que simplemente podemos escribir `Ctrl+U` o ver el código fuente de la página a través de un proxy web como Burp Suite. Echemos un vistazo al código fuente de la página `google.com`. Haga clic derecho y elija *View Page Source*, y se abrirá una nueva pestaña en nuestro navegador con la URL `view-source:https://www.google.com/`. Aquí podemos ver el HTML, JavaScript, y enlaces externos. Tómese un momento para explorar un poco el código fuente de la página.

A veces podemos encontrar credenciales de inicio de sesión, hashes, u otros datos confidenciales ocultos en los comentarios del código fuente de una página web o dentro de datos externos JavaScript que se importan. Otra información confidencial puede incluir enlaces o directorios expuestos o incluso información de usuario expuesta, todo lo cual puede aprovecharse potencialmente para promover nuestro acceso dentro de la aplicación web o incluso la infraestructura de soporte de la aplicación web (servidor web, servidor de base de datos, etc.).

Por esta razón, una de las primeras cosas que debemos hacer al evaluar una aplicación web es revisar el código fuente de su página para ver si podemos identificar algún "fruto al alcance de la mano", como credenciales expuestas o enlaces ocultos.

## Ejemplo

A primera vista, este formulario de inicio de sesión no parece nada fuera de lo común:

```html
<form action="action_page.php" method="post">

    <div class="container">
        <label for="uname"><b>Username</b></label>
        <input type="text" required>

        <label for="psw"><b>Password</b></label>
        <input type="password" required>

        <!-- TODO: remove test credentials test:test -->

        <button type="submit">Login</button>
    </div>
</form>
```

Vemos que los desarrolladores agregaron algunos comentarios que olvidaron eliminar, que contienen credenciales de prueba:

```html
<!-- TODO: remove test credentials test:test -->
```

El comentario parece ser un recordatorio para que los desarrolladores eliminen las credenciales de prueba. Dado que el comentario aún no ha sido eliminado, estas credenciales aún pueden ser válidas.

Aunque no es muy común encontrar credenciales de inicio de sesión en los comentarios de los desarrolladores, aún podemos encontrar varios fragmentos de información confidencial y valiosa al mirar el código fuente, como páginas o directorios de prueba, parámetros de depuración u funcionalidad oculta. Existen varias herramientas automatizadas que podemos utilizar para escanear y analizar el código fuente de la página disponible para identificar posibles rutas o directorios y otra información confidencial.

Aprovechar este tipo de información puede brindarnos mayor acceso a la aplicación web, lo que puede ayudarnos a atacar los componentes del back-end para obtener control sobre el servidor.

## Prevención

Lo ideal sería que el código fuente del front-end solo contuviera el código necesario para ejecutar todas las funciones de las aplicaciones web, sin ningún código adicional ni comentarios que no sean necesarios para que la aplicación web funcione correctamente. Siempre es importante revisar el código que será visible para los usuarios finales a través de la fuente de la página o ejecutarlo a través de herramientas para verificar si hay información expuesta.

También es importante clasificar los tipos de datos dentro del código fuente y aplicar controles sobre lo que puede o no exponerse en el lado del cliente. Los desarrolladores también deben revisar el código del lado del cliente para asegurarse de que no queden comentarios innecesarios ni enlaces ocultos. Además, es posible que los desarrolladores front-end quieran utilizar empaquetado u ofuscación de código JavaScript para reducir las posibilidades de exponer datos confidenciales en el código JavaScript. Estas técnicas pueden impedir que las herramientas automatizadas localicen este tipo de datos.
