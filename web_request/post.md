# POST — Solicitudes HTTP

A diferencia de **HTTP GET**, que coloca los parámetros del usuario dentro de la URL, **HTTP POST** coloca los parámetros del usuario dentro del **cuerpo** de la solicitud HTTP. Esto tiene tres beneficios principales:

- **Lack of Logging:** Como las solicitudes POST pueden transferir archivos grandes (por ejemplo, carga de archivos), no sería eficiente para el servidor registrar todos los archivos cargados como parte de la URL solicitada, como sería el caso de un archivo cargado a través de una solicitud GET.
- **Less Encoding Requirements:** Las URL están diseñadas para ser compartidas, lo que significa que deben ajustarse a caracteres que puedan convertirse en letras. La solicitud POST coloca datos en el cuerpo que pueden aceptar datos binarios. Los únicos caracteres que deben codificarse son aquellos que se utilizan para separar parámetros.
- **More data can be sent:** La longitud máxima de URL varía entre navegadores (Chrome/Firefox/IE), servidores web (IIS, Apache, nginx), redes de distribución de contenido (Fastly, Cloudfront, Cloudflare) e incluso acortadores de URL (bit.ly, amzn.to). En términos generales, las longitudes de una URL deben mantenerse por debajo de los 2000 caracteres, por lo que no pueden manejar una gran cantidad de datos.

Entonces, veamos algunos ejemplos de cómo funcionan las solicitudes POST y cómo podemos utilizar herramientas como **cURL** o las **herramientas de desarrollo del navegador** para leer y enviar solicitudes POST.

---

## Formularios de inicio de sesión

El ejercicio al final de esta sección es similar al ejemplo que vimos en la sección GET. Sin embargo, una vez que visitamos la aplicación web, vemos que utiliza un **formulario de inicio de sesión PHP** en lugar de autenticación básica HTTP:

```
http://<SERVER_IP>:<PORT>/
```
*Pantalla de inicio de sesión con campos para 'Nombre de usuario' y 'Contraseña' y un botón 'Iniciar sesión'.*

Si intentamos iniciar sesión con `admin:admin`, entramos y vemos una función de búsqueda similar a la que vimos anteriormente en la sección GET:

```
http://<SERVER_IP>:<PORT>/
```
*Icono de búsqueda con instrucción: 'Escriba el nombre de una ciudad y presione Enter'.*

Si borramos la pestaña **Red** en las herramientas de desarrollo de nuestro navegador e intentamos iniciar sesión nuevamente, veremos que se envían muchas solicitudes. Podemos filtrar las solicitudes por la IP de nuestro servidor, de modo que solo muestre las solicitudes que van al servidor web de la aplicación web (es decir, filtre las solicitudes externas) y notaremos que **se envía la siguiente solicitud POST**:

*La pestaña Red muestra tres solicitudes exitosas a 'server_ip', incluida una solicitud POST con nombre de usuario y contraseña 'admin'.*

Podemos hacer clic en la solicitud, hacer clic en la pestaña **Request** (que muestra el cuerpo de la solicitud) y luego hacer clic en **Raw** para mostrar los datos sin procesar de la solicitud. Vemos que los siguientes datos se envían como datos de solicitud POST:

```bash
username=admin&password=admin
```

Con los datos de la solicitud disponibles, podemos intentar enviar una solicitud similar con **cURL**, para ver si esto también nos permitiría iniciar sesión. Además, como hicimos en la sección anterior, podemos simplemente hacer clic derecho en la solicitud y seleccionar **Copy > Copy as cURL**. Sin embargo, es importante poder elaborar solicitudes POST manualmente, así que intentemos hacerlo.

Usaremos la bandera `-X POST` para enviar un **POST**. Luego, para agregar nuestros datos POST, podemos usar la bandera `-d` y agregar los datos anteriores después de él, de la siguiente manera:

```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
```

Salida (parcial):

```
...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```

> **Tip:** Muchos formularios de inicio de sesión nos redirigirían a una página diferente una vez autenticados (por ejemplo, `/dashboard.php`). Si queremos **seguir la redirección** con cURL, podemos utilizar la bandera `-L`.

---

## Cookies autenticadas

Si nos autenticamos correctamente, deberíamos haber recibido una **cookie** para que nuestros navegadores puedan conservar nuestra autenticación y no necesitemos iniciar sesión cada vez que visitamos la página. Podemos utilizar las banderas `-v` o `-i` para ver la respuesta, que debe contener el encabezado `Set-Cookie` con nuestra cookie autenticada:

```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i
```

Ejemplo de respuesta (parcial):

```
HTTP/1.1 200 OK
Date: 
Server: Apache/2.4.41 (Ubuntu)
Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```

