# WHOIS — Resumen rápido (cheatsheet)

## ¿Qué es WHOIS?

WHOIS es un protocolo de consulta/ respuesta para obtener información pública sobre recursos de Internet (dominios, bloques IP, ASNs). Actúa como una "guía telefónica" de Internet: quién registró un dominio, cuándo, por quién y qué servidores de nombres usa.

---

## Comando básico

```bash
whois ejemplo.com
```

Salida típica (fragmento):

```
Domain Name: ejemplo.com
Registrar: RegistrarName
Creation Date: 2019-08-05T22:43:09Z
Updated Date: 2023-07-03T01:11:15Z
Name Server: ns1.ejemplo.net
Registrant Contact: Company / Person / email
...
```

---

## Campos clave y qué significan

* **Domain Name**: dominio consultado.
* **Registrar**: empresa donde se registró el dominio.
* **Registrant / Admin / Tech Contact**: responsable legal, administrativo y técnico (pueden incluir nombre, email y teléfono).
* **Creation / Updated / Expiration Date**: fechas de creación, última modificación y expiración.
* **Name Servers**: servidores DNS autorizados para el dominio.
* **Registry Domain ID / WHOIS Server**: identificadores y servidor whois del registrador.

> Nota: por motivos de privacidad (GDPR), muchos contactos aparecen redacted o con datos del proveedor de privacidad.

---

## Historia breve

WHOIS se originó en los años 70 como un directorio rudimentario para ARPANET. Elizabeth Feinler y el NIC de Stanford jugaron un papel clave en su creación. Con el tiempo evolucionó y hoy convive con servicios modernos (RDAP) y paneles de registradores.

---

## Por qué WHOIS es útil en Web Recon

* **Identificar personal clave**: nombres y correos que ayudan en evaluación de ingeniería social (phishing, spear-phishing).
* **Descubrir infraestructura**: NS, registrador, IPs asociadas y pistas sobre dónde está alojado el servicio.
* **Análisis histórico**: cambios de propietario o contactos pueden indicar fusiones, migraciones o exposición previa.
* **Correlación**: combinar WHOIS con DNS, certificados TLS y búsquedas OSINT para Mapear la huella digital.

---

## Herramientas y recursos útiles

* **CLI**: `whois` (suele venir instalado en Linux/macOS), `rdap` (para consultas RDAP).
* **Web**: DomainTools, WhoisXMLAPI, Shodan, VirusTotal, Wayback Machine y servicios WHOIS históricos.
* **Complementarios**: `dig`, `nslookup`, `host` para DNS; `certsh` o revisar certificados TLS para datos alternativos.

---

## Comandos y ejemplos prácticos

* WHOIS básico:

  ```bash
  whois inlanefreight.com
  ```
* Consultar servidores de nombres y registros DNS:

  ```bash
  dig NS ejemplo.com +short
  dig A ejemplo.com +short
  ```
* Usar RDAP (cuando esté disponible):

  ```bash
  rdap domain ejemplo.com
  ```
* Buscar historial WHOIS (servicios online): DomainTools/WhoisFreaks (puede requerir cuenta de pago).

---

## Tips y buenas prácticas

* **Correlaciona datos**: cruza WHOIS con DNS, certificados, subdominios, IPs y repositorios de código público.
* **Ten en cuenta la privacidad**: muchos registros están ofuscados por privacidad. No asumir que la ausencia de datos significa que no hay información útil.
* **Revisa histórico**: los cambios en registrante/NS/registrar pueden revelar migraciones o exposición previa.
* **Automatiza con cuidado**: si haces muchas consultas, respeta las limitaciones y reglas del registrador para evitar bloqueo.

---

## Riesgos y limitaciones

* **Información inexacta o protegida** por privacidad/GDPR.
* **Bloqueo por abuso** si haces consultas masivas.
* **No es una fuente única**: hay que combinarla con otras técnicas OSINT.

---

## Checklist rápido para una consulta WHOIS en reconocimiento

* [ ] Ejecutar `whois domain` y guardar salida raw.
* [ ] Extraer registrador, fechas, NS y contactos.
* [ ] Consultar `dig NS` y `dig A` para correlacionar infraestructura.
* [ ] Buscar historial WHOIS si se sospecha cambio de propiedad.
* [ ] Correlacionar correos/telefonos con redes sociales y repositorios.

---

## Lecturas y siguientes pasos recomendados

* Explorar RDAP como alternativa moderna a WHOIS.
* Integrar WHOIS en flujos OSINT (subdomain enumeration, cert-search, Shodan).
* Practicar consultas en dominios públicos y comparar resultados históricos.

---


