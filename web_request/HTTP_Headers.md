# Solicitudes y respuestas HTTP

Las comunicaciones HTTP consisten principalmente en una **solicitud HTTP** y una **respuesta HTTP**. El cliente realiza una solicitud HTTP (por ejemplo, cURL/navegador) y el servidor la procesa (por ejemplo, servidor web). Las solicitudes contienen todos los detalles que necesitamos del servidor, incluido el recurso (por ejemplo: URL, ruta, parámetros), cualquier dato de solicitud, encabezados u opciones que especifiquemos y muchas otras opciones que discutiremos a lo largo de este módulo.

Una vez que el servidor recibe la solicitud HTTP, la procesa y responde enviando la **respuesta HTTP**, que contiene el código de respuesta, como se analiza en una sección posterior, y puede contener los datos de recursos si el solicitante tiene acceso a ella.

---

## Solicitud HTTP

Comencemos examinando el siguiente ejemplo de solicitud HTTP:

**Detalles de la solicitud HTTP:**  
Método `GET`, ruta `/users/login.html`, versión `HTTP/1.1`.  
Encabezados: `Host: inlanefreight.com`, `User-Agent: Mozilla/5.0`, `Cookie: PHPSESSID=c4ggt4jull9obt7aupa55o8vbf`.

La imagen de arriba muestra una solicitud HTTP GET a la URL:

```
http://inlanefreight.com/users/login.html
```

La primera línea de cualquier solicitud HTTP contiene tres campos principales separados por espacios:

| Campo   | Ejemplo               | Descripción                                                                 |
|---------|------------------------|-----------------------------------------------------------------------------|
| Method  | `GET`                  | El método o verbo HTTP, que especifica el tipo de acción a realizar.       |
| Path    | `/users/login.html`    | La ruta al recurso al que se accede. Puede incluir query (p. ej.: `?username=user`). |
| Version | `HTTP/1.1`             | El tercer y último campo se utiliza para indicar la versión HTTP.          |

El siguiente conjunto de líneas contiene **pares de valores de encabezado HTTP**, como `Host`, `User-Agent`, `Cookie`, y muchos otros encabezados posibles. Estos encabezados se utilizan para especificar varios atributos de una solicitud. Los encabezados terminan con una nueva línea, que es necesaria para que el servidor valide la solicitud. Finalmente, una solicitud puede finalizar con el **cuerpo de la solicitud** y los datos.

> **Nota:** La versión **HTTP/1.X** envía solicitudes como texto claro y utiliza un carácter de nueva línea para separar diferentes campos y diferentes solicitudes. La versión **HTTP/2.X**, por otro lado, envía solicitudes como **datos binarios** en forma de diccionario.

---

## Respuesta HTTP

Una vez que el servidor procesa nuestra solicitud, envía su respuesta. El siguiente es un ejemplo de respuesta HTTP:

**Detalles de la respuesta HTTP:**  
Versión `HTTP/1.1`, estado `200 OK`.  
Encabezados: `Date`, `Server: Apache/2.4.41`, `Set-Cookie: PHPSESSID=m4u64rqlpfthrvvb12ai9voqgf`, `Content-Type: text/html; charset=UTF-8`.

La primera línea de una respuesta HTTP contiene dos campos separados por espacios. El primero es la **versión HTTP** (p. ej. `HTTP/1.1`), y el segundo denota el **código de respuesta HTTP** (p. ej. `200 OK`).

Los **códigos de respuesta** se utilizan para determinar el estado de la solicitud, como se analizará en una sección posterior. Después de la primera línea, la respuesta enumera sus **encabezados**, de forma similar a una solicitud HTTP. Tanto los encabezados de **solicitud** como los de **respuesta** se analizan en la siguiente sección.

