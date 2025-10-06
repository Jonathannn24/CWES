# Burp Intruso

Tanto Burp como ZAP proporcionan funciones adicionales además del proxy web predeterminado, que son esenciales para las pruebas de penetración de aplicaciones web. Dos de las características adicionales más importantes son web fuzzers y web scanners. Los fuzzers web integrados son herramientas poderosas que actúan como herramientas de fuzzing web, enumeración y fuerza bruta. Esto también puede actuar como una alternativa para muchos de los fuzzers basados en CLI que utilizamos, como ffuf, dirbuster, gobuster, wfuzz, entre otros.

El fuzzer web de Burp se llama **Burp Intruder**, y se puede utilizar para difuminar páginas, directorios, subdominios, parámetros, valores de parámetros y muchas otras cosas. Aunque es mucho más avanzado que la mayoría de las herramientas de fuzzing web basadas en CLI, la versión **Community** está limitada a una velocidad de 1 solicitud por segundo, lo que la hace extremadamente lenta en comparación con las herramientas de fuzzing web basadas en CLI. La versión **Pro** tiene velocidad ilimitada y características avanzadas.

En esta sección se demuestra el uso de Burp Intruder para fuzzing y enumeración web.

---

## Objetivo

1. Inicia Burp y su navegador preconfigurado.
2. Visita la aplicación web objetivo.
3. En el **Proxy HTTP History**, localiza la solicitud a usar, clic derecho → **Send to Intruder** (o `Ctrl+I`).
4. Ve a la pestaña **Intruder** (`Ctrl+Shift+I`) para configurar el ataque.

En el panel **Target** verás los detalles del objetivo (host, puerto, HTTPS).

---

## Posiciones

En **Positions** colocas los marcadores `§` que serán reemplazados por las cargas útiles.  
Ejemplo: para fuzzear directorios, selecciona `DIRECTORY` en la ruta `GET /DIRECTORY/` y pulsa **Add §**.

> Nota: deja las líneas finales de la solicitud sin modificar para evitar errores del servidor.

---

## Cargas útiles (Payloads)

En la sección **Payloads** configuras las listas de palabras que Burp insertará en las posiciones `§`.

### Principales configuraciones de Payloads

1. **Payload Position & Type**  
   - Indica el conjunto de payloads (ej. `1 - DIRECTORY`) y el tipo (Simple List, Runtime file, Character substitution, etc.).
   - Para un único punto, usa **Sniper**; para múltiples posiciones, considera **Cluster Bomb** o **Pitchfork** según el caso.

2. **Payload Configuration**  
   - **Simple List**: añade manualmente o **Load** desde archivo (ej. `/opt/useful/seclists/Discovery/Web-Content/common.txt`).
   - **Runtime file**: útil para listas muy grandes (evita cargar todo en memoria).

3. **Payload Processing**  
   - Reglas para filtrar o transformar payloads (ej. **Skip if matches regex** para omitir líneas que empiezan con `.`: `^\..*$`).

4. **Payload Encoding**  
   - Opciones para codificar la carga útil (URL-encoding, etc.). Déjalo activado si es necesario.

---

## Configuración del ataque (Settings)

En **Settings** puedes ajustar opciones como:
- Número de reintentos en fallo de red.
- Pausa antes de reintentos.
- **Grep - Match**: marcar respuestas por contenido. Para fuzzing de directorios, añade `200 OK` para resaltar respuestas 200.
- **Grep - Extract**: extraer partes relevantes de respuestas largas.
- **Resource Pool**: controla cuántos recursos/red usar (útil para ataques grandes).

---

## Ejecución del ataque

Pulsa **Start attack**. En la versión Community el ataque será lento; en Pro será mucho más rápido.

- Observa la tabla de resultados: columnas útiles son **Payload**, **Status**, **Length**, y las coincidencias marcadas por **Grep**.
- Ordena por **200 OK** o **Length** para encontrar potenciales rutas interesantes (ej. `/admin/` con status `200`).

---

## Usos típicos de Intruder

- Enumeración de directorios/páginas (como `ffuf`/`gobuster`).
- Fuerza bruta de credenciales (user/pass).
- Fuzzing de parámetros (para SQLi, LFI, RCE, etc.).
- Manipulación de parámetros para bypass de autenticación o control de acceso.
- Pruebas específicas: manipular cabeceras, cookies, campos, etc.

> Nota: la versión gratuita limita la velocidad; para fuzzing intensivo y pruebas a gran escala, usa herramientas CLI optimizadas o Burp Pro.

---

## Consejos y buenas prácticas

- Para listas grandes, usa **Runtime file** para ahorrar memoria.
- Aplica reglas de **Payload Processing** para limpiar o filtrar la lista (ej. omitir archivos que empiezan por `.`).
- Usa **Grep** para marcar rápidamente respuestas relevantes (por código, longitud o texto).
- Revisa manualmente rutas interesantes en el navegador o con Repeater.
- Combina Intruder con Repeater y el historial del proxy para refinar payloads y observar respuestas.

---

## Recursos

- Documentación oficial de Burp Intruder: https://portswigger.net/burp/documentation/desktop/tools/intruder
- SecLists (listas útiles): https://github.com/danielmiessler/SecLists

---
