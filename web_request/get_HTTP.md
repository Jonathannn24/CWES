# Método HTTP GET, Autenticación Básica y Parámetros GET

## Solicitud GET
Cada vez que visitamos cualquier URL, nuestros navegadores utilizan de forma predeterminada una solicitud **GET** para obtener los recursos remotos alojados en esa URL. Una vez que el navegador recibe la página inicial que solicita, puede enviar otras solicitudes utilizando varios métodos HTTP. Esto se puede observar a través de la pestaña **Red** en las herramientas de desarrollo del navegador.

**Ejercicio:** Elija cualquier sitio web de su elección y monitoree la pestaña Red en las herramientas de desarrollo del navegador mientras lo visita para comprender qué está funcionando la página.

---

## Autenticación básica HTTP
Este tipo de autenticación utiliza **Basic HTTP Authentication**, manejado directamente por el servidor web para proteger un recurso.

Credenciales de ejemplo: **admin:admin**

### Ejemplo con cURL
```bash
# Solicitud sin credenciales → 401 Unauthorized
curl -i http://<SERVER_IP>:<PORT>/

# Autenticación con -u
curl -u admin:admin http://<SERVER_IP>:<PORT>/

# Autenticación en la URL
curl http://admin:admin@<SERVER_IP>:<PORT>/
```

### Respuesta 401 no autenticada
```http
HTTP/1.1 401 Authorization Required
Date: Mon, 21 Feb 2022 13:11:46 GMT
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-cache, must-revalidate, max-age=0
WWW-Authenticate: Basic realm="Access denied"
Content-Length: 13
Content-Type: text/html; charset=UTF-8

Access denied
```

### Respuesta autenticada (con -u o en URL)
```html
<!DOCTYPE html>
<html lang="en">
<head>
...SNIP...
```

---

## Encabezado de autorización HTTP
Si usamos `-v` en cURL vemos el encabezado:

```bash
curl -v http://admin:admin@<SERVER_IP>:<PORT>/
```

Salida (extracto):
```http
> Authorization: Basic YWRtaW46YWRtaW4=
< HTTP/1.1 200 OK
```

El valor `YWRtaW46YWRtaW4=` es `admin:admin` en **Base64**.

### Configuración manual con -H
```bash
curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/
```

---

## Parámetros GET
Después de autenticarse, accedemos a la función **City Search**.

Ejemplo:  
`http://<SERVER_IP>:<PORT>/search.php?search=le`

### Ejemplo con cURL
```bash
curl 'http://<SERVER_IP>:<PORT>/search.php?search=le'   -H 'Authorization: Basic YWRtaW46YWRtaW4='
```

Respuesta:
```
Leeds (UK)
Leicester (UK)
```

### Ejemplo con Fetch (DevTools)
```javascript
fetch("http://127.0.0.1/search.php?search=le", {
  headers: { "Authorization": "Basic YWRtaW46YWRtaW4=" }
})
```

---

Con GET podemos:  
- Autenticarnos con **Basic Auth**.  
- Enviar parámetros en la URL (`?clave=valor`).  
- Replicar peticiones fácilmente con **cURL** o **Fetch API**.
