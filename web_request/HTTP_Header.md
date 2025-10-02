# Encabezados HTTP

Hemos visto ejemplos de solicitudes HTTP y encabezados de respuesta en la sección anterior. Estos encabezados HTTP pasan información entre el cliente y el servidor. Algunos encabezados solo se utilizan con solicitudes o respuestas, mientras que otros encabezados generales son comunes a ambos.

Los encabezados pueden tener uno o varios valores, adjuntos después del nombre del encabezado y separados por dos puntos. Podemos dividir los encabezados en las siguientes categorías:

- **General Headers**
- **Entity Headers**
- **Request Headers**
- **Response Headers**
- **Security Headers**

Analicemos cada una de estas categorías.

---

## Encabezados generales

**Encabezados generales** se utilizan tanto en solicitudes como en respuestas HTTP. Son contextuales y están acostumbrados a *describe the message rather than its contents*.

| Encabezado | Ejemplo | Descripción |
|---|---|---|
| `Date` | `Date: Wed, 16 Feb 2022 10:38:44 GMT` | Contiene la fecha y hora en que se originó el mensaje. Se prefiere convertir el tiempo al estándar **UTC**. |
| `Connection` | `Connection: close` | Dicta si la conexión de red actual debe permanecer activa una vez finalizada la solicitud. Valores comunes: `close` y `keep-alive`. `close` indica cerrar la conexión; `keep-alive` mantenerla abierta. |

---

## Encabezados de entidad

Similar a los generales, los **Encabezados de entidad** pueden ser *common to both the request and response*. Describen el **contenido (entidad)** transferido por un mensaje. Generalmente se encuentran en respuestas y solicitudes **POST** o **PUT**.

| Encabezado | Ejemplo | Descripción |
|---|---|---|
| `Content-Type` | `Content-Type: text/html` | Describe el tipo de recurso transferido. Los navegadores lo añaden automáticamente. `charset` indica la codificación (p. ej. `UTF-8`). |
| `Media-Type` | `Media-Type: application/pdf` | Similar a `Content-Type`; describe los datos transferidos. También puede incluir `charset`. |
| `boundary` | `boundary="b4e4fbd93540"` | Marcador para separar partes cuando hay más de un contenido en el mismo mensaje (`--b4e4fbd93540`). |
| `Content-Length` | `Content-Length: 385` | Tamaño de la entidad que se transfiere. Necesario para que el servidor lea el cuerpo. |
| `Content-Encoding` | `Content-Encoding: gzip` | Transformaciones aplicadas a los datos (p. ej. compresión). |

---

## Solicitar encabezados (Request Headers)

El cliente envía **Request Headers** en una transacción HTTP. Son *used in an HTTP request and do not relate to the content* del mensaje.

| Encabezado | Ejemplo | Descripción |
|---|---|---|
| `Host` | `Host: www.inlanefreight.com` | Especifica el host consultado (nombre de dominio o IP). Clave para virtual hosting; útil en enumeración. |
| `User-Agent` | `User-Agent: curl/7.77.0` | Describe el cliente que solicita recursos (navegador, versión, SO). |
| `Referer` | `Referer: http://www.inlanefreight.com/` | Indica el origen de la solicitud actual (p. ej. desde Google). Puede manipularse. |
| `Accept` | `Accept: */*` | Tipos de medios que entiende el cliente. `*/*` = cualquiera. |
| `Cookie` | `Cookie: PHPSESSID=b4e4fbd93540` | Pares `name=value` almacenados en cliente/servidor; mantienen sesión/preferencias. Varias cookies separadas por `;`. |
| `Authorization` | `Authorization: BASIC cGFzc3dvcmQK` | Método para identificar al cliente (Basic/Bearer, etc.). Tras autenticación, el servidor puede devolver un token. |

> Se puede encontrar una lista completa de encabezados de solicitud y su uso en la documentación estándar.

---

## Encabezados de respuesta (Response Headers)

**Encabezados de respuesta** se usan en respuestas HTTP y *do not relate to the content*. Proporcionan contexto adicional como edad del recurso, ubicación o servidor.

