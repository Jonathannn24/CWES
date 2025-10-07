# Burp Scanner

Una característica esencial de las herramientas de proxy web son sus escáneres web. Burp Suite viene con **Burp Scanner**, un potente escáner para varios tipos de vulnerabilidades web, utilizando un *Crawler* para construir la estructura del sitio web, y *Scanner* para escaneo pasivo y activo.

> **Nota:** Burp Scanner es una función exclusiva para profesionales y no está disponible en la versión comunitaria gratuita de Burp Suite.

---

## Alcance objetivo

Opciones para iniciar un escaneo en Burp Suite:

- Iniciar el escaneo en una solicitud específica de **Proxy History**.
- Iniciar un nuevo escaneo en un conjunto de objetivos.
- Iniciar un escaneo de elementos dentro del alcance.

Para agregar elementos al alcance: **Target > Site map**, clic derecho en el elemento → *Add to scope*.  
También se pueden excluir elementos peligrosos (por ejemplo, `/logout`, `/xmlrpc.php`).

---

## Rastrero (Crawler)

- El *Crawler* navega por el sitio siguiendo enlaces y formularios, construyendo un mapa del sitio.
- Opciones de ejecución: **Crawl** o **Crawl and Audit** (éste último incluye el escaneo activo tras el rastreo).
- Configuración del rastreo: estrategia (rápida, completa), límites, credenciales de inicio de sesión (si se desean pruebas autenticadas).

Ejemplo de flujo:
1. Agregar URL al alcance.
2. `Dashboard > New Scan` → seleccionar configuración de rastreo.
3. Iniciar y observar progreso en `Dashboard > Tasks`.
4. Revisar `Target > Site map` al finalizar.

> El rastreo solo sigue enlaces presentes en las páginas (no realiza discovery masivo tipo ffuf a menos que se use Intruder/Content Discovery y luego se agregue al alcance).

---

## Escáner pasivo

- Analiza únicamente el contenido de las páginas ya visitadas (no envía nuevas solicitudes).
- Busca posibles problemas sin verificar por envío de payloads (ej. cabeceras faltantes, indicios de XSS en JS).
- Devuelve vulnerabilidades con un *level of confidence* (informativo, probable, seguro).
- Cómo usar: clic derecho en un elemento del *Site map* → *Do passive scan*.

---

## Escáner activo

- Ejecuta: crawl + fuzzing + validación activa de las posibles vulnerabilidades halladas.
- Pasos:
  1. Crawl y fuzzer para identificar páginas.
  2. Escaneo pasivo.
  3. Verificación activa de hallazgos (envío de payloads).
  4. Análisis de JavaScript y más técnicas de comprobación.
- Muy potente para detectar XSS, SQLi, RCE, command injection, etc.
- Se configura desde `New Scan` → seleccionar **Crawl and Audit** y elegir políticas de auditoría (por ejemplo: *critical issues only*).

Durante el escaneo activo se puede observar:
- `Dashboard > Tasks` para progreso.
- `Logger` para ver solicitudes generadas por el escáner.
- `Issue activity` para revisar los hallazgos (filtrar por gravedad/confianza).

Ejemplo: Burp identifica *OS command injection* con gravedad alta y confianza firme en un parámetro `ip`.

---

## Configuración fina

- **Scope**: incluir/excluir patrones con expresiones regulares.
- **Audit checks**: seleccionar tipos de pruebas (todo, solo críticas, etc.).
- **Crawl strategy**: ajustar rapidez y límites.
- **Login sequences**: registrar pasos de inicio de sesión o aportar credenciales para escaneo autenticado.
- **Grep/Extract**: reglas para marcar respuestas relevantes durante ataques (útil en Intruder).

---

## Informes (Reports)

- `Target > Site map` → clic derecho en el host → `Issue > Report issues for this host`.
- Se puede exportar en distintos formatos e incluir selecciones por gravedad/confianza.
- El informe incluye:
  - Resumen por gravedad.
  - Detalles de cada issue (Poc, request/response, cómo remediar).
- **Advertencia**: no enviar un informe automático sin validación manual. Usar los resultados como apoyo y comprobar/explotar manualmente antes de reportar.

---

## Buenas prácticas y advertencias

- Evitar escanear páginas destructivas (logout, delete, endpoints que provoquen acciones críticas) — excluirlas del alcance.
- Para aplicaciones con login, usar credenciales o registros de sesión para escanear de forma autenticada.
- Revisar y validar manualmente los hallazgos importantes (falsos positivos/negativos).
- Ajustar límites y tiempos para no sobrecargar el objetivo.
- Los escaneos activos pueden generar mucho tráfico y cambios; obtener autorización explícita antes de ejecutar pruebas.

---

## Resumen rápido

- **Burp Scanner** = Crawler + Passive Scan + Active Scan.
- **Passive**: seguro, no envía payloads, detecta indicios.
- **Active**: agresivo, envía pruebas, confirma vulnerabilidades.
- Solo disponible en **Burp Pro**.
- Útil para detectar XSS, SQLi, RCE, command injection, y otras vulnerabilidades comunes.
- Genera informes detallados con PoC y recomendaciones.

---
