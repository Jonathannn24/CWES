# API CRUD

## 📌 Resumen rápido
Las API CRUD permiten **Crear, Leer, Actualizar y Eliminar** (Create, Read, Update, Delete) recursos de una base de datos a través de métodos HTTP (POST, GET, PUT, DELETE).  
Las operaciones suelen devolver datos en **JSON** y se pueden probar fácilmente con `cURL`.

| Operación | Método HTTP | Ejemplo |
|-----------|-------------|---------|
| Create    | POST        | `curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` |
| Read      | GET         | `curl http://<SERVER_IP>:<PORT>/api.php/city/london` |
| Update    | PUT         | `curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` |
| Delete    | DELETE      | `curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City` |

---

## 🔹 Leer (Read)

```bash
curl http://<SERVER_IP>:<PORT>/api.php/city/london
```

Con formato JSON:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
```

Buscar coincidencias parciales:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/le | jq
```

Obtener todas las entradas:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/ | jq
```

---

## 🔹 Crear (Create)

```bash
curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```

Verificar creación:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq
```

---

## 🔹 Actualizar (Update - PUT)

```bash
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```

Confirmar cambio:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
```

---

## 🔹 Eliminar (Delete)

```bash
curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```

Confirmar eliminación:

```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq
```

---

## 📖 Notas

- Algunas APIs permiten **PATCH** para actualizaciones parciales.  
- También se puede usar `OPTIONS` para comprobar qué métodos están habilitados.  
- En aplicaciones reales, estas operaciones suelen requerir autenticación (cookies, JWT, etc.).  

