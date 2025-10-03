# Encabezados HTTP

Hemos visto ejemplos de solicitudes HTTP y encabezados de respuesta en la sección anterior. Estos encabezados HTTP pasan información entre el cliente y el servidor. Algunos encabezados solo se utilizan con solicitudes o respuestas, mientras que otros encabezados generales son comunes a ambos.

Los encabezados pueden tener uno o varios valores, adjuntos después del nombre del encabezado y separados por dos puntos. Podemos dividir los encabezados en las siguientes categorías:

- General Headers
- Entity Headers
- Request Headers
- Response Headers
- Security Headers

---

## Encabezados generales

Encabezados generales se utilizan tanto en solicitudes como en respuestas HTTP. Son contextuales y están acostumbrados a describir el **mensaje** más que su contenido.

| Encabezado | Ejemplo | Descripción |
|------------|---------|-------------|
| Date | Date: Wed, 16 Feb 2022 10:38:44 GMT | Contiene la fecha y hora en que se originó el mensaje. Se prefiere convertir el tiempo al estándar UTC. |
| Connection | Connection: close | Dicta si la conexión de red actual debe permanecer activa una vez finalizada la solicitud (`close` / `keep-alive`). |

---

## Encabezados de entidad

Estos encabezados describen el **contenido (entidad)** transferido. Generalmente en respuestas y solicitudes `POST` o `PUT`.

| Encabezado | Ejemplo | Descripción |
|------------|---------|-------------|
| Content-Type | Content-Type: text/html | Tipo de recurso transferido. Incluye `charset` (ej: UTF-8). |
| Media-Type | Media-Type: application/pdf | Similar a `Content-Type`. Describe los datos transferidos. |
| Boundary | boundary="b4e4fbd93540" | Marcador para separar contenido cuando hay más de uno en un mensaje. |
| Content-Length | Content-Length: 385 | Tamaño de la entidad transferida. Necesario para que el servidor lea los datos. |
| Content-Encoding | Content-Encoding: gzip | Transformaciones aplicadas (ej: compresión). |

---

## Encabezados de solicitud

Enviados por el cliente en una transacción HTTP.

| Encabezado | Ejemplo | Descripción |
|------------|---------|-------------|
| Host | Host: www.inlanefreight.com | Especifica el host consultado (dominio o IP). |
| User-Agent | User-Agent: curl/7.77.0 | Describe el cliente solicitando recursos. |
| Referer | Referer: http://www.inlanefreight.com/ | Indica de dónde proviene la solicitud. |
| Accept | Accept: */* | Describe qué tipos de medios puede aceptar el cliente. |
| Cookie | Cookie: PHPSESSID=b4e4fbd93540 | Contiene cookies en formato `name=value`. |
| Authorization | Authorization: BASIC cGFzc3dvcmQK | Método de identificación del cliente mediante token. |

---

## Encabezados de respuesta

Usados en respuestas HTTP para dar contexto adicional.

| Encabezado | Ejemplo | Descripción |
|------------|---------|-------------|
| Server | Server: Apache/2.2.14 (Win32) | Información sobre el servidor HTTP que procesó la solicitud. |
| Set-Cookie | Set-Cookie: PHPSESSID=b4e4fbd93540 | Cookies necesarias para la identificación del cliente. |
| WWW-Authenticate | WWW-Authenticate: BASIC realm="localhost" | Tipo de autenticación requerida para acceder al recurso. |

---

## Encabezados de seguridad

Cabeceras diseñadas para mejorar la seguridad en navegadores.

| Encabezado | Ejemplo | Descripción |
|------------|---------|-------------|
| Content-Security-Policy | Content-Security-Policy: script-src 'self' | Dicta la política contra recursos externos (previene XSS). |
| Strict-Transport-Security | Strict-Transport-Security: max-age=31536000 | Obliga al navegador a usar HTTPS. |
| Referrer-Policy | Referrer-Policy: origin | Controla si se envía el valor de `Referer`. |

---

## Uso de cURL

### Ver solo encabezados de respuesta:
```bash
curl -I https://www.inlanefreight.com
```

Salida de ejemplo:
```
Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5)
Cookie: cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4
Accept: text/plain
Referer: https://www.inlanefreight.com/
Authorization: BASIC cGFzc3dvcmQK

Date: Sun, 06 Aug 2020 08:49:37 GMT
Connection: keep-alive
Content-Length: 26012
Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: gzip
Server: Apache/2.2.14 (Win32)
Set-Cookie: name1=value1,name2=value2; Expires=Wed, 09 Jun 2021 10:18:14 GMT
WWW-Authenticate: BASIC realm="localhost"
Content-Security-Policy: script-src 'self'
Strict-Transport-Security: max-age=31536000
Referrer-Policy: origin
```

### Cambiar el User-Agent:
```bash
curl https://www.inlanefreight.com -A 'Mozilla/5.0'
```

Ejercicio: Intente usar `-I` o `-v` junto con `-A` para confirmar el cambio de User-Agent.

---

## Herramientas de desarrollo del navegador

- Abrir con **CTRL+SHIFT+I** o **F12** en Chrome/Firefox.  
- Pestaña **Network** → ver solicitudes y respuestas.  
- Sub-pestaña **Headers** → muestra encabezados organizados.  
- Sub-pestaña **Cookies** → ver cookies asociadas.  
- Opción **Raw** → ver encabezados en formato sin procesar.
