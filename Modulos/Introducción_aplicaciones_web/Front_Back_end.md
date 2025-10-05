# Front End vs. Back End

Es posible que hayamos escuchado los términos *front end* y *back end* (o *full stack*) en el desarrollo web. Ambos son partes clave del ciclo de desarrollo web, pero se refieren a áreas diferentes de la aplicación.

---

## Front End (Cliente)

La interfaz de una aplicación web contiene los componentes que el usuario ve e interactúa directamente desde el navegador (lado del cliente).  
Componentes principales:
- **HTML**: estructura del contenido.
- **CSS**: estilos y diseño visual.
- **JavaScript**: comportamiento y dinámica.

Características y responsabilidades:
- Renderizado en tiempo real por el navegador.
- Debe ser responsivo (adaptarse a distintos tamaños de pantalla).
- Involucra diseño visual, UI y UX.
- Puede incluir frameworks/librerías como React, Vue, Angular, etc.

Ejemplo de tareas front-end:
- Diseño web y conceptualización visual.
- Implementación de layouts, animaciones y accesibilidad.
- Optimización para rendimiento en navegador.

---

## Back End (Servidor)

El back-end controla la lógica y funcionalidades principales que se ejecutan en servidores remotos. Es la parte que normalmente no vemos directamente.

Componentes principales:
- **Servidores back-end**: hardware y OS (Linux, Windows).
- **Servidores web**: Apache, NGINX, IIS.
- **Bases de datos**: MySQL, PostgreSQL, MSSQL, Oracle, MongoDB, etc.
- **Frameworks**: Django (Python), Laravel (PHP), Express (Node.js), Spring (Java), ASP.NET (C#).

Responsabilidades:
- Procesamiento de solicitudes y respuestas HTTP.
- Gestión de la lógica de negocio y acceso a la base de datos.
- Exposición de APIs para la comunicación con el front-end.
- Integración con servicios externos y almacenamiento.

Arquitectura y despliegue:
- Componentes del back-end pueden estar en servidores separados o en contenedores (Docker).
- Separación y segmentación ayudan a mitigar riesgos y mejorar escalabilidad.

---

## Interacción Frontend ↔ Backend

- El front-end envía **solicitudes HTTP** al back-end (GET, POST, PUT, DELETE).
- El back-end procesa la solicitud, interactúa con la base de datos o servicios y devuelve la respuesta (HTML, JSON, etc.).
- APIs (REST/GraphQL) suelen ser la interfaz principal para esta comunicación.

---

## Pruebas y vulnerabilidades

Aunque no tengamos acceso al código back-end, las aplicaciones pueden ser vulnerables desde el front-end (entrada de usuario) o diseño inseguro del back-end.

Ejemplos de vulnerabilidades comunes:
- **Inyección SQL** — manejo inseguro de entradas.
- **Inclusión de archivos remotos/locales** — puede exponer o ejecutar código.
- **Carga de archivos no restringida** — posible ejecución remota de código.
- **IDOR / Control de acceso roto** — modificación de IDs en URLs que permite acceder a recursos de otros usuarios.
- **XSS (Cross-Site Scripting)** — ejecución de scripts maliciosos en el navegador.

---

## Errores típicos (Top 20) — resumen importante
1. Permitir datos no validados en la base de datos.  
2. Centrarse sólo en el sistema, no en componentes individuales.  
3. Usar mecanismos de seguridad homemade.  
4. Considerar seguridad al final.  
5. Almacenar contraseñas en texto plano.  
6. Contraseñas débiles.  
7. Datos sin cifrar en BD.  
8. Depender excesivamente del cliente.  
9. Ser demasiado optimista (no validar).  
10. Permitir variables vía rutas URL.  
11. Confiar en código de terceros sin revisar.  
12. Cuentas de puerta trasera hardcodeadas.  
13. Inyecciones SQL.  
14. Inclusiones de archivos remotos.  
15. Manejo inseguro de datos.  
16. No cifrar datos correctamente.  
17. No usar sistemas criptográficos seguros.  
18. Ignorar la capa 8 (usuario).  
19. No auditar acciones de usuarios.  
20. Configuración incorrecta de WAF / firewall de aplicaciones.

Estos errores suelen originar las vulnerabilidades principales listadas por OWASP (Control de acceso roto, Inyecciones, Configuración insegura, etc.).

---

## Buenas prácticas (breve)
- Validar y sanitizar toda entrada del usuario (server-side).
- Separar responsabilidades: UI, lógica de negocio y datos.
- Usar cifrado para datos sensibles y TLS para transporte.
- Implementar controles de acceso y autenticación robustos.
- Mantener dependencias y componentes actualizados.
- Realizar pruebas de seguridad periódicas (OWASP ASVS / OWASP Top 10).

---

## Lecturas y recursos recomendados
- OWASP Top 10
- OWASP ASVS
- Documentación de frameworks (Django, Laravel, Express, etc.)
- Guías oficiales de despliegue seguro de servidores web (NGINX, Apache)

---
