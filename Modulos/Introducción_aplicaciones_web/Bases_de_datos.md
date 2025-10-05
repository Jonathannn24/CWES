# Bases de datos

Las aplicaciones web utilizan back-end bases de datos para almacenar diversos contenidos e información relacionada con la aplicación web. Estos pueden ser activos principales de aplicaciones web, como imágenes y archivos, contenido de aplicaciones web, como publicaciones y actualizaciones, o datos de usuario, como nombres de usuario y contraseñas. Esto permite que las aplicaciones web almacenen y recuperen datos de forma fácil y rápida y habiliten contenido dinámico que sea diferente para cada usuario.

Existen muchos tipos diferentes de bases de datos, cada una de las cuales se adapta a un determinado tipo de uso. La mayoría de los desarrolladores buscan ciertas características en una base de datos, como **velocidad** al almacenar y recuperar datos, **capacidad** al almacenar grandes cantidades de datos, **escalabilidad** a medida que la aplicación web crece, y **coste**.

---

## Relacional (SQL)

Las bases de datos relacionales (SQL) almacenan sus datos en tablas, filas y columnas. Cada tabla puede tener claves únicas, que pueden vincular tablas entre sí y crear relaciones entre tablas.

Por ejemplo, podemos tener una tabla `users` en una base de datos relacional que contiene columnas como `id`, `username`, `first_name`, `last_name`, y así sucesivamente. El `id` se puede utilizar como clave de tabla. Otra mesa, `posts`, puede contener publicaciones realizadas por todos los usuarios, con columnas como `id`, `user_id`, `date`, `content`, y así sucesivamente.

Podemos vincular el `id` desde la tabla `users` a la `user_id` en la tabla `posts` para recuperar fácilmente los detalles del usuario para cada publicación, sin tener que almacenar todos los detalles del usuario con cada publicación.

La relación entre tablas dentro de una base de datos se llama **esquema**.

### Ventajas
- Rápido y fiable para conjuntos de datos estructurados.
- Eficiente para consultas que combinan varias tablas.

### Ejemplos comunes
- MySQL
- MSSQL (Microsoft SQL Server)
- Oracle
- PostgreSQL
- Otros: SQLite, MariaDB, Amazon Aurora, Azure SQL

---

## No relacional (NoSQL)

Una base de datos no relacional no utiliza tablas, filas, columnas o esquemas estrictos. En cambio, un sistema NoSQL almacena datos según varios modelos (dependiendo del uso):

- **Clave-valor**
- **Basado en documentos**
- **Columna ancha**
- **Grafo**

Debido a la falta de estructura fija, las bases de datos NoSQL son muy escalables y flexibles, adecuadas para datos menos definidos.

### Ejemplo (Key-Value en JSON)
```json
{
  "100001": {
    "date": "01-01-2021",
    "content": "Welcome to this web application."
  },
  "100002": {
    "date": "02-01-2021",
    "content": "This is the first post on this web app."
  },
  "100003": {
    "date": "02-01-2021",
    "content": "Reminder: Tomorrow is the ..."
  }
}
```

### Ejemplos comunes
- MongoDB (Document-based)
- Elasticsearch (optimizado para búsqueda y análisis)
- Apache Cassandra (altamente escalable)
- Otros: Redis, Neo4j, CouchDB, Amazon DynamoDB

---

## Uso en aplicaciones web

La mayoría de los lenguajes y frameworks facilitan la integración con bases de datos. Primero la base de datos debe instalarse y configurarse en el servidor back-end y, una vez disponible, la aplicación puede almacenar y recuperar datos.

**Ejemplo básico (PHP + MySQL):**
```php
$conn = new mysqli("localhost", "user", "pass");
$sql = "CREATE DATABASE database1";
$conn->query($sql);

$conn = new mysqli("localhost", "user", "pass", "database1");
$query = "select * from table_1";
$result = $conn->query($query);

while($row = $result->fetch_assoc() ){
    echo $row["name"]."<br>";
}
```

**Ejemplo de uso de entrada de usuario en una consulta (¡peligroso si no se valida!):**
```php
$searchInput =  $_POST['findUser'];
$query = "select * from users where name like '%$searchInput%'";
$result = $conn->query($query);
```

> **Advertencia:** Si no se codifica de forma segura, el manejo de entradas puede provocar **inyección SQL** y otras vulnerabilidades.

---

## Recomendaciones de seguridad
- Validar y sanear todas las entradas del usuario antes de incorporarlas en consultas.
- Usar consultas preparadas / parámetros (`prepared statements`) para evitar inyección SQL.
- Restringir privilegios de las cuentas de base de datos (principio de mínimo privilegio).
- Encriptar datos sensibles en reposo y en tránsito.
- Auditar y monitorizar accesos y consultas inusuales.
- Hacer copias de seguridad periódicas y probar restauraciones.

---
