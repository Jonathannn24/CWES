# Modificación automática (Match & Replace) — Resumen y comandos

## Objetivo
Automatizar cambios en solicitudes y respuestas HTTP usando reglas **match & replace** en Burp Suite y **Replacer** en ZAP para:
- Modificar encabezados (ej. User-Agent).
- Transformar el body de respuestas (ej. cambiar `type="number"` por `type="text"`).
- Aplicar reemplazos persistentes sin interceptar manualmente.

---

## Burp Suite — Match & Replace
Ruta: `Proxy > Options > Match and Replace` (o `Proxy > Proxy settings > HTTP match and replace rules` en algunas versiones).

### Ejemplo 1 — Reemplazar User-Agent (Request header)
- **Type:** Request header  
- **Match (regex):** `^User-Agent.*$`  
- **Replace:** `User-Agent: HackTheBox Agent 1.0`  
- **Regex match:** true

> Esta regla sustituye cualquier `User-Agent` que envíe el navegador por `HackTheBox Agent 1.0`.

### Ejemplo 2 — Cambiar tipo de input en respuestas (Response body)
- **Type:** Response body  
- **Match:** `type="number"`  
- **Replace:** `type="text"`  
- **Regex match:** false

### Ejemplo 3 — Ajustar maxlength
- **Type:** Response body  
- **Match:** `maxlength="3"`  
- **Replace:** `maxlength="100"`  
- **Regex match:** false

> Tras aplicar estas reglas, recargar la página (`Ctrl+Shift+R`) mostrará el formulario ya modificado y persistente.

---

## ZAP — Replacer
Acceso: `CTRL+R` o `Tools > Options > Replacer`.

### Configuración equivalente en ZAP
- **Description:** HTB User-Agent  
- **Match Type:** Request Header (will add if not present)  
- **Match String:** `User-Agent`  
- **Replacement String:** `HackTheBox Agent 1.0`  
- **Enable:** true

Opcional: usar expresión regular con *Request Header String* si se requiere patrón.

**Initiators:** permite limitar dónde aplicar la regla (por defecto: *Apply to all HTTP(S) messages*).

---

## Ejemplos prácticos con cURL (comprobar efectos)
> Tras aplicar reglas, revisar solicitudes/respuestas desde una terminal ayuda a comprobar cambios.

Mostrar headers enviados (HEAD request):
```bash
curl -I https://example.com
```

Enviar POST con cuerpo JSON (ejemplo de prueba):
```bash
curl -X POST https://example.com/api -H 'Content-Type: application/json' -d '{"search":"london"}'
```

---

## Ejercicios recomendados
1. **Burp:** Añade la regla `User-Agent` y visita `https://httpbin.org/headers` con el navegador proxy; comprueba que el user-agent aparece como `HackTheBox Agent 1.0`.
2. **ZAP:** Crea la misma regla en Replacer y repite la comprobación anterior usando el navegador preconfigurado de ZAP.
3. **Persistencia de inputs:** Crea reglas en Burp para reemplazar `type="number"` → `type="text"` y `maxlength="3"` → `maxlength="100"`. Recarga la página objetivo y prueba enviar una carga útil larga (por ejemplo `;ls;`) en el campo modificado.
4. **Request body replace:** (Avanzado) añadir una regla que inserte `;ls;` en el body de la petición `POST /ping` (match por ruta o por pattern y replace del body).

---

## Buenas prácticas y precauciones
- Estas reglas modifican tráfico en tránsito: úsalo sólo en entornos de prueba o con autorización.
- Ten cuidado con reemplazos globales (riesgo de romper otros endpoints). Limita por host/path si es posible.
- Revisa con `Proxy History` (Burp) o `History` (ZAP) los mensajes afectados para validar impactos.
- Al modificar **Response body** con cambios en longitud, asegúrate de que `Content-Length` o compresión no invaliden la respuesta (Burp suele actualizar `Content-Length` si se habilita la opción correspondiente).

---

## Notas rápidas
- Burp permite reglas muy potentes con regex; ZAP tiene una interfaz más simple pero equivalente.
- Para cambios dinámicos en el navegador (mostrar campos ocultos, habilitar inputs), ZAP HUD y Burp response rules pueden ayudar sin interceptar manualmente.
- Combina reglas automáticas con interceptación selectiva cuando necesites controlar casos puntuales.
