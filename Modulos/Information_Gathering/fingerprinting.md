# Fingerprinting 

## Introducción
La **Fingerprinting** se centra en extraer detalles técnicos sobre las tecnologías que impulsan un sitio web o una aplicación web. De manera similar a cómo una huella digital identifica de forma única a una persona, las firmas digitales de servidores web, sistemas operativos y componentes de software pueden revelar información crítica sobre la infraestructura de un objetivo y posibles debilidades de seguridad.

Este conocimiento permite adaptar ataques y explotar vulnerabilidades específicas de las tecnologías identificadas.

### Importancia
- **Ataques dirigidos:** Identificar tecnologías específicas permite centrar los esfuerzos en exploits conocidos.
- **Configuraciones incorrectas:** Detecta software desactualizado o configuraciones inseguras.
- **Priorización de objetivos:** Ayuda a determinar los sistemas más vulnerables.
- **Perfil completo:** Permite comprender la postura de seguridad del objetivo.

---

## Técnicas de huellas dactilares

### 1. Banner Grabbing
Captura de los banners que presentan servidores web u otros servicios, los cuales suelen revelar el software y versión.

### 2. Análisis de encabezados HTTP
Los encabezados **HTTP** transmiten información como:
- **Server:** tipo y versión del servidor web.
- **X-Powered-By:** tecnologías como PHP, ASP.NET o frameworks.

### 3. Respuestas específicas
Solicitudes especialmente diseñadas pueden provocar respuestas únicas que delatan tecnologías o versiones concretas.

### 4. Análisis del contenido
Estructura HTML, scripts o comentarios pueden revelar el uso de CMS, frameworks o bibliotecas específicas.

---

## Herramientas comunes
| Herramienta | Descripción | Características |
|--------------|-------------|-----------------|
| **Wappalyzer** | Extensión de navegador para perfilado tecnológico. | Identifica CMS, frameworks y herramientas. |
| **BuiltWith** | Analizador web con informes detallados. | Planes gratuitos y de pago. |
| **WhatWeb** | Herramienta de línea de comandos. | Amplia base de datos de firmas. |
| **Nmap** | Escáner de red. | Scripts NSE para fingerprinting especializado. |
| **Netcraft** | Servicio de análisis de servidores web. | Informa sobre tecnología y seguridad. |
| **wafw00f** | Detecta **Web Application Firewalls (WAF)**. | Identifica tipo y configuración del WAF. |

---

## Ejemplo práctico: inlanefreight.com

### 1. Banner Grabbing con `curl`
```bash
curl -I inlanefreight.com
```
**Resultado:**
```
HTTP/1.1 301 Moved Permanently
Server: Apache/2.4.41 (Ubuntu)
Location: https://inlanefreight.com/
```

El servidor utiliza **Apache/2.4.41 (Ubuntu)**.

```bash
curl -I https://inlanefreight.com
```
**Resultado:**
```
Server: Apache/2.4.41 (Ubuntu)
X-Redirect-By: WordPress
Location: https://www.inlanefreight.com/
```
Se confirma el uso de **WordPress**.

```bash
curl -I https://www.inlanefreight.com
```
**Resultado:**
```
Server: Apache/2.4.41 (Ubuntu)
Link: <https://www.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Content-Type: text/html; charset=UTF-8
```
La ruta `/wp-json/` confirma una API de WordPress.

---

## 2. Detección de WAF con `wafw00f`
Instalación:
```bash
pip3 install git+https://github.com/EnableSecurity/wafw00f
```
Ejecución:
```bash
wafw00f inlanefreight.com
```
**Resultado:**
```
The site https://inlanefreight.com is behind Wordfence (Defiant) WAF.
```
El sitio está protegido por **Wordfence (Defiant)**.

---

## 3. Fingerprinting con `Nikto`
Instalación:
```bash
sudo apt update && sudo apt install -y perl
git clone https://github.com/sullo/nikto
cd nikto/program
chmod +x ./nikto.pl
```
Escaneo:
```bash
nikto -h inlanefreight.com -Tuning b
```
**Resultados destacados:**
```
+ Server: Apache/2.4.41 (Ubuntu)
+ A Wordpress installation was found.
+ License file found may identify site software.
+ Missing Strict-Transport-Security header.
+ The site uses TLS but lacks HSTS.
```
### Hallazgos
- IPs: 134.209.24.248 (IPv4) y 2a03:b0c0:1:e0::32c:b001 (IPv6).
- Servidor: Apache/2.4.41 (Ubuntu).
- CMS: WordPress.
- Cabeceras inseguras: falta de HSTS.
- Versión antigua de Apache.

---

## Conclusión
El **fingerprinting** es esencial en el reconocimiento web, revelando información técnica crítica sobre la infraestructura del objetivo.  
Combinando herramientas como **curl**, **wafw00f** y **Nikto**, se obtiene un perfil completo del servidor y sus vulnerabilidades.

**Buenas prácticas:**
- Verificar siempre la autorización antes del escaneo.  
- Usar múltiples herramientas para resultados consistentes.  
- Combinar con otras fases de reconocimiento (DNS, puertos, subdominios).
