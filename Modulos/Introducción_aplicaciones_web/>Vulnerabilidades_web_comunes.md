# Vulnerabilidades web comunes

Si estuviéramos realizando una prueba de penetración en una aplicación web desarrollada internamente o no encontráramos ningún exploit público para una aplicación web pública, podríamos identificar manualmente varias vulnerabilidades. También podemos descubrir vulnerabilidades causadas por configuraciones incorrectas, incluso en aplicaciones web disponibles públicamente, ya que este tipo de vulnerabilidades no son causadas por la versión pública de la aplicación web sino por una configuración incorrecta realizada por los desarrolladores. Los siguientes ejemplos son algunos de los tipos de vulnerabilidad más comunes para aplicaciones web, parte de Los 10 mejores de OWASP vulnerabilidades para aplicaciones web.

## Autenticación/control de acceso rotos

**Broken authentication** y **Broken Access Control** se encuentran entre las vulnerabilidades más comunes y peligrosas para las aplicaciones web.

**Broken Authentication** se refiere a vulnerabilidades que permiten a los atacantes eludir las funciones de autenticación. Por ejemplo, esto puede permitir que un atacante inicie sesión sin tener un conjunto válido de credenciales o permitir que un usuario normal se convierta en administrador sin tener los privilegios para hacerlo.

**Broken Access Control** se refiere a vulnerabilidades que permiten a los atacantes acceder a páginas y funciones a las que no deberían tener acceso. Por ejemplo, un usuario normal obtiene acceso al panel de administración.

> Por ejemplo, College Management System 1.2 tiene una simple Omisión de autenticación vulnerabilidad que nos permite iniciar sesión sin tener cuenta, ingresando lo siguiente para el campo de correo electrónico: `' or 0=0 #`, y usando cualquier contraseña con él.

## Carga de archivos maliciosos

Otra forma común de obtener control sobre las aplicaciones web es mediante la carga de scripts maliciosos. Si la aplicación web tiene una función de carga de archivos y no valida correctamente los archivos cargados, podemos cargar un script malicioso (por ejemplo, un archivo `.php`), que nos permitirá ejecutar comandos en el servidor remoto.

Aunque se trata de una vulnerabilidad básica, muchos desarrolladores no son conscientes de estas amenazas, por lo que no comprueban ni validan adecuadamente los archivos cargados. Además, algunos desarrolladores realizan comprobaciones e intentan validar los archivos cargados, pero estas comprobaciones a menudo se pueden omitir, lo que aún nos permitiría cargar scripts maliciosos.

> Por ejemplo, el complemento de WordPress *Responsive Thumbnail Slider 1.0* se puede aprovechar para cargar cualquier archivo arbitrario, incluidos scripts maliciosos, cargando un archivo con doble extensión (p. ej. `shell.php.jpg`). Incluso hay un módulo Metasploit que permite explotar esta vulnerabilidad fácilmente.

## Inyección de comandos

Muchas aplicaciones web ejecutan comandos locales del sistema operativo para realizar ciertos procesos. Por ejemplo, una aplicación web puede instalar un complemento descargándolo usando un nombre proporcionado por el usuario. Si no se filtran y desinfectan adecuadamente estos valores, los atacantes pueden inyectar otro comando para ejecutar junto con el comando previsto originalmente (por ejemplo, dentro del nombre del complemento), lo que les permite ejecutar comandos directamente en el servidor back-end y obtener control sobre él. Este tipo de vulnerabilidad se llama **inyección de comandos**.

Esta vulnerabilidad está muy extendida, ya que es posible que los desarrolladores no desinfecten adecuadamente la entrada del usuario o utilicen comprobaciones débiles, permitiendo a los atacantes eludir cualquier verificación implementada.

> Por ejemplo, el complemento de WordPress *Plainview Activity Monitor 20161228* tiene una vulnerabilidad que permite a los atacantes inyectar su comando en el valor `ip`, simplemente añadiendo `| COMMAND...` después del valor `ip`.

## Inyección SQL (SQLi)

Otra vulnerabilidad muy común en las aplicaciones web es la **inyección SQL**. De manera similar a una vulnerabilidad de inyección de comandos, esta vulnerabilidad puede ocurrir cuando la aplicación web ejecuta una consulta SQL que incluye valores tomados de la entrada proporcionada por el usuario.

Por ejemplo, en la sección de bases de datos vimos un ejemplo de cómo una aplicación web usaría la entrada del usuario para buscar dentro de una determinada tabla, con la siguiente línea de código:

```php
$query = "select * from users where name like '%$searchInput%'";
$result = $conn->query($query);
```

Si la entrada del usuario no se filtra y valida correctamente, podemos ejecutar otra consulta SQL junto con esta consulta, lo que eventualmente puede permitirnos tomar el control de la base de datos y su servidor de alojamiento.

> Por ejemplo, el mismo College Management System 1.2 sufre de una inyección SQL que permite ejecutar una consulta que siempre devuelve true, autenticándonos correctamente y permitiendo el acceso a la aplicación. También se puede usar para extraer datos de la base de datos o incluso obtener control del servidor.

## Conclusión

Veremos estas vulnerabilidades una y otra vez en nuestro viaje de aprendizaje y en evaluaciones reales. Es importante familiarizarse con cada una de ellas, ya que incluso una comprensión básica da una ventaja en el campo de la seguridad de la información. Los módulos posteriores cubrirán en profundidad cada una de estas vulnerabilidades.
