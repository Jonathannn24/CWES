# Codificación / Decodificación

Al manipular solicitudes HTTP personalizadas es frecuente necesitar codificar o decodificar datos para que el servidor los interprete correctamente. Burp y ZAP incluyen herramientas integradas para esto.

---

## Tipos comunes de codificación
- **URL encoding** (percent-encoding): necesario para espacios, `&`, `#`, etc.
- **Base64**
- **HTML**
- **Unicode**
- **Hex / ASCII**

---

## URL encoding
- Espacios → `%20` o `+`
- `&` delimita parámetros
- `#` identifica fragmentos
- En **Burp Repeater**: selecciona el texto → clic derecho → `Convert Selection > URL > URL-encode key characters` o `Ctrl+U`.
- **ZAP** normalmente codifica automáticamente antes de enviar; en cualquier caso revisa el cuerpo enviado.

---

## Decodificación
- **Burp**: pestaña **Decoder** → pega la cadena → `Decode as > Base64` (u otro).
- **ZAP**: `Encoder/Decoder/Hash` (Ctrl+E) → pestaña **Decode**; puede intentar varios decodificadores automáticamente.

**Ejemplo (Base64)**  
Cadena: `eyJ1c2VybmFtZSI6Imd1ZXN0IiwgImlzX2FkbWluIjpmYWxzZX0=`  
Decodificado: `{"username":"guest", "is_admin":false}`

---

## Codificar para pruebas
- Si quieres probar manipular una cookie en Base64:
  1. Decodifica la cookie.
  2. Modifica el JSON (ej. `"username":"admin","is_admin":true`).
  3. Vuelve a codificar a Base64.
  4. Sustituye la cookie en la solicitud (header `Cookie:` o en almacenamiento del navegador).

**Ejemplo (Python, para referencia rápida):**
```python
import base64, json
s = 'eyJ1c2VybmFtZSI6Imd1ZXN0IiwgImlzX2FkbWluIjpmYWxzZX0='
obj = json.loads(base64.b64decode(s).decode())
obj['username'] = 'admin'
obj['is_admin'] = True
print(base64.b64encode(json.dumps(obj).encode()).decode())
```

---

## Herramientas en Burp y ZAP
- **Burp**
  - `Proxy`, `Repeater`, `Intruder` y `Decoder`.
  - `Decoder` permite múltiples formatos y encadenar codificaciones.
  - `Inspector` puede ayudar a ver y decodificar valores inline.
- **ZAP**
  - `Encoder/Decoder/Hash` (Ctrl+E).  
  - Permite añadir pestañas personalizadas y aplicar varios decodificadores automáticamente.

---

## Consejos prácticos
- Comprueba siempre `Content-Type` y si el servidor espera JSON (`application/json`) u otro formato.
- Cuando modifiques cookies, considera atributos como `HttpOnly` y `SameSite` (no accesibles desde JS si `HttpOnly`).
- Ten cuidado: manipular cookies o tokens para escalar privilegios puede ser ilegal fuera de un entorno de prueba autorizado.
- Automatiza transformaciones repetitivas con scripts (Python, jq, base64) para agilizar pruebas.

---

### Ejercicio sugerido
1. Intercepta una cookie Base64 con Burp/ZAP.
2. Decodíficala en Burp Decoder o ZAP.
3. Modifica el JSON (activa `is_admin`).
4. Re-codifica y sustituye en la petición.
5. Observa la respuesta del servidor (autentificado con diferentes privilegios).

---