| Encabezado | Ejemplo | Descripción |
|---|---|---|
| `Server` | `Server: Apache/2.2.14 (Win32)` | Información del servidor HTTP que procesó la solicitud (versión, plataforma). |
| `Set-Cookie` | `Set-Cookie: PHPSESSID=b4e4fbd93540` | Cookies para identificación del cliente; el navegador las almacena. Formato similar a `Cookie`. |
| `WWW-Authenticate` | `WWW-Authenticate: BASIC realm="localhost"` | Indica el esquema de autenticación requerido para acceder al recurso. |

---

## Encabezados de seguridad (Security Headers)

Con la variedad de navegadores y ataques web, se definen **Security Headers** (encabezados de respuesta) para dictar políticas al navegador.

| Encabezado | Ejemplo | Descripción |
|---|---|---|
| `Content-Security-Policy` | `Content-Security-Policy: script-src 'self'` | Restringe orígenes de recursos (p. ej. scripts) para prevenir XSS. |
| `Strict-Transport-Security` | `Strict-Transport-Security: max-age=31536000` | Obliga HTTPS y evita degradación a HTTP. |
| `Referrer-Policy` | `Referrer-Policy: origin` | Controla si y cómo se envía el encabezado `Referer`. |

> **Nota:** Esto es un subconjunto común. Existen muchos otros encabezados y pueden definirse personalizados según requisitos. Consulte la especificación HTTP para una lista completa.

---

## cURL

En la sección anterior, vimos cómo usar `-v` con **cURL** para ver detalles completos de solicitud y respuesta.
- Si solo queremos **encabezados de respuesta**, usamos `-I` para enviar `HEAD` y mostrar solo encabezados.
- Si queremos **encabezados y cuerpo**, usamos `-i`.  
Diferencia: `-I` **envía HEAD**; `-i` **envía el método indicado** pero imprime encabezados también.

### Ejemplo con `-I`

```bash
curl -I https://www.inlanefreight.com
```

**Salida de ejemplo (abreviada):**
```
Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/605.1.15 (KHTML, like Gecko)
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

### Establecer encabezados con cURL

Además de ver encabezados, cURL permite **configurar encabezados de solicitud** con `-H`. Algunos encabezados tienen banderas específicas:

- `-A` → `User-Agent`
- `-b`/`--cookie` → `Cookie`
- `-H` → cualquier encabezado arbitrario

**Ejemplos:**

```bash
# Cambiar el User-Agent
curl https://www.inlanefreight.com -A 'Mozilla/5.0'
```

```bash
# Enviar cookies
curl https://www.inlanefreight.com -b 'cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4'
```

```bash
# Añadir encabezado arbitrario (p. ej., Authorization: Bearer ...)
curl https://www.inlanefreight.com -H 'Authorization: Bearer eyJhbGciOi...'
```

```bash
# Ver encabezados + cuerpo (GET por defecto)
curl -i https://www.inlanefreight.com
```

```bash
# Ver solo encabezados (HEAD)
curl -I https://www.inlanefreight.com
```

```bash
# Modo detallado (verbose)
curl -v https://www.inlanefreight.com
```

> **Ejercicio:** Revisa todos los encabezados anteriores e intenta recordar el uso de cada uno.  
> **Ejercicio:** Usa `-I` o `-v` junto al ejemplo de `-A` para verificar el cambio del `User-Agent`.

---

## Herramientas de desarrollo del navegador

Abre **DevTools** (Chrome/Firefox) con `CTRL+SHIFT+I` o `F12` y ve a **Network**:
- Selecciona una solicitud para ver **Request Headers** y **Response Headers**.
- Clic en **Raw** para verlos sin procesar.
- Revisa **Cookies** para ver las cookies usadas por la solicitud.

*Ejemplo observado*: pestaña Network mostrando dos solicitudes `GET` a `188.166.146.97:31122` con estado `304` para `/` (encabezados mostrados) y `404` para `favicon.ico`.
