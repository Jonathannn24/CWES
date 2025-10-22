# Subdominio — Fuerza Bruta

**Descripción corta**  
La enumeración por fuerza bruta de subdominios prueba sistemáticamente una *wordlist* contra un dominio (p.ej. `dev.example.com`) para identificar subdominios válidos. Técnica **activa** útil cuando la recon pasiva no descubre suficientes activos.

---

## Flujo resumido
1. **Selección de wordlist**
   - *General-purpose*: `dev`, `staging`, `admin`, `mail`, `test`, ...
   - *Targeted*: orientada a industria/tecnologías del objetivo
   - *Custom*: lista propia basada en OSINT

2. **Iteración + consultas DNS**
   - Construir `subdominio.domain.com` y resolver (A/AAAA).

3. **Filtrado y validación**
   - Si resuelve → guardar. Validar con HTTP(S) si procede.
   - Detectar y descartar *wildcard* y falsos positivos.

4. **Recursividad (opcional)**
   - Si aparece `x.example.com`, intentar bruteforce sobre `*.x.example.com`.

---

## Herramientas recomendadas
- `dig`, `nslookup`, `host` — consultas manuales / rápidas  
- `dnsenum` — enumeración + brute-force + attempts de zone transfer  
- `fierce`, `dnsrecon` — reconocimiento/descubrimiento DNS  
- `amass` — discovery (OSINT + bruteforce)  
- `puredns`, `massdns` — resolución masiva y filtrado  
- `theHarvester` — OSINT combinado

---

## Comandos esenciales (ejemplos)

### `dig`
```bash
# A simple
dig domain.com A

# Usar servidor DNS específico
dig @1.1.1.1 domain.com A

# Respuesta corta (solo IPs)
dig +short hackthebox.com

# Traza completa
dig +trace domain.com
```

### dnsenum — fuerza bruta (ejemplo)
```bash
dnsenum --enum inlanefreight.com   -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt   -r
```
- `--enum` realiza varias acciones (whois, enum básica).  
- `-f <wordlist>` especifica la lista de subdominios.  
- `-r` habilita fuerza bruta **recursiva**.

---

## Buenas prácticas
- **Autorización**: obtener permiso antes de cualquier escaneo activo.  
- **Rate limiting**: evitar sobrecargar el objetivo.  
- **Combina técnicas**: OSINT + bruteforce → mejor cobertura.  
- **Validación**: comprobar vía HTTP/HTTPS y detectar wildcard.  
- **Guardar resultados**: exportar y limpiar duplicados.

---

## Señales a priorizar
- Subdominios que apuntan a servicios obsoletos (posibles vulnerabilidades).  
- Paneles de administración (`/admin`, `/wp-admin`, etc.).  
- CNAMEs que apuntan a terceros (posible takeover).

---

## Checklist rápido
- [ ] Elegir wordlist adecuada  
- [ ] Ejecutar enumeración (dnsenum / amass / puredns)  
- [ ] Filtrar y detectar wildcard  
- [ ] Validar vía HTTP(S) si procede  
- [ ] Documentar y priorizar hallazgos

---

**Referencias de wordlists útiles**  
- SecLists: `/usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt`

---