Con nuestra cookie autenticada, ahora deberíamos poder interactuar con la aplicación web sin necesidad de proporcionar nuestras credenciales cada vez. Para probar esto, podemos **configurar la cookie** con la bandera `-b` en cURL, de la siguiente manera:

```bash
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```

Salida (parcial):

```
...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```

También es posible especificar la cookie como encabezado:

```bash
curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```

También podemos probar lo mismo con nuestros navegadores. Primero **cerremos sesión** y luego deberíamos regresar a la página de inicio de sesión. Luego podemos ir a la pestaña **Storage** en las herramientas de desarrollo con `[SHIFT+F9]`. En la pestaña Storage, podemos hacer clic en **Cookies** en el panel izquierdo y seleccionar nuestro sitio web para ver nuestras cookies actuales. Es posible que tengamos o no cookies existentes, pero si cerramos la sesión, entonces nuestra cookie PHP no debe autenticarse, por eso obtenemos el formulario de inicio de sesión y no la función de búsqueda.

Ahora, intentemos usar nuestra cookie autenticada anterior y veamos si logramos ingresar sin necesidad de proporcionar nuestras credenciales. Para ello:

1. Sustituimos el **valor de la cookie** por el nuestro, o
2. Hacemos clic derecho en la cookie y seleccionamos **Delete All**, y luego clic en el **+** para **agregar una nueva cookie**.  
   - **Nombre:** `PHPSESSID`  
   - **Valor:** `c1nsa6op7vtk7kdis7bcnbadf1`

Actualizamos la página y veremos que efectivamente nos autenticamos sin necesidad de iniciar sesión, simplemente usando una cookie autenticada.

> Como podemos ver, tener una cookie válida puede ser suficiente para autenticarse en muchas aplicaciones web. Esto puede ser una parte esencial de algunos ataques web, como **Cross-Site Scripting (XSS)**.

---

## Datos JSON

Finalmente, veamos qué solicitudes se envían cuando interactuamos con la **City Search**. Para hacerlo, iremos a la pestaña **Red** en las herramientas de desarrollo del navegador y luego haremos clic en el ícono de la papelera para borrar todas las solicitudes. Luego, podemos realizar cualquier consulta de búsqueda para ver qué solicitudes se envían.

*La pestaña Red muestra una solicitud POST exitosa a `server_ip` para `search.php` con carga útil `{'search':'London'}`.*

Como podemos ver, el formulario de búsqueda envía una **solicitud POST** a `search.php`, con los siguientes datos:

```json
{"search":"london"}
```

Los datos POST parecen estar en **formato JSON**, por lo que nuestra solicitud debe haber especificado el encabezado `Content-Type` a `application/json`. Podemos confirmarlo haciendo clic derecho en la solicitud y seleccionando **Copy > Copy Request Headers**:

```bash
POST /search.php HTTP/1.1
Host: server_ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:97.0) Gecko/20100101 Firefox/97.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://server_ip/index.php
Content-Type: application/json
Origin: http://server_ip
Content-Length: 19
DNT: 1
Connection: keep-alive
Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1
```

De hecho, tenemos `Content-Type: application/json`. Intentemos replicar esta solicitud como lo hicimos anteriormente, pero **incluyendo los encabezados de cookies y de tipo de contenido**, y enviemos nuestra solicitud a `search.php`:

```bash
curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php
```

Respuesta:

```
["London (UK)"]
```

Como podemos ver, pudimos interactuar con la función de búsqueda directamente sin necesidad de iniciar sesión ni interactuar con la interfaz de la aplicación web. Esta puede ser una habilidad esencial al realizar evaluaciones de aplicaciones web o ejercicios de recompensas por errores, ya que es mucho más rápido probar aplicaciones web de esta manera.

> **Ejercicio:** Intente repetir la solicitud anterior **sin** agregar los encabezados de cookies o de tipo de contenido y vea cómo la aplicación web actuaría de manera diferente.

Finalmente, intentemos repetir la misma solicitud anterior usando **Fetch**, como hicimos en la sección anterior. Podemos hacer clic derecho en la solicitud y seleccionar **Copy > Copy as Fetch**, y luego ir a la **Console** y ejecutar nuestro código allí. La respuesta JSON debe contener `London (UK)` (o resultados equivalentes según el término buscado).

---

### Resumen rápido

- **POST** envía datos en el cuerpo (ideal para archivos, JSON y grandes cargas).
- Usa `curl -X POST -d 'k=v' URL` para formularios y `-H 'Content-Type: application/json' -d '{...}'` para JSON.
- **Autenticación:** guarda la sesión con cookies (`Set-Cookie` → `-b 'name=value'`).
- **DevTools:** Pestañas **Network** y **Storage** son tus mejores amigas para espiar solicitudes/respuestas y cookies.

