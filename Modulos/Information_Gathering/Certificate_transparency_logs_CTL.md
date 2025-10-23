# Registros de Transparencia de Certificados (Certificate Transparency Logs)

## Introducción
En la vasta extensión de Internet, la confianza es un bien frágil. Uno de los pilares de esta confianza es el protocolo **Secure Sockets Layer/Transport Layer Security (SSL/TLS)**, que cifra la comunicación entre el navegador y un sitio web. En el núcleo de SSL/TLS se encuentra el **certificado digital**, un pequeño archivo que verifica la identidad de un sitio web y permite una comunicación segura y cifrada.

Sin embargo, el proceso de emisión y gestión de estos certificados no es infalible. Los atacantes pueden explotar **certificados fraudulentos o mal emitidos** para hacerse pasar por sitios web legítimos, interceptar datos confidenciales o distribuir malware. Aquí es donde entran en juego los **Registros de Transparencia de Certificados (CT Logs)**.

---

## ¿Qué son los Registros de Transparencia de Certificados?
Los **Registros de Transparencia de Certificados (CT)** son libros de contabilidad públicos, de solo anexión, que registran la emisión de certificados SSL/TLS. Cada vez que una **Autoridad de Certificación (CA)** emite un nuevo certificado, debe enviarlo a varios registros CT. Estas bases de datos, mantenidas por organizaciones independientes, están abiertas a inspección pública.

Piense en los CT Logs como un **registro global de certificados**. Proporcionan un registro transparente y verificable de cada certificado SSL/TLS emitido, lo que ofrece beneficios clave como:

- **Detección temprana de certificados fraudulentos:** Permite a investigadores y propietarios identificar certificados mal emitidos y revocarlos rápidamente.  
- **Responsabilidad de las Autoridades de Certificación:** Cualquier error o práctica indebida es visible públicamente, fomentando la transparencia.  
- **Fortalecimiento de la Infraestructura PKI (Public Key Infrastructure):** Los registros CT refuerzan la confianza y la seguridad del ecosistema web.

---

## Cómo funcionan los Registros de CT
El funcionamiento de los CT Logs combina criptografía y auditoría pública:

1. **Emisión del certificado:** El propietario solicita un certificado a la CA, que verifica identidad y dominio. Luego, emite un *pre-certificate*.
2. **Envío al log:** La CA envía este pre-certificate a varios registros CT (garantizando redundancia y descentralización).
3. **SCT (Signed Certificate Timestamp):** Cada log genera un SCT, una prueba criptográfica de que el certificado fue registrado en un momento determinado.
4. **Verificación del navegador:** Los navegadores verifican los SCT en los logs públicos para confirmar la validez del certificado.
5. **Monitoreo:** Investigadores, navegadores y CAs auditan continuamente los CT Logs para detectar anomalías.

---

## La estructura del Árbol de Merkle
Para garantizar la integridad y resistencia a manipulaciones, los CT Logs utilizan una **estructura de árbol Merkle**. Cada hoja representa un certificado; los nodos intermedios son hashes de sus hijos; la raíz (Merkle Root) representa todo el registro.

**Ejemplo:**

```
Root Hash
├── Hash 1
│   ├── Cert 1
│   └── Cert 2
└── Hash 2
    ├── Cert 3
    └── Cert 4
```

Este diseño permite verificar cualquier certificado sin descargar el log completo. Si un solo bit cambia, la raíz se altera, indicando manipulación.

---

## CT Logs y Reconocimiento Web
Los registros CT son una herramienta poderosa para la **enumeración de subdominios**, ya que muestran todos los certificados emitidos (incluso antiguos o expirados) de un dominio y sus subdominios.

Ventajas:
- Descubrimiento sin fuerza bruta ni listas de palabras.  
- Acceso a subdominios históricos u ocultos.  
- Detección de entornos obsoletos o vulnerables.

---

## Herramientas para Consultar Registros CT
| Herramienta | Características | Casos de uso | Pros | Contras |
|--------------|----------------|---------------|------|----------|
| **crt.sh** | Interfaz web sencilla, búsqueda por dominio, muestra detalles de certificados y entradas SAN. | Identificación de subdominios y verificación del historial de certificados. | Gratuito, sin registro. | Opciones limitadas de filtrado. |
| **Censys** | Motor de búsqueda avanzado con filtrado por dominio, IP y atributos. | Análisis profundo de certificados y configuraciones. | API disponible, gran base de datos. | Requiere registro (plan gratuito). |

---

## Ejemplo: búsqueda con crt.sh
Podemos usar la API JSON de **crt.sh** para buscar subdominios de `facebook.com` que contengan “dev”:

```bash
curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[] | select(.name_value | contains("dev")) | .name_value' | sort -u
```

**Salida esperada:**

```
*.dev.facebook.com
*.newdev.facebook.com
dev.facebook.com
secure.dev.facebook.com
```

**Explicación:**
- `curl`: descarga los certificados del dominio.  
- `jq`: filtra los subdominios que contienen “dev”.  
- `sort -u`: ordena alfabéticamente y elimina duplicados.

---

## Conclusión
Los **Registros de Transparencia de Certificados** son esenciales para mantener la confianza y la seguridad del ecosistema SSL/TLS. Facilitan la detección de certificados ilegítimos, la auditoría pública y el fortalecimiento de la infraestructura de confianza digital.
