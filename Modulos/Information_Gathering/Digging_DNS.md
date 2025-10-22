# Digging DNS — Resumen práctico (cheatsheet)

**Objetivo:** técnicas y comandos esenciales para reconocimiento DNS en pruebas de seguridad web. Resumen conciso con los comandos importantes y consejos.

---

## Herramientas DNS recomendadas
- **dig** — Muy versátil; consulta cualquier tipo de registro y soporta opciones avanzadas.
- **nslookup** — Sencillo, bueno para consultas rápidas (A, AAAA, MX).
- **host** — Salida concisa y directa.
- **dnsenum** — Enumeración automatizada: fuerza bruta, transferencias de zona.
- **fierce** — Reconocimiento y enumeración de subdominios, detección de comodines.
- **dnsrecon** — Múltiples técnicas combinadas para enumeración DNS.
- **theHarvester** — OSINT: recopila emails y datos públicos relacionados con dominios.
- **Servicios online** — Lookups rápidos si no hay CLI disponible.

---

## Tipos de registros útiles (rápido)
- **A** — IPv4
- **AAAA** — IPv6
- **CNAME** — alias
- **MX** — servidores de correo
- **NS** — servidores de nombres autorizados
- **TXT** — texto (SPF, verificaciones, datos expuestos)
- **SOA** — autoridad de la zona
- **PTR** — reverso (IP → nombre)

---

## Comandos `dig` esenciales (con ejemplos)
> Formato: `dig [opciones] [nombre] [tipo]`

- `dig domain.com`  
  — Búsqueda A por defecto.
- `dig domain.com A`  
  — Obtener registro A (IPv4).
- `dig domain.com AAAA`  
  — Obtener registro AAAA (IPv6).
- `dig domain.com MX`  
  — Listar servidores de correo.
- `dig domain.com NS`  
  — Servidores de nombres autorizados.
- `dig domain.com TXT`  
  — Registros TXT (SPF, claves, etc.).
- `dig domain.com CNAME`  
  — Canonical name (alias).
- `dig domain.com SOA`  
  — Inicio de autoridad (info de zona).
- `dig @1.1.1.1 domain.com`  
  — Consultar usando servidor DNS específico.
- `dig +trace domain.com`  
  — Seguir la resolución recursiva: root → TLD → autoritativo.
- `dig -x 192.168.1.1`  
  — Búsqueda inversa (PTR).
- `dig +short domain.com`  
  — Salida corta (solo respuesta).
- `dig +noall +answer domain.com`  
  — Mostrar únicamente la sección "ANSWER".
- `dig domain.com ANY`  
  — Intento de recuperar todos los registros (muchos servidores ignoran `ANY`).

**Ejemplo real:**
```
dig google.com

;; ANSWER SECTION:
google.com. 0 IN A 142.251.47.142
```

---

## Flujo práctico de reconocimiento DNS
1. **Recon pasivo primero** — WHOIS, buscadores, Wayback, GitHub, certificados públicos.
2. **Consulta básica con `dig`** — A / NS / MX / TXT.
3. **Comprobar servidores autoritativos** — `dig NS domain.com` y luego `dig @ns1.example.com domain.com SOA`.
4. **Reversa** — `dig -x <IP>` para identificar hostnames asociados.
5. **Trazado** — `dig +trace domain.com` para detectar delegaciones/servicios intermedios.
6. **Enumeración de subdominios** — `dnsenum`, `dnsrecon`, `fierce` o fuerza bruta con wordlists.
7. **Transferencia de zona (AXFR)** — probar `dig @<ns> domain.com AXFR` (si está permitida; rara y mal configurada).
8. **Buscar registros TXT sensibles** — `dig domain.com TXT` (SPF, claves leak, metadatos).
9. **Monitorización** — repetir consultas con programación para detectar cambios (nuevos subdominios, MX, etc.).

---

## Comandos rápidos para otras utilidades
- `nslookup domain.com`  
- `host domain.com`  
- `dnsenum domain.com`  
- `dnsrecon -d domain.com`  
- `fierce -dns domain.com`  
- `theHarvester -d domain.com -b all`  *(OSINT; recoge emails, subdominios, hosts)*

---

## Consejos y buenas prácticas
- **Pedir permiso** antes de realizar reconocimiento activo o fuerza bruta.
- **Rate-limit**: no bombardear servidores DNS; puede activar detección/IPS.
- **Evitar consultas `ANY` masivas**; muchos DNS modernos limitan o ignoran `ANY`.
- **Comprobar delegaciones**: zonas mal delegadas pueden revelar infraestructura de proveedor.
- **Buscar TXT y subdominios** por posibles credenciales o servicios extra (ej. `_1password=`).
- **Revisar SOA** para obtener contactos y serial (útil para detectar cambios).
- **Usar servidores distintos** (ej. `@1.1.1.1`, `@8.8.8.8`) para comparar respuestas y cachés.
- **Registros de zona AXFR**: si están habilitados, puedes descargar toda la zona (gran hallazgo).

---
