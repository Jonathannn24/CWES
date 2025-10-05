# Configuración del proxy

## Introducción
Ahora que hemos instalado e iniciado ambas herramientas (Burp y ZAP), aprenderemos a utilizar la función más utilizada: **Web Proxy**.

Los proxies web se configuran entre el navegador y el servidor para capturar, inspeccionar e interceptar las solicitudes HTTP/HTTPS. Esto permite interceptar, modificar y volver a enviar peticiones para pruebas de seguridad.

---

## Navegador preconfigurado
Tanto Burp como ZAP incluyen un navegador preconfigurado con:
- Proxy configurado automáticamente (por defecto `127.0.0.1:8080`)
- Certificado CA instalado (para evitar advertencias HTTPS)
- Útil para comenzar rápidamente sin tocar la configuración del navegador del sistema

**Burp:** en `Proxy > Intercept` haz clic en **Open Browser** para abrir el navegador integrado.

**ZAP:** haz clic en el icono del navegador Firefox en la barra superior para abrir el navegador preconfigurado.

---

## Configuración del proxy para un navegador real (Firefox)
Si prefieres usar tu navegador (ej. Firefox), debes configurarlo para enrutar el tráfico a través del proxy (Burp/ZAP).

### 1. Puerto del proxy
- Por defecto ambos usan `127.0.0.1:8080`. Puedes cambiar el puerto en:
  - **Burp:** `Proxy > Options > Proxy listeners`
  - **ZAP:** `Tools > Options > Network > Local Servers/Proxies`

### 2. Configurar Firefox manualmente
1. Abrir `Preferences` → `General` → `Network Settings` → `Settings...`
2. Seleccionar **Manual proxy configuration**
3. Poner `HTTP Proxy: 127.0.0.1` y `Port: 8080` (y marcar “Use this proxy for all protocols” si se desea).

> Nota: si el puerto está en uso, el proxy no iniciará. Elige un puerto libre.

### 3. Usar FoxyProxy (recomendado)
FoxyProxy facilita alternar proxies en Firefox.

- Instala la extensión FoxyProxy (si no está instalada).
- Abre FoxyProxy → **Options** → **Add**
  - Title: `Burp` o `ZAP`
  - Proxy Type: `HTTP`
  - IP: `127.0.0.1`
  - Port: `8080`
  - Save
- Activa el perfil desde el icono de FoxyProxy para enrutar el navegador hacia Burp/ZAP.

> En PwnBox la configuración de FoxyProxy ya suele estar preconfigurada.

---

## Instalación del certificado CA (para HTTPS)
Para interceptar HTTPS sin advertencias, instala el certificado CA del proxy en Firefox.

### Burp
1. Con FoxyProxy activado hacia Burp, visita: `http://burp`
2. Haz clic en **CA Certificate** y descárgalo (por ejemplo `burp_ca.pem`).

### ZAP
1. En ZAP: `Tools > Options > Network > Server Certificates` → **Save**
2. Guarda el certificado (por ejemplo `zap_ca.crt`).

### Importar certificado en Firefox
1. Abre `about:preferences#privacy` → **View Certificates** (Administrar certificados)
2. Ve a la pestaña **Authorities** → **Import...**
3. Selecciona el archivo del certificado descargado (Burp o ZAP).
4. Marca:
   - **Trust this CA to identify websites**
   - (opcional) **Trust this CA to identify email users**
5. Acepta y cierra.

Ahora Firefox confiará en el proxy y las conexiones HTTPS pasarán sin advertencias.

---

## Validación final
1. Con FoxyProxy activado y el certificado importado, navega normalmente.
2. En Burp/ZAP verifica que las solicitudes aparezcan en la pestaña **Proxy → HTTP history** o **Sites/History**.
3. Intercepta una petición y comprueba que puedes ver y modificar encabezados y cuerpo.

---

## Consejos y buenas prácticas
- Recuerda desactivar el proxy cuando termines para evitar enrutar todo el tráfico accidentalmente.
- Si usas múltiples herramientas, asegúrate de que solo una esté escuchando en el mismo puerto.
- Para pruebas avanzadas activa/guarda proyectos en Burp Pro o usa sesiones persistentes en ZAP.
- Mantén los certificados CA privados y nunca los instales en navegadores/productores de confianza fuera de entornos de prueba.

---

## Resumen rápido (comandos/acciones)
```text
# Burp: iniciar jar (si usas jar)
java -jar /path/to/burpsuite.jar

# Burp: cambiar puerto del listener
Proxy > Options > Proxy listeners

# ZAP: iniciar (si usas jar)
java -jar /path/to/zaproxy.jar

# ZAP: guardar certificado
Tools > Options > Network > Server Certificates > Save

# Firefox: importar certificado
about:preferences#privacy -> View Certificates -> Authorities -> Import
```

---
