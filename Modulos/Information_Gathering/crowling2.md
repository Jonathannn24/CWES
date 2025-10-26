# Crawlin
El rastreo web es vasto e intrincado, pero no es necesario emprender este viaje solo. Hay una gran cantidad de herramientas de rastreo web disponibles para ayudarlo, cada una con sus propias fortalezas y especialidades. Estas herramientas automatizan el proceso de rastreo, haciéndolo más rápido y eficiente, permitiéndole concentrarse en analizar los datos extraídos.

## Rastreadores web populares
- **Burp Suite Spider:** Burp Suite, una plataforma de prueba de aplicaciones web ampliamente utilizada, incluye un potente rastreador activo llamado Spider. Spider se destaca en mapear aplicaciones web, identificar contenido oculto y descubrir vulnerabilidades potenciales.
- **OWASP ZAP (Zed Attack Proxy):** ZAP es un escáner de seguridad de aplicaciones web gratuito y de código abierto. Se puede utilizar en modo automatizado y manual e incluye un componente de araña para rastrear aplicaciones web e identificar posibles vulnerabilidades.
- **Scrapy (Python Framework):** Scrapy es un marco Python versátil y escalable para crear rastreadores web personalizados. Proporciona funciones enriquecidas para extraer datos estructurados de sitios web, manejar escenarios de rastreo complejos y automatizar el procesamiento de datos. Su flexibilidad lo hace ideal para tareas de reconocimiento personalizadas.
- **Apache Nutch (Scalable Crawler):** Nutch es un rastreador web de código abierto altamente extensible y escalable escrito en Java. Está diseñado para manejar rastreos masivos en toda la web o centrarse en dominios específicos. Si bien requiere más experiencia técnica para su instalación y configuración, su potencia y flexibilidad lo convierten en un activo valioso para proyectos de reconocimiento a gran escala.

Adherirse a prácticas de rastreo éticas y responsables es crucial sin importar qué herramienta elija. Obtenga siempre permiso antes de rastrear un sitio web, especialmente si planea realizar escaneos extensos o intrusivos. Tenga en cuenta los recursos del servidor del sitio web y evite sobrecargarlos con solicitudes excesivas.

## Scrapy
Aprovecharemos Scrapy y una araña personalizada diseñada para reconocimiento inlanefreight.com. Si está interesado en obtener más información sobre técnicas de rastreo/araña, consulte el "Uso de proxies web" módulo, ya que también forma parte de CWES.

### Instalación de Scrapy
Antes de comenzar, asegúrese de tener Scrapy instalado en su sistema. Si no lo haces, puedes instalarlo fácilmente usando pip, el instalador de paquetes de Python:

```bash
pip3 install scrapy
```

Este comando descargará e instalará Scrapy junto con sus dependencias, preparando su entorno para construir nuestra araña.

### ReconSpider
Primero, ejecute este comando en su terminal para descargar la araña scrapy personalizada ReconSpider, y extraerlo al directorio de trabajo actual.

```bash
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
unzip ReconSpider.zip
```

Con los archivos extraídos, puedes ejecutar ReconSpider.py usando el siguiente comando:

```bash
python3 ReconSpider.py http://inlanefreight.com
```

Reemplazar inlanefreight.com con el dominio que quieres explorar. La araña rastreará el objetivo y recopilará información valiosa.

## resultados.json
Después de correr ReconSpider.py, los datos se guardarán en un archivo JSON, results.json. Este archivo se puede explorar utilizando cualquier editor de texto. A continuación se muestra la estructura del archivo JSON producido:

```json
{
    "emails": [
        "lily.floid@inlanefreight.com",
        "cvs@inlanefreight.com"
    ],
    "links": [
        "https://www.themeansar.com",
        "https://www.inlanefreight.com/index.php/offices/"
    ],
    "external_files": [
        "https://www.inlanefreight.com/wp-content/uploads/2020/09/goals.pdf"
    ],
    "js_files": [
        "https://www.inlanefreight.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.3.2"
    ],
    "form_fields": [],
    "images": [
        "https://www.inlanefreight.com/wp-content/uploads/2021/03/AboutUs_01-1024x810.png"
    ],
    "videos": [],
    "audio": [],
    "comments": [
        "<!-- #masthead -->"
    ]
}
```

Cada clave en el archivo JSON representa un tipo diferente de datos extraídos del sitio web de destino:

| Clave JSON     | Descripción                                                                 |
|----------------|-----------------------------------------------------------------------------|
| emails         | Enumera las direcciones de correo electrónico que se encuentran en el dominio. |
| links          | Enumera las URL de los enlaces que se encuentran dentro del dominio.        |
| external_files | Enumera las URL de archivos externos, como archivos PDF.                    |
| js_files       | Enumera las URL de los archivos JavaScript utilizados por el sitio web.     |
| form_fields    | Las listas forman campos que se encuentran en el dominio (vacío en este ejemplo). |
| images         | Enumera las URL de las imágenes encontradas en el dominio.                 |
| videos         | Enumera las URL de los vídeos que se encuentran en el dominio (vacías en este ejemplo). |
| audio          | Enumera las URL de los archivos de audio que se encuentran en el dominio (vacío en este ejemplo). |
| comments       | Enumera los comentarios HTML que se encuentran en el código fuente.        |

Al explorar esta estructura JSON, puede obtener información valiosa sobre la arquitectura, el contenido y los posibles puntos de interés de la aplicación web para una mayor investigación.
