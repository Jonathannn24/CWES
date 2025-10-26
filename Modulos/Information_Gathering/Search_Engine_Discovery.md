# Descubrimiento de motores de búsqueda (Search Discovery) — Resumen

**Descripción**  
Uso de motores de búsqueda y operadores para recopilación OSINT aplicada al reconocimiento web. Legal y no intrusivo; útil para localizar páginas, archivos, inicios de sesión ocultos y datos expuestos.

---

## Por qué importa
- **Open Source:** información pública y legalmente accesible.  
- **Cobertura amplia:** muchos recursos indexados.  
- **Fácil de usar:** no requiere skills avanzadas.  
- **Económico:** gratuito y disponible.

**Aplicaciones:** evaluación de seguridad, inteligencia competitiva, periodismo de investigación, threat intelligence.

---

## Operadores de búsqueda (comandos)
> Sustituir `example.com` por el dominio objetivo autorizado.

- `site:example.com` — limitar resultados al dominio.
- `inurl:login` — buscar `login` en la URL.
- `filetype:pdf` — buscar archivos PDF (docx, xls, sql, etc.).
- `intitle:"texto exacto"` — buscar frase en el título.
- `intext:"texto"` o `inbody:"texto"` — buscar en el cuerpo.
- `cache:example.com` — ver versión en caché.
- `link:example.com` — páginas que enlazan al dominio.
- `related:example.com` — sitios relacionados.
- `info:example.com` — resumen de la página.
- `define:palabra` — definiciones.
- `numrange:1000-2000` — buscar números en rango.
- `allintext:admin password reset` — todas las palabras en el texto.
- `allinurl:admin panel` — todas las palabras en la URL.
- `allintitle:confidential report 2023` — todas las palabras en el título.
- `AND`, `OR`, `NOT` — operadores booleanos.
- `*` — comodín (ej. `user*`).
- `..` — rango numérico (ej. `100..500`).
- `"frase exacta"` — coincidencia exacta.
- `-term` — excluir término.

---

## Google Dorking — ejemplos (prácticos)
> Ejemplos para usar en búsquedas (siempre con autorización).

**Páginas de inicio de sesión**
```
site:example.com inurl:login
site:example.com (inurl:login OR inurl:admin)
```

**Archivos expuestos**
```
site:example.com filetype:pdf
site:example.com (filetype:xls OR filetype:docx)
```

**Archivos de configuración**
```
site:example.com inurl:config.php
site:example.com (ext:conf OR ext:cnf)
```

**Backups / dumps**
```
site:example.com inurl:backup
site:example.com filetype:sql
```

---

## Buenas prácticas
- Obtener **autorización** antes de búsquedas masivas sobre un objetivo.  
- **Correlacionar** hallazgos; una coincidencia no es prueba por sí sola.  
- Guardar consultas útiles y resultados relevantes.  
- Evitar automatizar sin control (posibles bloqueos o límites).

---
