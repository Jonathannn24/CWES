# Protocolo de Transferencia de Hipertexto Seguro (HTTPS)

## Descripción
HTTPS (HTTP Secure) es HTTP sobre una capa de cifrado (normalmente TLS). Protege la confidencialidad e integridad de las comunicaciones entre cliente y servidor, evitando que credenciales y datos viajen en texto claro y sean capturados por un atacante Man-in-the-Middle (MiTM).

---

## ¿Por qué usar HTTPS?
- Cifra todo el tráfico HTTP (cabeceras y cuerpo).
- Evita ataques MiTM cuando el cliente verifica correctamente certificados.
- Es el esquema recomendado (https://) y los navegadores marcan HTTP como inseguro.

> **Nota:** Si DNS se realiza en texto claro, un observador aún puede ver qué dominios se consultan. Se recomienda usar DNS cifrado (DoT/DoH) o VPN.

---

## Flujo HTTPS (alto nivel)
1. Cliente solicita `http://example.com` → servidor responde con `301` redirigiendo a `https://`.
2. Cliente inicia *TLS handshake* (ClientHello).
3. Servidor responde con certificado y se realiza el intercambio de claves.
4. Se establece canal cifrado y continúan solicitudes HTTP (ahora cifradas).
5. Cliente verifica certificado (CA, validez, nombre, etc.).

**Riesgo:** ataques de degradación (downgrade a HTTP). Mitigado con HSTS y verificaciones modernas.

---

## Uso con `curl`
- `curl` verifica certificados por defecto y falla con certificados inválidos:

```bash
curl https://inlanefreight.com
```

- Para ignorar verificación (solo en pruebas):

```bash
curl -k https://inlanefreight.com
```

Otros ejemplos:
```bash
# Mostrar cabeceras de respuesta
curl -I https://inlanefreight.com

# Verbose (ver handshake TLS y cabeceras)
curl -v https://inlanefreight.com
```

---

## Buenas prácticas
- Usar certificados válidos (Let's Encrypt u otra CA).
- Habilitar HSTS.
- Renovar certificados antes de caducidad.
- Usar TLS1.2+ o TLS1.3 y suites de cifrado modernas.
- Evitar configuraciones que permitan downgrade.
- Complementar con DNS cifrado (DoT/DoH) o VPN.

---

## Limitaciones
- HTTPS cifra el canal pero no soluciona vulnerabilidades como XSS o SQLi.
- Configuraciones TLS débiles (autofirmados, cadenas incompletas) pueden comprometer la seguridad.
- Los metadatos (SNI, DNS) pueden filtrar información si no se protegen.

---

## Conceptos clave
- **TLS handshake**: intercambio inicial para establecer claves.
- **Certificado X.509**: contiene información del dominio y CA.
- **HSTS**: política que fuerza HTTPS en navegadores.
- **SNI**: permite múltiples certificados en una IP.
- **DoT/DoH**: DNS cifrado sobre TLS/HTTPS.
