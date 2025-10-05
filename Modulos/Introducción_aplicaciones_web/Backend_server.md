# Servidores de Back-End

Un **servidor back-end** es el hardware y sistema operativo que aloja todas las aplicaciones necesarias para ejecutar una aplicación web. Es el sistema que ejecuta todos los procesos y tareas que componen la aplicación. Este servidor encaja dentro de la **Capa de acceso a datos (Data Access Layer)**.

---

##  Software

El servidor back-end contiene los siguientes tres componentes principales:

1. **Web Server (Servidor web)**  
2. **Database (Base de datos)**  
3. **Development Framework (Marco de desarrollo)**  

Estos trabajan juntos para procesar las solicitudes del cliente y devolver las respuestas adecuadas.

Además, pueden incluir otros componentes de software como:
- Hipervisores  
- Contenedores (por ejemplo, Docker)  
- WAF (Web Application Firewall)  

###  Pilas comunes de servidores web

| Combinación | Componentes principales |
|--------------|-------------------------|
| **LAMP** | Linux, Apache, MySQL, PHP |
| **WAMP** | Windows, Apache, MySQL, PHP |
| **WISA** | Windows, IIS, .NET, SQL Server |
| **MAMP** | macOS, Apache, MySQL, PHP |
| **XAMPP** | Multiplataforma, Apache, MySQL, PHP/PERL |

Cada pila ofrece un entorno diferente para ejecutar aplicaciones web. Por ejemplo, LAMP es ampliamente utilizado en entornos Linux, mientras que WISA es típico en servidores Windows empresariales.

---

## Hardware

El **hardware del servidor back-end** contiene todos los recursos físicos que permiten la ejecución de las aplicaciones web. Su potencia y rendimiento determinan la estabilidad y capacidad de respuesta del sitio o aplicación.

En arquitecturas modernas, las aplicaciones web suelen distribuir la carga entre múltiples servidores back-end que trabajan de forma coordinada para manejar grandes volúmenes de tráfico y solicitudes simultáneas.

Las aplicaciones web no necesitan ejecutarse directamente en un solo servidor físico: pueden aprovechar **centros de datos, entornos virtualizados y servicios en la nube** que ofrecen hosts virtuales, escalabilidad automática y redundancia.

---

 **Referencia:**  
Una lista más completa de pilas de soluciones web puede encontrarse en [este artículo](https://en.wikipedia.org/wiki/Solution_stack).
