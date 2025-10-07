# Reconocimiento Web — Resumen

Este archivo es una **hoja resumen** en Markdown con los puntos esenciales para realizar reconocimiento web (web recon). Ideal para descargar/guardar y usar como referencia rápida.

---

## Objetivos del reconocimiento

* **Identificar activos:** páginas, subdominios, IPs, tecnologías.
* **Descubrir información oculta:** backups, configs, documentación.
* **Analizar superficie de ataque:** tecnologías, endpoints, configuraciones.
* **Recolectar inteligencia:** correos, personal clave, patrones para ingeniería social.

---

## Enfoques

### Reconocimiento activo

* Interacción directa con el objetivo (riesgo de detección mayor).
* Técnicas típicas:

  * **Port scanning:** `nmap`, `masscan` (alto riesgo).
  * **Vulnerability scanning:** `nikto`, `nessus`, `openvas` (alto riesgo).
  * **Banner grabbing / service enum:** `nc`, `nmap -sV` (bajo/medio).
  * **OS fingerprinting:** `nmap -O` (bajo).
  * **Web spidering:** Burp/ZAP spider, `scrapy` (bajo/medio si mal configurado).

### Reconocimiento pasivo

* Sin interacción directa (muy bajo riesgo de detección).
* Fuentes y técnicas:

  * **Motores de búsqueda:** Google, DuckDuckGo, Shodan.
  * **WHOIS / DNS:** `whois`, `dig`, `dnsenum`, `dnsrecon`.
  * **Wayback / Web archives:** Wayback Machine.
  * **Redes sociales / OSINT:** LinkedIn, Twitter, GitHub.
  * **Repositorios de código:** búsqueda de credenciales o info expuesta.

---

## Herramientas útiles (rápida referencia)

* `nmap`, `masscan`, `unicornscan`
* `nikto`, `openvas`, `nessus`
* `whois`, `dig`, `nslookup`, `host`, `dnsenum`, `fierce`, `dnsrecon`
* Burp Suite, OWASP ZAP (spider, proxy, scanner)
* Shodan, Censys
* Wayback Machine, Google Dorks
* GitHub/GitLab search, OSINT frameworks (theHarvester, Maltego)

---

## Ejemplos de comandos rápidos

* Escaneo de puertos (simple):

  ```bash
  nmap -sC -sV -oA recon_nmap target.com
  ```
* WHOIS:

  ```bash
  whois target.com
  ```
* DNS (listar registros A/NS/MX):

  ```bash
  dig +noall +answer target.com ANY
  dig NS target.com
  dig MX target.com
  ```
* Enumerar subdominios (ejemplo con `dnsrecon`):

  ```bash
  dnsrecon -d target.com -t brt
  ```
* Buscar en Wayback:

  * Visitar: `https://web.archive.org/web/*/https://target.com`

---

## Análisis de la superficie de ataque

* Inventariar tecnologías: servidor web, frameworks, CMS, librerías.
* Identificar endpoints expuestos (APIs, admin panels, endpoints internos).
* Priorizar: **exposición pública**, **datos sensibles**, **funcionalidad crítica**.

---

## Recomendaciones operativas

* Comenzar por técnicas pasivas para construir contexto sin alertar detecciones.
* Cuando se haga reconocimiento activo, ajustar velocidad/huella para evitar detección.
* Registrar todo: comandos, resultados, timestamps y fuentes.
* Respetar el ámbito (scope) y reglas de autorización.

---

## Próximos pasos sugeridos

1. WHOIS + DNS enumeration.
2. Enumeración de subdominios y mapeo (passive + active).
3. Rastrear sitio (spider) con Burp/ZAP para mapear rutas y formularios.
4. Escaneo de vulnerabilidades pasivo / luego activo (si está autorizado).

---


