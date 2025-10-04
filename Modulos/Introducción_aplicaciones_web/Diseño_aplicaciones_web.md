# Diseño de Aplicaciones Web

## Introducción
No existen dos aplicaciones web idénticas. Cada empresa diseña sus aplicaciones según sus necesidades y público objetivo. Para comprender cómo se ejecutan y estructuran las aplicaciones web, debemos conocer su infraestructura, componentes y arquitectura.

---

## Categorías Principales
| Categoría | Descripción |
|------------|-------------|
| **Infraestructura de Aplicaciones Web** | Define la estructura y los componentes necesarios (como bases de datos) para el funcionamiento correcto. |
| **Componentes de Aplicaciones Web** | Incluye UI/UX, cliente y servidor. |
| **Arquitectura de Aplicaciones Web** | Define la relación entre todos los componentes. |

---

## Modelos de Infraestructura

### 1. Cliente-Servidor
El servidor aloja la aplicación y el cliente (navegador) interactúa con ella.  
**Ejemplo:** Un usuario accede a `https://www.acme.local` → el servidor procesa la solicitud y devuelve el contenido.

### 2. Un Servidor
Toda la aplicación (y su base de datos) se aloja en un único servidor.  
 Fácil de implementar.  
 Riesgoso: si el servidor se ve comprometido o falla, todo deja de funcionar.

### 3. Muchos Servidores - Una Base de Datos
Separación de funciones. Múltiples servidores acceden a una base de datos común.  
 Segmentación de activos.  
 Mejora la seguridad al aislar servicios.  
Un fallo en la base de datos afecta a todos los servidores.

### 4. Muchos Servidores - Muchas Bases de Datos
Cada aplicación tiene su propia base de datos.  
Alta redundancia y seguridad.  
Implementación compleja; requiere balanceadores de carga.

---

## Componentes Clave

- **Cliente:** navegador o interfaz de usuario.  
- **Servidor:** ejecuta la lógica de la aplicación.  
- **Servidor Web:** gestiona solicitudes HTTP.  
- **Base de Datos:** almacena datos persistentes.  
- **Microservicios:** pequeñas funciones independientes.  
- **Integraciones de terceros:** API externas.  
- **Funciones sin servidor:** tareas ejecutadas en entornos en la nube (AWS Lambda, Azure Functions, etc.).

---

## Arquitectura de Tres Capas

| Capa | Descripción |
|------|--------------|
| **Presentación** | Interfaz con el usuario (HTML, CSS, JS). |
| **Aplicación** | Procesa las solicitudes, verifica permisos y maneja la lógica. |
| **Datos** | Gestiona el acceso y almacenamiento de información. |

**Ejemplo:** Arquitectura ASP.NET Core → Cliente ⇄ Proxy IIS ⇄ App ⇄ Base de datos/Servicios externos.

---

## Microservicios
Son componentes independientes que realizan una sola tarea.  
**Ejemplo de microservicios en una tienda online:**
- Registro  
- Búsqueda  
- Pagos  
- Calificaciones  
- Reseñas  

**Ventajas:**
- Escalabilidad flexible  
- Despliegue rápido  
- Código reutilizable  
- Mayor resiliencia

---

## Aplicaciones Sin Servidor (Serverless)
Plataformas como AWS, Azure y GCP permiten ejecutar aplicaciones web sin gestionar servidores.  
- Se ejecutan en contenedores sin estado (ej. Docker).  
- Permiten escalar automáticamente.  
- Reducen costes de mantenimiento.

---

## Seguridad en la Arquitectura
- Las vulnerabilidades pueden surgir de errores **de diseño**, no solo de programación.  
- Es fundamental implementar **RBAC (Role-Based Access Control)**.  
- Las pruebas de penetración deben realizarse **en todas las fases del desarrollo**.  

**Ejemplo:**  
Si una aplicación permite acceso a funciones de administración por error en el control de roles → riesgo crítico.

---

## Conclusión
Comprender la infraestructura, componentes y arquitectura de una aplicación web es esencial para:
- Evaluar su seguridad.  
- Diseñar pruebas de penetración efectivas.  
- Detectar vulnerabilidades de diseño antes de que sean explotadas.
