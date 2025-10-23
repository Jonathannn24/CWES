# Anfitriones virtuales — Resumen (VHost discovery)

Breve guía en **Markdown** con lo importante, comandos y precauciones para descubrir hosts virtuales (vhosts).

---
## Importante : poner en el /etc/hosts/ --> la ip y el nombre de dominio
## Concepto rápido

* **Virtual Hosts (VHosts)**: configuraciones del servidor web que permiten alojar varios sitios en una sóla IP usando el encabezado `Host` de HTTP.
* **Subdominio vs VHost**: un subdominio es una entrada DNS (p.ej. `dev.example.com`). Un VHost es la configuración del servidor web que sirve contenido según el `Host` recibido.
* Puedes acceder a un VHost sin DNS editando `/etc/hosts` (o `C:\Windows\System32\drivers\etc\hosts`).

## Tipos de alojamiento

* **Name-based**: usa el `Host` header (más común). No necesita IPs adicionales.
* **IP-based**: cada sitio tiene su propia IP.
* **Port-based**: varios sitios en la misma IP pero puertos distintos.

## Por qué buscar VHosts

* Descubrir sitios no publicados (paneles de administración, entornos de dev/test).
* Identificar superficie de ataque adicional.

## Herramientas útiles

* **gobuster** (modo `vhost`) — rápido y popular.
* **ffuf**, **feroxbuster** — fuzzer rápidos que pueden probar el header `Host`.
* **nmap** (scripts HTTP) — para comprobaciones adicionales.

## Preparación

1. **Obtener IP objetivo** (DNS lookup o `dig` / `host`).
2. **Seleccionar wordlist** (p.ej. SecLists `subdomains-top1million-110000.txt` o listas más pequeñas para pruebas cortas).
3. **Configurar límites**: threads, timeouts y respetar reglas/autoridad.

## Comandos esenciales

> **Gobuster — modo VHOST**

```bash
# Ejemplo básico
gobuster vhost -u http://<TARGET_IP>:<PORT> -w <wordlist> --append-domain

# Ejemplo real (puerto 81)
gobuster vhost -u http://inlanefreight.htb:81 \
  -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt \
  --append-domain -t 40 -o gobuster-vhosts.txt
```

Opciones útiles:

* `-t` : threads (aumenta velocidad, cuidado con detección).
* `-k` : ignorar errores TLS/SSL.
* `-o` : guardar salida.
* `--append-domain` : añade el dominio base a cada palabra (recomendado).

> **ffuf (header Host fuzzing)**

```bash
ffuf -u http://<TARGET_IP>/ -H "Host: FUZZ.<DOMAIN>" -w <wordlist> -mc 200,301,302 -t 40 -o ffuf-vhosts.json
```

> **feroxbuster** similar a gobuster, cambia la sintaxis pero permite recursion y filtros.

## Interpretación de resultados

* Respuestas con **200 / 301 / 302** o cambios en tamaño (`Size`) suelen indicar hosts válidos.
* Verifica manualmente los hallazgos con navegador (añadiendo entrada en `hosts`) y revisa contenido.
* Falsos positivos: algunos servidores retornan 200 para cualquier `Host` (wildcard). confirmar con contenido y rutas.

## Técnicas complementarias

* **Comprobar certificados TLS**: CN/SAN en certificado puede revelar nombres de host.
* **Revisar cabeceras HTTP** (Server, X-Powered-By) para pistas.
* **Probar zone transfers / DNS enumeration** para posibles subdominios adicionales.

## Riesgos y buenas prácticas

* **Detectable**: fuerza bruta de vhosts genera mucho tráfico y puede disparar IDS/WAF. Obtener autorización previa.
* **Tasa y threads**: bajar velocidad si el objetivo es sensible.
* **Registro y análisis**: guardar salidas y validar cada hallazgo manualmente.

## Checklist rápido

* [ ] Obtener IP objetivo.
* [ ] Elegir wordlist adecuada (size → equilibrio entre cobertura y ruido).
* [ ] Ejecutar `gobuster vhost` / `ffuf` con límites y guardar salida.
* [ ] Confirmar resultados añadiendo entradas `hosts` y revisar en navegador.
* [ ] Anotar falsos positivos y patrones (comodines, certificados).

---

