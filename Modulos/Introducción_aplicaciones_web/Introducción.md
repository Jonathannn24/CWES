# Introducción a las Aplicaciones Web

## Resumen (rápido)
Las **aplicaciones web** son programas interactivos que se ejecutan en navegadores y adoptan una arquitectura **cliente‑servidor**. Tienen un frontend (HTML/CSS/JS) que corre en el navegador y un backend que procesa la lógica y gestiona datos en servidores y bases de datos. Las aplicaciones web son accesibles globalmente, actualizables centralmente y pueden ser tan sencillas como un blog o tan complejas como un servicio de correo.

---

## ¿Qué son y ventajas principales?
- **Independencia de plataforma:** se ejecutan en el navegador, no requieren instalación.
- **Actualizaciones centralizadas:** todos los usuarios usan la misma versión.
- **Modularidad y adaptabilidad:** responsive, ejecutables en múltiples pantallas.
- **Tipos de distribución:**  
  - *Código abierto:* WordPress, Joomla, OpenCart.  
  - *Propietario:* Wix, Shopify, DotNetNuke.

---

## Aplicaciones web vs Sitios estáticos
- **Sitio web estático:** contenido fijo, cambios manuales (Web 1.0).
- **Aplicación web:** contenido dinámico y personalizado por usuario (Web 2.0+).

## Aplicaciones web vs Apps nativas
- **Apps nativas:** mejor rendimiento, acceso a hardware y APIs del SO.
- **Apps web:** portables, más simples de mantener.
- **Híbridas / PWA:** combinan ventajas — rendimiento y capacidades nativas.

---

## Riesgos y motivos para hacer pruebas
- Las aplicaciones web tienen **gran superficie de ataque** y pueden exponer datos sensibles si están mal diseñadas.
- Un exploit exitoso puede permitir:
  - robo de datos,
  - acceso a sistemas internos,
  - ejecución remota de código,
  - interrupciones significativas del negocio.

Es esencial realizar **pruebas de seguridad** periódicas (OWASP Testing Guide es un buen punto de partida).

---

## Tipos de vulnerabilidades frecuentes (ejemplos reales)
- **Inyección SQL:** extraer datos (p. ej. emails en Active Directory) → ataques de fuerza/brute‑force.
- **Inclusion de archivos (LFI/RFI):** leer código fuente o ejecutar código.
- **Carga de archivos sin restricciones:** subir webshells → ejecución remota.
- **IDOR / Referencia directa de objetos insegura:** manipular IDs para acceder a recursos de otros usuarios.
- **Control de acceso roto:** manipular parámetros (p. ej. `roleid`) para escalar privilegios.

---

## Metodología de prueba recomendada (alto nivel)
1. **Enumerar** frontend (HTML/CSS/JS) y endpoints.
2. **Revisar** inputs del cliente (formularios, parámetros GET/POST, APIs).
3. **Probar** tanto desde contexto no autenticado como autenticado.
4. **Priorizar** con OWASP Top 10 y verificar parches/mitigaciones.
5. **Comprobar** cadenas de errores, manejos de sesion y control de acceso.

---

## Buenas prácticas para desarrolladores / administradores
- Validación y saneamiento del lado servidor (nunca confiar en el cliente).
- Uso de prepared statements/ORM para evitar inyecciones SQL.
- Restricción y validación de tipos y tamaños en cargas de archivos.
- Implementar control de acceso robusto y pruebas de autorización.
- Monitorización, logging seguro y parches rápidos.

---

## Recursos útiles
- OWASP Testing Guide / OWASP Top 10
- Documentación de frameworks usados (ej. Django, Express, Rails)
- Repositorios y herramientas para pruebas: Burp Suite, ZAP, sqlmap, wfuzz

---

*Archivo generado: `Introduccion_Aplicaciones_Web_resumen.md`*  
