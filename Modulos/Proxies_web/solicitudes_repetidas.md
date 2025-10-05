# Solicitudes repetidas

En las secciones anteriores evitamos la validación de entrada para usar una entrada no numérica y lograr una **inyección de comandos** en el servidor remoto. Repetir este proceso manualmente (interceptar → editar → reenviar → comprobar) para cada comando es lento. Para tareas repetitivas podemos usar la **repetición de solicitudes** que simplifica este flujo.

---

## Historial de proxy

- **Burp:** `Proxy → HTTP history` muestra todas las solicitudes capturadas (método, URL, código, etc.).  
- **ZAP:** usa el panel **History** o el HUD (panel inferior).

Ambas herramientas permiten filtrar y ordenar el historial. Burp permite ver la *Original Request* y la *Edited Request* si se modificó la petición.

---

## Repetir solicitudes

### Burp (Repeater)
1. Localiza la solicitud en **Proxy → HTTP history**.
2. Selecciónala y presiona `Ctrl+R` para enviarla a **Repeater**.
3. En **Repeater**, edita el cuerpo o los encabezados y haz clic en **Send**.
4. Consejo: clic derecho → **Change Request Method** para alternar entre `GET`/`POST` sin reescribir la petición.

> Ejemplo: modificar `ip=1` a `ip=;ls;` y enviar. La respuesta mostrará la salida del comando.

### ZAP (Request Editor / HUD)
- **Interfaz principal:** clic derecho en la solicitud → **Open/Resend with Request Editor** y presiona **Send**.
- **HUD:** en el navegador preconfigurado, localiza la solicitud en el panel **History** y elige **Replay in Console** (respuesta en HUD) o **Replay in Browser** (ver en navegador).
- Puedes cambiar el método HTTP desde el desplegable **Method**.

---

## Por qué es útil
- Ejecutar múltiples payloads rápidamente sin interceptar cada vez.
- Facilita la enumeración y el análisis (p. ej., ejecutar varios comandos o probar inyecciones).
- Acelera pruebas de fuzzing manual y verificación de filtrado/back-end.

---

## Notas sobre codificación
- Fíjate si los datos están en `application/x-www-form-urlencoded`, JSON u otro formato. Ajusta el cuerpo conforme a la codificación requerida.
- Tras editar la petición en Repeater/Request Editor, **Send** ejecuta la misma petición como si la hubiera enviado el navegador.

---

## Resumen rápido (pasos)
1. Captura la solicitud objetivo en el historial del proxy.  
2. Mándala al Repeater (Burp) o Request Editor (ZAP).  
3. Edita la carga/encabezados.  
4. Presiona **Send** y revisa la respuesta.  
5. Repite con otras cargas útiles.

---

## Consejos adicionales
- Usa filtros del historial para ubicar la solicitud objetivo rápidamente.
- Guarda peticiones útiles para reusarlas en pruebas posteriores (Burp Project o exportación; ZAP session).
- Si la aplicación usa protección (CSRF, tokens), asegúrate de actualizar los tokens en la petición antes de reenviar.

---
