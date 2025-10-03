# HTTP POST - Resumen y Ejemplos

## 📌 Resumen (TL;DR)
- **POST** envía parámetros en el **cuerpo de la solicitud**, no en la URL.  
- **Ventajas:** no se loguea en URL, acepta binarios, permite más datos.  
- **Uso típico:** formularios de login, carga de archivos, APIs con JSON.  
- **cURL:** `-X POST`, `-d` para datos, `-H` para encabezados, `-b` para cookies.  
- **Cookies:** autenticación persistente con `Set-Cookie` y `-b` en cURL.  
- **JSON:** usar `Content-Type: application/json`.  
- **Redirecciones:** usar `-L` en cURL.  

---

## Formularios de inicio de sesión

Ejemplo básico con **cURL**:

```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
```

- `-X POST` → define método POST.  
- `-d` → incluye datos en el cuerpo.  
- Tras login exitoso, se accede a la función de búsqueda.  

Seguir redirecciones si aplica:

```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -L
```

---

## Cookies autenticadas

Al autenticarse, el servidor devuelve una **cookie de sesión**:

```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i
```

Respuesta incluye:

```
Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/
```

Usar la cookie en nuevas solicitudes:

```bash
curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```

O como encabezado:

```bash
curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```

---

## Datos en formato JSON

El formulario de búsqueda envía JSON al backend. Ejemplo:

```json
{"search":"london"}
```

Solicitud equivalente con **cURL**:

```bash
curl -X POST -d '{"search":"london"}' \
     -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' \
     -H 'Content-Type: application/json' \
     http://<SERVER_IP>:<PORT>/search.php
```

Respuesta:

```json
["London (UK)"]
```

---

## Uso con Fetch en navegador

Ejemplo de cómo copiar como **Fetch** en DevTools y ejecutarlo en la consola:

```javascript
fetch("http://<SERVER_IP>:<PORT>/search.php", {
  "headers": {
    "Content-Type": "application/json",
    "Cookie": "PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1"
  },
  "body": "{"search":"London"}",
  "method": "POST"
});
```

---

## 🔑 Puntos Clave
- **POST** permite datos más complejos y seguros que GET.  
- **Cookies** = autenticación persistente.  
- **Content-Type** correcto es esencial (`application/json` para JSON).  
- Con cURL se puede reproducir y automatizar pruebas de aplicaciones web.  


