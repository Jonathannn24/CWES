# Crawling — Resumen práctico

**Qué es**  
El *crawling* (o *spidering*) es el proceso automatizado de recorrer páginas web siguiendo enlaces, para descubrir e indexar contenido. Es útil para reconocimiento web porque revela estructura, enlaces ocultos y archivos expuestos.

---

## Cómo funciona (resumen)
1. **Semilla**: se parte de una URL inicial.  
2. **Descarga**: se recupera la página y se extrae su contenido.  
3. **Extracción de enlaces**: se extraen enlaces (internos/externos) y se añaden a una cola.  
4. **Iteración**: el crawler procesa la cola de enlaces de forma sistemática hasta agotar el alcance o cumplir límites.

---

## Estrategias comunes
- **Breadth‑First (BFS)**: explora por niveles (ancho primero). Bueno para mapear la estructura general.  
- **Depth‑First (DFS)**: sigue rutas largas antes de retroceder (profundidad primero). Útil para contenido profundo o páginas poco enlazadas.

---

## Qué extraer (prioridad)
- **Enlaces**: internos y externos.  
- **Metadatos**: títulos, descripciones, fechas, autores.  
- **Comentarios**: posible info sensible o pistas.  
- **Archivos sensibles**: backups (`.bak`, `.old`), `config.*`, `*.log`, `wp-config.php`, etc.  
- **APIs / Endpoints**: rutas `wp-json`, `/api`, `/admin`, `/uploads`, etc.

> Consejo: correlaciona hallazgos (p. ej. `/files/` + navegación por directorios) para identificar riesgos reales.

---

## Buenas prácticas para reconocimiento (ética y técnica)
- **Pedir autorización** antes de rastrear sistemas que no te pertenecen.  
- **Respetar `robots.txt`** salvo que tengas permiso explícito para ignorarlo.  
- **Limitar tasa/threads** para no sobrecargar el servidor.  
- **Registrar y contextualizar** los hallazgos: un solo dato rara vez es suficiente.

---

## Herramientas y comandos útiles (compacto)
- `wget` (simple, espejo):
```bash
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://target.example/
```
- `wget` (modo spider, solo comprobar enlaces):
```bash
wget --spider -r -l 5 https://target.example/
```
- `curl` (obtener HTML / headers):
```bash
curl -sL https://target.example/ -o page.html
curl -I https://target.example/
```
- `scrapy` (framework de crawling en Python — para crawls personalizados).  
- **Burp Suite / OWASP ZAP** — spiders integrados para crawls autenticados y controlados.  
- `httrack` — espejo de sitios web.  
- `feroxbuster`, `gobuster`, `ffuf` — para descubrir directorios/archivos (fuzzing complementario al crawling).

---

## Resumen rápido
- El *crawling* descubre enlaces y contenido accesible, no adivina rutas (eso es fuzzing).  
- Prioriza extracción de enlaces, archivos sensibles y metadatos.  
- Usa crawling con cuidado (autoridad, tasa, `robots.txt`).  
- Combina resultados con otras técnicas (fingerprinting, CT logs, fuerza bruta) para maximizar hallazgos.

---