Finalmente, la respuesta puede terminar con un **cuerpo de respuesta**, que está separado por una nueva línea después de los encabezados. El cuerpo de respuesta suele definirse como **HTML**. Sin embargo, también puede responder con otros tipos de contenido como **JSON**, recursos del sitio web como **imágenes**, **hojas de estilo** o **scripts**, o incluso un documento como un **PDF** alojado en el servidor web.

---

## cURL

En nuestros ejemplos anteriores con **cURL**, solo especificamos la URL y obtuvimos el cuerpo de la respuesta a cambio. Sin embargo, cURL también nos permite obtener una **vista previa de la solicitud HTTP completa y la respuesta HTTP completa**, lo que puede resultar muy útil al realizar pruebas de penetración web o escribir exploits. Para ver la solicitud y respuesta HTTP completa, simplemente podemos agregar la bandera detallada **`-v`** para nuestros comandos anteriores, y debería imprimir tanto la solicitud como la respuesta:

```bash
curl inlanefreight.com -v
```

Salida (resumen):

```
*   Trying SERVER_IP:80...
* TCP_NODELAY set
* Connected to inlanefreight.com (SERVER_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: inlanefreight.com
> User-Agent: curl/7.65.3
> Accept: */*
> Connection: close
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< WWW-Authenticate: Basic realm="Restricted Content"
< Content-Length: 464
< Content-Type: text/html; charset=iso-8859-1
<
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

Como podemos ver, esta vez obtenemos la **solicitud y respuesta HTTP completa**. La solicitud simplemente envió `GET / HTTP/1.1` junto con los encabezados `Host`, `User-Agent` y `Accept`. A cambio, la respuesta HTTP contenía el `HTTP/1.1 401 Unauthorized`, lo que indica que no tenemos acceso al recurso solicitado. De manera similar a la solicitud, la respuesta también contenía varios encabezados enviados por el servidor, incluidos `Date`, `Content-Length`, y `Content-Type`. Finalmente, la respuesta contenía el cuerpo de la respuesta en HTML, que es el mismo que recibimos anteriormente cuando usamos cURL sin la bandera `-v`.

> **Ejercicio:** La bandera `-vvv` muestra un resultado aún más detallado. Intenta utilizar esta bandera para ver qué detalles adicionales de solicitud y respuesta se muestran con ella.

---

## Herramientas de desarrollo del navegador

La mayoría de los navegadores web modernos vienen con **herramientas de desarrollo** integradas (**DevTools**), que están destinadas principalmente a que los desarrolladores prueben sus aplicaciones web. Sin embargo, como evaluadores de penetración web, estas herramientas pueden ser un **activo vital** en cualquier evaluación web que realicemos. En este módulo, también discutiremos cómo utilizar algunas de las herramientas básicas de desarrollo del navegador para evaluar y monitorear diferentes tipos de solicitudes web.

Cada vez que visitamos cualquier sitio web o accedemos a cualquier aplicación web, nuestro navegador envía **múltiples solicitudes web** y maneja múltiples **respuestas HTTP** para representar la vista final que vemos en la ventana del navegador. Para abrir las herramientas de desarrollo del navegador en **Chrome o Firefox**, podemos hacer clic en **`CTRL+SHIFT+I`** o simplemente en **`F12`**. Las herramientas de desarrollo contienen varias pestañas, cada una de las cuales tiene su propio uso. Nos centraremos principalmente en la pestaña **Network** (Red), ya que es responsable de las solicitudes web.

Si hacemos clic en la pestaña **Network/Red** y actualizamos la página, deberíamos poder ver la **lista de solicitudes** enviadas por la página (por ejemplo: dos solicitudes GET; estado `304` para `/` y `404` para `favicon.ico`).

Como podemos ver, las herramientas de desarrollo nos muestran de un vistazo el **estado de la respuesta** (código de respuesta), el **método de solicitud** utilizado (GET), el **recurso solicitado** (URL/dominio), junto con la **ruta** solicitada. Además, podemos utilizar **Filter URLs** para buscar una solicitud específica, en caso de que el sitio web cargue demasiadas para revisarlas.
