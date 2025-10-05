# Servidores web

Un **servidor web** es una aplicación que se ejecuta en el servidor back-end, que maneja todo el tráfico HTTP desde el navegador del lado del cliente, lo enruta a las páginas solicitadas y finalmente responde al navegador del lado del cliente. Los servidores web suelen ejecutarse en TCP puertos 80 o 443, y son responsables de conectar a los usuarios finales a varias partes de la aplicación web, además de manejar sus diversas respuestas.

## Flujo de trabajo

Un servidor web típico acepta solicitudes HTTP del lado del cliente y responde con diferentes respuestas y códigos HTTP, como un código **200 OK** respuesta a una solicitud exitosa, un código **404 NOT FOUND** al solicitar páginas que no existen, **403 FORBIDDEN** para solicitar acceso a páginas restringidas, etc.

Diagrama que muestra un servidor web que maneja solicitudes y respuestas de tres clientes: teléfono inteligente, computadora portátil y monitor.

Los siguientes son algunos de los más comunes Códigos de respuesta HTTP:

| Código | Descripción |
|---|---|
| **Respuestas exitosas** | |
| 200 OK | La solicitud ha tenido éxito |
| **Mensajes de redirección** | |
| 301 Moved Permanently | La URL del recurso solicitado ha sido cambiada permanentemente |
| 302 Found | La URL del recurso solicitado ha sido cambiada temporalmente |
| **Respuestas de error del cliente** | |
| 400 Bad Request | El servidor no pudo comprender la solicitud debido a una sintaxis no válida |
| 401 Unauthorized | Intento no autenticado de acceder a la página |
| 403 Forbidden | El cliente no tiene derechos de acceso al contenido |
| 404 Not Found | El servidor no puede encontrar el recurso solicitado |
| 405 Method Not Allowed | El servidor conoce el método de solicitud, pero está deshabilitado y no se puede utilizar |
| 408 Request Timeout | Esta respuesta es enviada en una conexión inactiva por algunos servidores, incluso sin ninguna solicitud previa por parte del cliente |
| **Respuestas de error del servidor** | |
| 500 Internal Server Error | El servidor se ha encontrado con una situación que no sabe cómo manejar |
| 502 Bad Gateway | El servidor, mientras trabajaba como puerta de enlace para obtener la respuesta necesaria para manejar la solicitud, recibió una respuesta no válida |
| 504 Gateway Timeout | El servidor actúa como puerta de enlace y no puede obtener una respuesta a tiempo |

Los servidores web también aceptan varios tipos de entradas de usuario dentro de las solicitudes HTTP, incluido texto JSON, e incluso datos binarios (es decir, para cargas de archivos). Una vez que un servidor web recibe una solicitud web, es responsable de enrutarla a su destino, ejecutar cualquier proceso necesario para esa solicitud y devolver la respuesta al usuario en el lado del cliente. Las páginas y archivos a los que el servidor web procesa y enruta el tráfico son los archivos principales de la aplicación web.

A continuación se muestra un ejemplo de solicitud de una página en una terminal Linux utilizando el `curl` utilidad y recibir la respuesta del servidor mientras se utiliza la `-I` bandera, que muestra los encabezados:

```bash
# Servidores web
JonaLF@htb[/htb]$ curl -I https://academy.hackthebox.com

HTTP/2 200
date: Tue, 15 Dec 2020 19:54:29 GMT
content-type: text/html; charset=UTF-8
...SNIP...
```

Mientras que este ejemplo de `curl` nos muestra el código fuente de la página web:

```bash
# Servidores web
JonaLF@htb[/htb]$ curl https://academy.hackthebox.com

<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>Cyber Security Training : HTB Academy</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Se pueden utilizar muchos tipos de servidores web para ejecutar aplicaciones web. La mayoría de ellos pueden gestionar todo tipo de solicitudes HTTP complejas y, por lo general, son gratuitos. Incluso podemos desarrollar nuestro propio servidor web básico utilizando lenguajes como Python, JavaScript, y PHP. Sin embargo, para cada idioma, existe una aplicación web popular que está optimizada para manejar grandes cantidades de tráfico web, lo que nos ahorra tiempo en la creación de nuestro propio servidor web.

## Apache

Apache ('o httpd') es el servidor web más común en Internet y aloja más de 40% de todos los sitios web de Internet. Apache generalmente viene preinstalado en la mayoría Linux distribuciones y también se pueden instalar en servidores Windows y macOS.

Apache se utiliza habitualmente con PHP para el desarrollo de aplicaciones web, pero también admite otros lenguajes como .Net, Python, Perl, e incluso lenguajes del sistema operativo como Bash a través de CGI. Los usuarios pueden instalar una amplia variedad de módulos de Apache para ampliar su funcionalidad y soportar más idiomas. Por ejemplo, para apoyar el servicio PHP archivos que los usuarios deben instalar PHP en el servidor back-end, además de instalar el `mod_php` módulo para Apache.

Apache es un proyecto de código abierto y los usuarios de la comunidad pueden acceder a su código fuente para solucionar problemas y buscar vulnerabilidades. Está bien mantenido y se repara periódicamente contra vulnerabilidades para mantenerlo seguro contra la explotación. Además, está muy bien documentado, lo que hace que utilizar y configurar diferentes partes del servidor web sea relativamente fácil. Apache es comúnmente utilizado por empresas emergentes y pequeñas, ya que es sencillo de desarrollar. Aún así, algunas grandes empresas utilizan Apache, entre ellas:

- Apple
- Adobe
- Baidu

## NGINX

NGINX es el segundo servidor web más común en Internet y aloja aproximadamente 30% de todos los sitios web de Internet. NGINX se centra en atender muchas solicitudes web simultáneas con una carga de memoria y CPU relativamente baja utilizando una arquitectura asíncrona para hacerlo. Esto hace NGINX un servidor web muy confiable para aplicaciones web populares y las principales empresas de todo el mundo, por lo que es el servidor web más popular entre los sitios web de alto tráfico, con alrededor del 60% de los 100.000 sitios web más utilizados NGINX.

NGINX también es gratuito y de código abierto, lo que ofrece los mismos beneficios mencionados anteriormente, como seguridad y confiabilidad. Algunos sitios web populares que utilizan NGINX incluyen:

- Google
- Facebook
- Twitter
- Cisco
- Intel
- Netflix
- HackTheBox

## IIS

IIS (Servicios de información de Internet) es el tercer servidor web más común en Internet y se aloja alrededor de 15% de todos los sitios web de Internet. IIS es desarrollado y mantenido por Microsoft y se ejecuta principalmente en servidores Microsoft Windows. IIS generalmente se utiliza para alojar aplicaciones web desarrolladas para Microsoft .NET framework, pero también se puede utilizar para alojar aplicaciones web desarrolladas en otros lenguajes como PHP, o alojar otros tipos de servicios como FTP. Además, IIS está muy bien optimizado para la integración de Active Directory e incluye funciones como Windows Auth para autenticar a los usuarios mediante Active Directory, permitiéndoles iniciar sesión automáticamente en aplicaciones web.

Aunque no es el servidor web más popular, muchas grandes organizaciones lo utilizan IIS como su servidor web. Muchos de ellos utilizan Windows Server en su back-end o dependen en gran medida de Active Directory dentro de su organización. Algunos sitios web populares que utilizan IIS incluyen:

- Microsoft
- Office365
- Skype
- Stack Overflow
- Dell

Además de estos 3 servidores web, existen muchos otros servidores web de uso común, como Apache Tomcat para aplicaciones Java, y Node.JS para aplicaciones web desarrolladas utilizando JavaScript en la parte trasera.
