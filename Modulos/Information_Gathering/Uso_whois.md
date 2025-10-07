# WHOIS 

> Resumen práctico sobre qué es WHOIS, por qué importa en reconocimiento web y cómo usarlo.

---

## ¿Qué es WHOIS?

* Protocolo de consulta/ respuesta para consultar bases de datos de recursos de Internet (dominios, bloques IP, ASNs).
* Equivalente a una "guía telefónica" de Internet: registra propietario, registrador, fechas, servidores de nombres y contactos técnicos/administrativos.

## Información típica devuelta por WHOIS

* **Domain Name** — Nombre de dominio.
* **Registrar** — Empresa donde se registró el dominio.
* **Registrant / Admin / Tech** — Contactos y organización responsable.
* **Creation / Updated / Expiry dates** — Fechas importantes.
* **Name Servers** — Servidores DNS del dominio.
* **Domain status** — Bloqueos y restricciones (p. ej. `clientTransferProhibited`).

---

## ¿Por qué WHOIS es útil en Web Recon?

* **Identificar personal clave**: nombres y correos para ingeniería social o phishing.
* **Descubrir infraestructura**: NS, registrador y pistas de hosting asociados.
* **Analizar historial**: cambios de propietario o patrones (dominios registrados en masa, repeticiones en fechas).
* **Priorizar alertas**: dominios recientemente creados o con privacidad activada son señales de posible abuso.

---

## Tres escenarios prácticos

1. **Investigación de phishing**

   * Señales: registro reciente, registrante privado, hosting “bulletproof”.
   * Acción típica: bloquear dominio, buscar infraestructura asociada.

2. **Análisis de malware / C2**

   * Señales: registrante con correo anónimo, país con actividad maliciosa, registrador con historial laxo.
   * Acción típica: notificar proveedor de hosting, correlacionar IPs/dominios.

3. **Informe de inteligencia (threat intel)**

   * Patrones: dominios registrados en grupos, alias repetidos, NS comunes.
   * Resultado: IOCs (dominios, NS, fechas) para detección y bloqueo.

---

## Buenas prácticas al usar WHOIS

* Combine WHOIS con otras fuentes OSINT (DNS, SHODAN, Wayback, repositorios públicos).
* Correlacione dominios por **NS**, **registrador**, y rangos IP.
* Revise históricos (p. ej. servicios de WHOIS histórico) para cambios sospechosos.
* No confíe solo en WHOIS: muchos registrantes usan protección de privacidad.

---

## Herramientas y comando básico

> Nota: aquí se incluye solo el comando esencial para sistemas Linux; ajuste según tu plataforma.

* **Instalar (Debian/Ubuntu)**

```
sudo apt update
sudo apt install whois -y
```

* **Uso básico**

```
whois <dominio>
```

Ejemplo: `whois facebook.com` devuelve registrador, fechas, statuses y name servers; útil para verificar legitimidad y antigüedad.

---

## Qué buscar en la salida de WHOIS (lista rápida)

* Registro muy reciente ✅️ (posible phishing)
* Registrante privado/oculto ✅️ (señal de anonimato)
* Registrador con historial de abuso ✅️ (investigar)
* Name servers apuntando a proveedores sospechosos ✅️ (correlacionar)
* Estados `clientTransferProhibited`/`serverUpdateProhibited` ✅️ (dominio bien protegido)

---

## Siguientes pasos recomendados al obtener un WHOIS sospechoso

1. Hacer un **enumerado DNS** (subdominios, MX, SPF, etc.).
2. Buscar **correlaciones** en IPs y name servers (¿comparten otros dominios maliciosos?).
3. Revisar **Wayback/archivos** para contenido histórico.
4. Añadir indicadores a una lista de bloqueo y alertar a SOC/CSIRT si es relevante.

---

