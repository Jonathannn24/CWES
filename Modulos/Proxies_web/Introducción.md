# Introducción a los proxies web

Hoy en día, la mayoría de las aplicaciones web y móviles modernas funcionan conectándose continuamente a servidores back-end para enviar y recibir datos y luego procesándolos en el dispositivo del usuario, como sus navegadores web o teléfonos móviles. Dado que la mayoría de las aplicaciones dependen en gran medida de servidores back-end para procesar datos, probar y proteger los servidores back-end se está volviendo rápidamente más importante.

Las pruebas de solicitudes web a servidores back-end constituyen la mayor parte de las pruebas de penetración de aplicaciones web, que incluyen conceptos que se aplican tanto a aplicaciones web como móviles. Para capturar las solicitudes y el tráfico que pasa entre aplicaciones y servidores back-end y manipular este tipo de solicitudes con fines de prueba, necesitamos usar Web Proxies.

## ¿Qué son los proxies web?

Los proxies web son herramientas especializadas que se pueden configurar entre un navegador/aplicación móvil y un servidor back-end para capturar y ver todas las solicitudes web que se envían entre ambos extremos, actuando esencialmente como herramientas de intermediario (MITM). Mientras que otras aplicaciones de captura de red (por ejemplo, Wireshark) funcionan analizando todo el tráfico local para ver qué pasa a través de una red, los proxies web funcionan principalmente con puertos web como HTTP/80 y HTTPS/443.

Los proxies web se consideran una de las herramientas más esenciales para cualquier pentester web. Simplifican significativamente el proceso de captura y reproducción de solicitudes web en comparación con herramientas anteriores basadas en CLI. Una vez configurado un proxy web, podemos ver todas las solicitudes HTTP realizadas por una aplicación y todas las respuestas enviadas por el servidor back-end. Además, podemos interceptar una solicitud específica para modificar sus datos y ver cómo los maneja el servidor back-end, lo cual es una parte esencial de cualquier prueba de penetración web.

## Usos de los proxies web

Si bien el uso principal de los servidores proxy web es capturar y reproducir solicitudes HTTP, tienen muchas otras características que permiten diferentes usos. Algunas tareas comunes son:

- Escaneo de vulnerabilidades de aplicaciones web  
- Fuzzing web  
- Rastreo web  
- Mapeo de aplicaciones web  
- Análisis de solicitudes web  
- Pruebas de configuración web  
- Revisiones de código

En este módulo no analizaremos ataques web específicos (otros módulos los cubren). Nos centraremos en cómo utilizar proxies web y sus funciones. Veremos las dos herramientas más comunes: **Burp Suite** y **OWASP ZAP**.

---

## Burp Suite

**Burp Suite** (o *Burp*) es el proxy web más común para pruebas de penetración web. Tiene una interfaz muy completa e incluso incluye un navegador Chromium integrado. Algunas funciones avanzadas son de pago (Burp Pro/Enterprise), pero la versión Community (gratuita) sigue siendo muy potente.

**Funciones de pago destacadas**:
- Escáner activo de aplicaciones web  
- Intruder (versión rápida/avanzada)  
- Ciertas extensiones avanzadas

Consejo: si tienes correo institucional (educativo o empresarial) puedes solicitar una prueba de Burp Pro para evaluar funciones avanzadas.

---

## OWASP Zed Attack Proxy (ZAP)

**OWASP ZAP** es otra herramienta proxy muy usada. Es un proyecto open source mantenido por OWASP y la comunidad. Al ser gratuito y de código abierto, no tiene limitaciones de uso que algunas funciones de Burp sí imponen en su versión gratuita. ZAP ha ido incorporando muchas funcionalidades avanzadas y es una alternativa sólida a Burp.

**Ventajas de ZAP**:
- Completamente gratuito y open source  
- Comunidad activa y contribuciones continuas  
- Muchas funciones avanzadas disponibles sin pago

---

## Elección entre Burp y ZAP

Aprender ambas herramientas es recomendable. En entornos corporativos o cuando se necesita un conjunto de herramientas maduras y soporte comercial, Burp Pro puede aportar valor. Para auditorías abiertas, formaciones o cuando se requiere una solución sin coste, ZAP es excelente. En la práctica, muchos pentesters usan la herramienta que mejor se adapta a la tarea y al presupuesto.

---
