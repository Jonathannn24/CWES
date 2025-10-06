# Herramientas de proxy

Un aspecto importante del uso de servidores proxy web es permitir la interceptación de solicitudes web realizadas por herramientas de línea de comandos y aplicaciones cliente pesadas. Esto nos brinda transparencia en las solicitudes web realizadas por estas aplicaciones y nos permite utilizar todas las diferentes funciones de proxy que hemos utilizado con las aplicaciones web.

Para enrutar todas las solicitudes web realizadas por una herramienta específica a través de nuestras herramientas de proxy web, debemos configurarlas como proxy de la herramienta (por ejemplo `http://127.0.0.1:8080`), similar a lo que hicimos con nuestros navegadores. Cada herramienta puede tener un método diferente para configurar su proxy, por lo que es posible que tengamos que investigar cómo hacerlo para cada una.

> **Nota:** Las herramientas de proxy generalmente las ralentizan; por tanto, sólo úsalas cuando necesites investigar solicitudes, no para uso normal.

---

## Proxychains

`proxychains` es una herramienta útil en Linux que enruta el tráfico de cualquier herramienta de línea de comandos a través de un proxy especificado. Para usar `proxychains`:

1. Edita `/etc/proxychains.conf` y añade (o descomenta) la línea al final, por ejemplo:
```text
#socks4         127.0.0.1 9050
http 127.0.0.1 8080
```

2. Usa la opción `-q` para modo silencioso (suprime la salida de información de conexión):
```bash
proxychains -q curl http://SERVER_IP:PORT
```

En Burp o ZAP verás la solicitud GET/POST correspondiente en el historial del proxy.

---

## Metasploit

Puedes forzar que los módulos de Metasploit utilicen un proxy con la opción `PROXIES`. Ejemplo usando el módulo `robots_txt`:

```bash
msfconsole
msf6 > use auxiliary/scanner/http/robots_txt
msf6 auxiliary(scanner/http/robots_txt) > set PROXIES HTTP:127.0.0.1:8080
PROXIES => HTTP:127.0.0.1:8080
msf6 auxiliary(scanner/http/robots_txt) > set RHOST SERVER_IP
msf6 auxiliary(scanner/http/robots_txt) > set RPORT PORT
msf6 auxiliary(scanner/http/robots_txt) > run
```

Después, revisa el historial del proxy (Burp/ZAP) para inspeccionar todas las peticiones generadas por Metasploit.

---

## Otras herramientas y clientes

El mismo enfoque es aplicable a otras herramientas, scripts o clientes pesados:

- Configura la opción de proxy de la herramienta al host/puerto del proxy (ej. `127.0.0.1:8080`).
- Ejecuta la herramienta; el tráfico HTTP(S) pasará por Burp o ZAP.
- Inspecciona, repite o modifica las peticiones desde el historial del proxy.

---

## Buenas prácticas

- **No proxyices todo el tiempo.** Los proxies ralentizan el tráfico; habilítalos solo mientras investigas.
- **Usa navegador preconfigurado** (Burp/ZAP) para pruebas web interactivas; para herramientas CLI usa `proxychains` o la configuración nativa de la herramienta.
- **Instala certificados CA** en tu navegador si necesitas inspeccionar tráfico HTTPS (ver sección de configuración de certificados).
- **Revisa el historial del proxy** para reproducir y modificar peticiones con Repeater (Burp) o Request Editor (ZAP).
- **Ten cuidado con datos sensibles** al interceptar y modificar peticiones (credenciales, cookies, tokens).

---

## Ejemplo rápido: curl vía proxychains

```bash
# Usando proxychains (con proxy configurado a 127.0.0.1:8080 en /etc/proxychains.conf)
proxychains -q curl http://SERVER_IP:PORT
```

En tu proxy (Burp/ZAP) deberías ver la solicitud HTTP GET interceptada y poder inspeccionarla.

---

## Ejemplo rápido: ver peticiones de Metasploit en Burp

```bash
msfconsole
use auxiliary/scanner/http/robots_txt
set PROXIES HTTP:127.0.0.1:8080
set RHOST SERVER_IP
set RPORT PORT
run
```

Luego abre Burp → Proxy → HTTP history y localiza las peticiones a `/robots.txt`.

---
