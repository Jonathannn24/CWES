# Vulnerabilidades públicas

Las vulnerabilidades más críticas de los componentes back-end son aquellas que pueden atacarse externamente y aprovecharse para tomar el control del servidor back-end sin necesidad de acceso local a ese servidor (es decir, pruebas de penetración externas). Estas vulnerabilidades suelen ser causadas por errores de codificación cometidos durante el desarrollo de los componentes back-end de una aplicación web. Por lo tanto, existe una amplia variedad de tipos de vulnerabilidades en esta área, que van desde vulnerabilidades básicas que pueden explotarse con relativa facilidad hasta vulnerabilidades sofisticadas que requieren un conocimiento profundo de toda la aplicación web.

---

## CVE público

Como muchas organizaciones implementan aplicaciones web que se utilizan públicamente, como aplicaciones web de código abierto y propietarias, estas aplicaciones web tienden a ser probadas por muchas organizaciones y expertos de todo el mundo. Esto lleva a descubrir con frecuencia una gran cantidad de vulnerabilidades, la mayoría de las cuales se parchean y luego se comparten públicamente y se les asigna un **CVE** (Vulnerabilidades y Exposiciones Comunes).

Muchos probadores de penetración también desarrollan *proofs of concept* para comprobar si una vulnerabilidad pública puede explotarse y, a menudo, ponen estos exploits a disposición del público para su uso, pruebas y fines educativos. Buscar exploits públicos es un primer paso esencial en una evaluación de seguridad.

**Consejo:** identifica la versión de la aplicación web (se puede encontrar en el código fuente, en una página `version.php`, etc.) y busca exploits públicos para esa versión en bases de datos como Exploit Database, Rapid7 o VulnDB.

---

## Sistema común de puntuación de vulnerabilidades (CVSS)

El *Common Vulnerability Scoring System* (CVSS) es un estándar para evaluar la gravedad de las vulnerabilidades. CVSS produce una puntuación base (0–10) que puede ajustarse con métricas temporales y ambientales.

- **Grupos de métricas:** Base, Temporal, Environmental.
- **Versiones comunes:** CVSS v2 y CVSS v3.

### Rangos de gravedad

**CVSS v2**
- Bajo: 0.0–3.9
- Medio: 4.0–6.9
- Alto: 7.0–10.0

**CVSS v3**
- Ninguno: 0.0
- Bajo: 0.1–3.9
- Medio: 4.0–6.9
- Alto: 7.0–8.9
- Crítico: 9.0–10.0

El NVD (National Vulnerability Database) proporciona puntajes CVSS base para la mayoría de los CVE y calculadoras interactivas para ajustar las métricas temporales y ambientales.

---

## Vulnerabilidades del servidor back-end

Además de las vulnerabilidades propias de las aplicaciones web, hay que considerar componentes del back-end (servidor web, sistema operativo, servicios, bases de datos). Algunas vulnerabilidades críticas en servidores web permiten la explotación remota sin acceso previo, por ejemplo:

- **Shellshock** (vulnerabilidad histórica en `bash`) que permitió ejecución remota vía solicitudes HTTP en ciertos setups.
- Vulnerabilidades específicas en servidores web (Apache, NGINX, IIS) o en software de la pila (PHP, módulos, extensiones) que conducen a RCE (Remote Code Execution).

Las vulnerabilidades del servidor y de la base de datos suelen aprovecharse tras obtener acceso local o desde movimientos laterales en la red; sin embargo, las fallas en servicios expuestos públicamente son las más críticas para pruebas externas.

---

## Buenas prácticas al evaluar vulnerabilidades públicas

1. **Identificar versión y componentes**: localizar versiones de la aplicación, frameworks, plugins y servidores.
2. **Buscar CVE/exploits**: usar bases de datos de vulnerabilidades (Exploit-DB, Rapid7, NVD).
3. **Priorizar por impacto**: centrarse en CVE con puntuación alta/critica y en RCE.
4. **Verificar configuraciones**: muchas fallas provienen de mala configuración, no solo de bugs en el código.
5. **Considerar toda la pila**: plugins, módulos, servidores web, y dependencias externas.
6. **Documentar y reportar**: incluir PoC, pasos para reproducir, riesgo y recomendación de mitigación/patch.

---

## Recursos útiles

- National Vulnerability Database (NVD)
- Exploit Database (exploit-db.com)
- Rapid7 Vulnerability DB
- OWASP Top 10

---
