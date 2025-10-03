# Métodos y Códigos HTTP (Resumen)

## Métodos HTTP más usados
- **GET** → Solicita un recurso específico (parámetros en URL).
- **POST** → Envía datos al servidor (formularios, archivos).
- **HEAD** → Solo devuelve encabezados (sin cuerpo).
- **PUT** → Crea/reemplaza recursos en el servidor.
- **DELETE** → Elimina un recurso existente.
- **OPTIONS** → Lista métodos soportados por el servidor.
- **PATCH** → Modificaciones parciales en un recurso.

🔎 Nota: Web apps modernas → usan principalmente **GET** y **POST**.  
APIs REST → dependen mucho de **PUT** y **DELETE**.

---

## Clases de códigos HTTP
- **1xx** → Informativos (no afectan al flujo).
- **2xx** → Éxito.
- **3xx** → Redirecciones.
- **4xx** → Errores del cliente.
- **5xx** → Errores del servidor.

---

## Ejemplos comunes
- **200 OK** → Solicitud exitosa.
- **302 Found** → Redirección (ej. login exitoso → dashboard).
- **400 Bad Request** → Formato incorrecto en la solicitud.
- **403 Forbidden** → Acceso denegado.
- **404 Not Found** → Recurso inexistente.
- **500 Internal Server Error** → Falla en el servidor.

---

## cURL ejemplos útiles
```bash
# GET por defecto
curl -v http://inlanefreight.com

# Enviar datos con POST
curl -X POST -d "username=admin&password=1234" http://inlanefreight.com/login

# Solo encabezados con HEAD
curl -I http://inlanefreight.com

# PUT para subir recurso
curl -X PUT -d @archivo.txt http://inlanefreight.com/upload

# DELETE recurso
curl -X DELETE http://inlanefreight.com/recurso
