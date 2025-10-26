# Automatización de Recon

Resumen corto
-------------
La automatización de reconocimiento web acelera y estandariza tareas repetitivas (enumeración DNS, subdominios, rastreo, escaneo rápido de puertos, recolección de metadatos), permitiendo cobertura a escala, resultados consistentes e integración con otras herramientas.

Por qué automatizar
-------------------
- **Eficiencia:** realiza tareas repetitivas más rápido.
- **Escalabilidad:** facilita recolectar datos en múltiples dominios.
- **Consistencia:** procedimientos reproducibles y menos errores humanos.
- **Cobertura:** combina múltiples módulos (DNS, subdominios, crawl, headers, WHOIS).
- **Integración:** encadena herramientas y APIs (Shodan, VirusTotal, crt.sh, etc.).

Marcos y herramientas recomendadas
---------------------------------
- **FinalRecon** — All-in-one (headers, whois, SSL, crawl, DNS, subdomains, dir, wayback, port scan).  
- **Recon-ng** — Marco modular en Python para OSINT y recogida automatizada.  
- **theHarvester** — Reúne correos, hosts y data desde motores de búsqueda y fuentes públicas.  
- **SpiderFoot** — Automatiza recopilación de inteligencia sobre un objetivo.  
- **OSINT Framework** — Catálogo de herramientas y técnicas.

FinalRecon — instalación y uso rápido
------------------------------------
Clonar, instalar dependencias y mostrar ayuda:

```bash
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x ./finalrecon.py
./finalrecon.py --help
```

Opciones relevantes (resumen):
- `--url URL`     : especifica objetivo.  
- `--headers`     : recuperar información de encabezados HTTP.  
- `--sslinfo`     : obtener información del certificado SSL/TLS.  
- `--whois`       : consulta WHOIS.  
- `--crawl`       : rastrear el objetivo.  
- `--dns`         : enumeración DNS.  
- `--sub`         : enumeración de subdominios.  
- `--dir`         : búsqueda de directorios (usa wordlists).  
- `--wayback`     : recuperar URLs históricas desde Wayback.  
- `--ps`          : escaneo rápido de puertos.  
- `--full`        : ejecución completa de reconocimiento.

Ejemplo práctico (headers + whois):
```bash
./finalrecon.py --headers --whois --url http://inlanefreight.com
```

Salida esperada (ejemplo resumido)
- IP objetivo, encabezados HTTP con `Server`, `Link`, `Content-Type`, etc.  
- Bloque WHOIS con fechas de registro, registrador y nameservers.  
- Exporta resultados a un directorio (ajustable con `-cd`).

Consejos de automatización
--------------------------
- **Configuración de API keys:** añade claves (Shodan, VirusTotal, etc.) si la herramienta lo soporta para enriquecer resultados.  
- **Rate limiting:** respeta límites y configura timeouts/threads para no causar carga excesiva.  
- **Filtrado de resultados:** exporta en formatos (txt/json) y procesa con scripts para eliminar falsos positivos.  
- **Integración con pipelines:** encadena la salida hacia análisis posterior (p.ej. CI, Jira, base de datos).  
- **Auditoría y permisos:** siempre obtener autorización previa antes de ejecutar escaneos automatizados en objetivos terceros.

Resumen final
-------------
Automatizar recon permite aplicar de forma repetible una batería amplia de pruebas y recolección de datos. Herramientas como FinalRecon reducen tiempo y unifican pasos (headers, whois, subdominios, crawl, directorios, wayback), pero deben usarse con responsabilidad y configurarse para evitar ruido y detección innecesaria.
