# Interceptación de solicitudes web

Ahora que hemos configurado nuestro proxy, podemos usarlo para interceptar y manipular varias solicitudes HTTP enviadas por la aplicación web que estamos probando. Comenzaremos aprendiendo cómo interceptar solicitudes web, cambiarlas y luego enviarlas a su destino previsto.

---

## Solicitudes de interceptación

### Burp
En Burp, podemos navegar hasta la pestaña **Proxy** y la interceptación de solicitudes debe estar activada por defecto. Para activar o desactivar la interceptación, ir a la subpestaña **Intercept** y hacer clic en **Intercept is on/off**.

Una vez activada la interceptación, iniciar el navegador preconfigurado y visitar el sitio web objetivo. En Burp veremos la solicitud interceptada esperando nuestra acción y podremos hacer clic en **Forward** para reenviarla.

> Nota: Como todo el tráfico del navegador será interceptado, es posible ver múltiples solicitudes; haga clic en *Forward* hasta que reciba la solicitud dirigida a la IP objetivo.

### ZAP
En ZAP, la interceptación está desactivada por defecto (botón verde en la barra superior). Haga clic en el botón o use `CTRL+B` para activarla/desactivarla.

Inicie el navegador preconfigurado y visite el ejercicio. La solicitud interceptada aparecerá en el panel superior derecho; use el botón **Step** (paso) para reenviarla paso a paso o **Continue** para dejar pasar las solicitudes restantes.

ZAP incluye una característica HUD (Heads Up Display) que permite controlar funciones desde dentro del navegador preconfigurado. El HUD tiene un botón para activar interceptación y presenta la solicitud con opciones **Step**, **Continue** y **Drop**.

> Nota: En algunas versiones de navegadores, el HUD puede no funcionar correctamente. Si es la primera vez que usa el navegador preconfigurado, el HUD suele mostrar un tutorial que puede seguir.

---

## Manipulación de solicitudes interceptadas

Una vez interceptada, la solicitud quedará a la espera hasta que la reenviemos. Podemos examinarla, modificarla y enviarla a su destino. Esto nos permite ver qué información envía la aplicación y cómo responde al cambiarla.

Usos comunes de la manipulación de solicitudes:
- Inyecciones SQL
- Inyecciones de comandos
- Bypass de subida de ficheros
- Omisión de autenticación
- XSS
- XXE
- Manejo de errores
- Deserialización
- Otras vulnerabilidades web

### Ejemplo práctico

Activar la interceptación, configurar el campo `ip` en la página de prueba y pulsar **Ping**. La solicitud interceptada puede verse así:

```http
POST /ping HTTP/1.1
Host: 94.237.62.138:32306
Content-Length: 4
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://94.237.62.138:32306
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://94.237.62.138:32306/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

ip=1
```

Normalmente, la entrada `ip` solo acepta números en el navegador por validación front-end. Pero con interceptación podemos modificar la petición para enviar otros valores, por ejemplo:

```
ip=;ls;
```

Tras reenviar la petición modificada, si el servidor no valida correctamente en el backend, podemos obtener salida de comandos (ejemplo teórico):

```
flag.txt
index.html
node_modules
package-lock.json
public
server.js
```

Esto demuestra cómo la interceptación y manipulación de solicitudes ayuda a encontrar y explotar vulnerabilidades en aplicaciones web.

---

## Buenas prácticas al interceptar

- No dañe servicios de terceros; realice pruebas solo en entornos autorizados.
- Registre los cambios y respuestas para reproducir hallazgos.
- Use `Drop` o `Forward` con cuidado para no interrumpir flujos críticos.
- Aplique pruebas incrementales (usar `Step`/`Continue`) para entender cada interacción.
- Combine la manipulación con otras técnicas (fuzzing, escaneo, replay) para detectar fallos.

---

## Resumen

- Configurar un proxy (Burp/ZAP) permite capturar y manipular tráfico HTTP/HTTPS.
- Burp y ZAP tienen navegadores preconfigurados y opciones para habilitar interceptación.
- La interceptación facilita pruebas manuales para una amplia gama de vulnerabilidades web.
- Siempre valide en el backend; la validación únicamente front-end no es suficiente.
- Realice pruebas solo en objetivos autorizados y documente resultados y pasos.
