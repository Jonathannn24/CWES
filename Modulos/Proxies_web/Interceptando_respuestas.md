# Interceptando respuestas

En algunos casos, es posible interceptar las **respuestas HTTP** del servidor antes de que lleguen al navegador. Esto es útil para cambiar el aspecto o comportamiento de una página (activar campos deshabilitados, mostrar campos ocultos, etc.) y facilita tareas de pentesting.

---

## Objetivo
Modificar la respuesta del servidor para:
- Habilitar inputs deshabilitados (`disabled`)
- Cambiar atributos HTML (p. ej. `type="number"` → `type="text"`)
- Aumentar `maxlength`
- Mostrar campos ocultos o comentarios útiles

---

## Flujo general
1. Configurar proxy (Burp o ZAP) como interceptador.
2. Activar la interceptación de respuestas.
3. Realizar la acción en el navegador que genera la solicitud.
4. Cuando la respuesta sea interceptada, editar el HTML y reenviarla (Forward / Continue).
5. Ver en el navegador los cambios aplicados en la representación de la página.

---

## Ejemplo práctico (formulario "Ping")

Respuesta interceptada — fragmento HTML original:

```html
<input type="number" id="ip" name="ip" min="1" max="255" maxlength="3"
    oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
    required>
```

Editar a:

```html
<input type="text" id="ip" name="ip" min="1" max="255" maxlength="100"
    oninput="javascript: if (this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);"
    required>
```

Con esto el navegador aceptará entrada no numérica y más larga.

---

## Burp Suite

1. Ir a **Proxy → Proxy settings**.
2. En **Response interception rules**, habilitar `Intercept Response`.
3. Activar **Proxy → Intercept** (Intercept is on).
4. En el navegador (forzar refresh con `CTRL+SHIFT+R`) generar la solicitud.
5. Burp interceptará la respuesta; hacer `Forward` para ver la respuesta o editarla antes.
6. Para reglas automáticas de modificación: **Proxy → Proxy settings → Response modification rules** (p. ej. `Unhide hidden form fields`).
7. También se puede usar la opción para actualizar `Content-Length` automáticamente si se modifica el cuerpo.

---

## ZAP (OWASP ZAP)

1. Intercepción por HUD o desde la interfaz principal:
   - Activar la Intercepción (botón rojo/verde en la barra superior) o usar HUD.
2. En HUD: al interceptar, elegir **Step** para enviar la solicitud y capturar la respuesta.
3. Editar la respuesta y hacer **Continue** para reenviarla.
4. HUD dispone del botón **Show/Enable** (bombilla) que puede automáticamente mostrar/activar campos sin necesidad de interceptar.
5. También existe la opción de ver indicadores de comentarios HTML y mostrarlos desde el HUD.

---

## Consejos prácticos

- Si solo quieres habilitar campos deshabilitados u ocultos, intenta primero con las funciones HUD (ZAP) o reglas de respuesta (Burp) antes de editar manualmente.
- Ten en cuenta `Content-Length`: si modificas el cuerpo de la respuesta, actualiza el `Content-Length` o permite que la herramienta lo haga automáticamente.
- Guardar reglas de modificación si necesitas aplicarlas repetidamente.
- Recordar que estas modificaciones solo cambian lo que el navegador ve en ese momento; recargar la página o volver a solicitarla desde el servidor volverá al estado original (a menos que automatices la modificación en el proxy).

---
