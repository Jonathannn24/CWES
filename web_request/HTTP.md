# Protocolo de Transferencia de Hipertexto (HTTP)

HTTP es un protocolo a nivel de aplicación usado para acceder a recursos en la web.  
Funciona con un **cliente** (ej. navegador) que envía solicitudes y un **servidor** que responde con los recursos.  
El puerto por defecto es **80** (HTTP) y **443** (HTTPS).

---

## Componentes de una URL

Ejemplo:  
```
http://admin:password@inlanefreight.com:80/dashboard.php?login=true#status
```

| Componente   | Ejemplo                   | Descripción |
|--------------|---------------------------|-------------|
| **Scheme**   | `http://` / `https://`    | Protocolo usado. |
| **User Info**| `admin:password@`         | Credenciales opcionales. |
| **Host**     | `inlanefreight.com`       | Nombre de dominio o IP. |
| **Port**     | `:80`                     | Puerto usado (por defecto 80/443). |
| **Path**     | `/dashboard.php`          | Recurso solicitado. |
| **Query**    | `?login=true`             | Parámetros enviados en la petición. |
| **Fragment** | `#status`                 | Procesado por el navegador (sección de página). |

---

## Flujo de una Solicitud HTTP

1. El cliente resuelve el dominio con **DNS**.
2. Envía una solicitud (ej. `GET /`) al servidor en el puerto 80.
3. El servidor responde con el recurso (`index.html`) y un **código de estado** (ej. `200 OK`).
4. El navegador interpreta el HTML/CSS/JS recibido.

🔹 Nota: Se puede modificar la resolución de dominios en `/etc/hosts`.

---

## Herramienta cURL

cURL permite enviar solicitudes web desde la terminal.

### Solicitud básica
```bash
curl inlanefreight.com
```
📌 Devuelve el contenido HTML de la página.

### Descargar archivo
```bash
curl -O inlanefreight.com/index.html
```
Guarda el archivo con su nombre original.

### Descargar archivo con nombre personalizado
```bash
curl -o salida.html inlanefreight.com/index.html
```

### Descargar en modo silencioso
```bash
curl -s -O inlanefreight.com/index.html
```

### Ayuda y opciones
```bash
curl -h
```

Opciones comunes:
- `-d` → Enviar datos (POST).
- `-i` → Incluir cabeceras de respuesta.
- `-u user:pass` → Autenticación básica.
- `-A "Agente"` → Definir User-Agent.
- `-v` → Modo verboso.

---

## Conclusión
HTTP es la base de la comunicación web.  
`cURL` es una herramienta esencial para pruebas de penetración y automatización, ya que permite interactuar con servidores sin necesidad de un navegador.
