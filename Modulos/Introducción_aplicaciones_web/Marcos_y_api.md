# Marcos de desarrollo y API

## Marcos de desarrollo

Con la creciente complejidad de las aplicaciones web, los **marcos de desarrollo web** permiten crear aplicaciones robustas y seguras más rápidamente. Estos marcos proporcionan estructuras prediseñadas y funcionalidad común como autenticación, gestión de sesiones y manipulación de bases de datos.

### Ejemplos comunes

| Framework | Lenguaje | Uso común |
|------------|-----------|------------|
| **Laravel** | PHP | Ideal para startups y pequeñas empresas. Potente y sencillo. |
| **Express** | Node.js | Utilizado por PayPal, Yahoo, Uber e IBM. |
| **Django** | Python | Usado por Google, YouTube, Instagram, Mozilla, Pinterest. |
| **Ruby on Rails** | Ruby | Usado por GitHub, Airbnb, Hulu, Twitch, Twitter (en el pasado). |

> 🔸 Los sitios web populares suelen combinar varios frameworks y servidores web para distintas funciones.

---

## API (Application Programming Interface)

Una **API web** conecta el *frontend* con el *backend*, permitiendo que los datos viajen entre ambos. Las APIs procesan solicitudes, ejecutan funciones en el servidor y devuelven respuestas al navegador o aplicación cliente.

### Parámetros de consulta

Los parámetros de entrada se envían generalmente por los métodos **GET** o **POST**.

#### Ejemplo:

**GET request:**
```
/search.php?item=apples
```

**POST request:**
```http
POST /search.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded

item=apples
```

---

## Tipos de API

### SOAP (Simple Object Access Protocol)

SOAP utiliza **XML** para estructurar solicitudes y respuestas. Ideal para compartir datos complejos entre cliente y servidor.

**Ejemplo SOAP:**
```xml
<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://www.example.com/soap/soap/"
soap:encodingStyle="http://www.w3.org/soap/soap-encoding">
  <soap:Header></soap:Header>
  <soap:Body>
    <soap:Fault></soap:Fault>
  </soap:Body>
</soap:Envelope>
```

🔹 Ventajas:
- Intercambio estructurado de datos.
- Permite transferencia de objetos serializados y binarios.

🔹 Desventajas:
- Más complejo y pesado que REST.
- Requiere solicitudes más largas.

---

### REST (Representational State Transfer)

REST utiliza **HTTP estándar** y **JSON** o **XML** para la comunicación. Los datos se transmiten generalmente a través de rutas URL y son más livianos y fáciles de manejar.

**Ejemplo REST:**
```json
{
  "100001": {"date": "01-01-2021", "content": "Welcome to this web application."},
  "100002": {"date": "02-01-2021", "content": "This is the first post on this web app."},
  "100003": {"date": "02-01-2021", "content": "Reminder: Tomorrow is the ..."}
}
```

### Métodos HTTP usados en REST

| Método | Descripción |
|--------|--------------|
| **GET** | Recuperar datos |
| **POST** | Crear datos nuevos |
| **PUT** | Actualizar o reemplazar datos |
| **DELETE** | Eliminar datos existentes |

---

## Conclusión

Los frameworks y las API son esenciales para el desarrollo moderno de aplicaciones web.  
- Los **frameworks** aceleran el desarrollo y garantizan buenas prácticas.  
- Las **API** permiten comunicación eficiente y modular entre componentes.
