# DNS — Resumen rápido (cheatsheet)

> **El DNS (Domain Name System)** es el sistema que traduce nombres de dominio legibles por humanos (como `www.example.com`) en direcciones IP que las computadoras entienden (`192.0.2.1`). Sin él, navegar por Internet sería como conducir sin mapa.

---

##  Cómo funciona el DNS

1. **Tu equipo pregunta (DNS Query):** verifica primero su caché local. Si no tiene la IP, contacta al **resolver** DNS (de tu ISP o público como 8.8.8.8).
2. **El resolver busca (Recursive Lookup):** si no sabe la IP, pregunta a los **root servers**.
3. **Servidor raíz (Root Server):** indica cuál es el **TLD Server** (.com, .org, etc.) correspondiente.
4. **Servidor TLD:** señala el **Authoritative Server** del dominio (`example.com`).
5. **Servidor autorizado:** devuelve la IP correcta.
6. **Resolver devuelve la IP** a tu equipo y la guarda temporalmente (cache).
7. **Tu navegador se conecta** al servidor web.

---

##  Archivo *hosts*

Archivo local que asocia manualmente nombres de host con direcciones IP.

Rutas:

* **Windows:** `C:\Windows\System32\drivers\etc\hosts`
* **Linux/macOS:** `/etc/hosts`

📄 Formato:

```
<IP>    <hostname> [<alias>]
```

Ejemplos:

```
127.0.0.1       localhost
192.168.1.10    devserver.local
0.0.0.0         unwanted-site.com  # Bloquear sitio
```

Usos:

* Redirigir un dominio a un servidor local.
* Probar conectividad manual.
* Bloquear sitios no deseados.

---

##  Conceptos clave

| Concepto                 | Descripción                                  | Ejemplo              |
| ------------------------ | -------------------------------------------- | -------------------- |
| **Domain Name**          | Nombre legible de un recurso.                | `www.example.com`    |
| **IP Address**           | Identificador numérico único.                | `192.0.2.1`          |
| **DNS Resolver**         | Traduce dominios a IPs.                      | `8.8.8.8` (Google)   |
| **Root Name Server**     | Nivel superior jerárquico.                   | `a.root-servers.net` |
| **TLD Name Server**      | Responsable de dominios `.com`, `.org`, etc. | Verisign para `.com` |
| **Authoritative Server** | Contiene la IP real.                         | `ns1.example.com`    |

---

##  Tipos de registros DNS

| Tipo      | Nombre completo    | Descripción                        | Ejemplo de zona                                            |
| --------- | ------------------ | ---------------------------------- | ---------------------------------------------------------- |
| **A**     | Address            | Asocia nombre → IPv4               | `www.example.com. IN A 192.0.2.1`                          |
| **AAAA**  | IPv6 Address       | Asocia nombre → IPv6               | `www.example.com. IN AAAA 2001:db8::1`                     |
| **CNAME** | Canonical Name     | Alias hacia otro host              | `blog.example.com. IN CNAME web.example.net.`              |
| **MX**    | Mail Exchange      | Servidor de correo                 | `example.com. IN MX 10 mail.example.com.`                  |
| **NS**    | Name Server        | Servidores de nombres              | `example.com. IN NS ns1.example.com.`                      |
| **TXT**   | Text               | Info de texto / verificación / SPF | `example.com. IN TXT "v=spf1 mx -all"`                     |
| **SOA**   | Start of Authority | Datos administrativos de la zona   | `example.com. IN SOA ns1.example.com. admin.example.com.`  |
| **SRV**   | Service            | Nombre/puerto de servicio          | `_sip._udp.example.com. IN SRV 10 5 5060 sip.example.com.` |
| **PTR**   | Pointer            | Búsqueda inversa (IP → nombre)     | `1.2.0.192.in-addr.arpa. IN PTR www.example.com.`          |

> El campo **IN** indica que pertenece a la clase Internet (el más usado hoy en día).

---

##  Ejemplo de archivo de zona

```
$TTL 3600
@ IN SOA ns1.example.com. admin.example.com. (
        2024060401 ; Serial
        3600       ; Refresh
        900        ; Retry
        604800     ; Expire
        86400 )    ; Minimum TTL

@   IN NS ns1.example.com.
@   IN NS ns2.example.com.
@   IN MX 10 mail.example.com.
www IN A 192.0.2.1
mail IN A 198.51.100.1
ftp  IN CNAME www.example.com.
```

---

##  Por qué DNS es importante en Web Recon

* **Descubre activos ocultos:** subdominios, servidores de correo, CNAME antiguos → posibles puntos de entrada.
* **Mapea infraestructura:** correlacionar NS, IPs y A records revela el hosting y la arquitectura.
* **Monitoreo de cambios:** nuevos subdominios o TXT sospechosos pueden indicar nuevos servicios o integraciones.

Ejemplo:

* Un CNAME `dev.example.com → oldserver.example.net` podría exponer un servidor vulnerable.
* Un TXT `_1password=...` puede delatar uso de software o servicios internos.

---

##  Comandos útiles

```
# Consultar registros A/NS/MX
$ dig example.com ANY +noall +answer
$ dig NS example.com
$ dig MX example.com

# Búsqueda inversa (PTR)
$ dig -x 192.0.2.1 +short

# Consultar registro TXT (SPF/DKIM)
$ dig TXT example.com

# Consultar DNS con host
$ host example.com

# nslookup interactivo
$ nslookup
> server 8.8.8.8
> set type=MX
> example.com
```

---

## Herramientas complementarias

* **Enum DNS:** `dnsenum`, `fierce`, `dnsrecon`.
* **Subdominios:** `sublist3r`, `amass`, `assetfinder`, `crt.sh`.
* **Monitoreo:** `SecurityTrails`, `DNSDumpster`, `VirusTotal`, `Spyse`.
* **Recon automatizado:** `theHarvester`, `Recon-ng`, `Maltego`.

---

## Checklist para análisis DNS en pruebas de penetración

* [ ] Enumerar subdominios (pasivo y activo).
* [ ] Consultar registros A, MX, NS, TXT, CNAME.
* [ ] Buscar registros SPF/DKIM/DMARC.
* [ ] Revisar PTR (búsqueda inversa).
* [ ] Correlacionar NS/IPs con otros dominios.
* [ ] Revisar históricos (Wayback + SecurityTrails).
* [ ] Identificar servicios externos (CDN, correos, balanceadores).

---

