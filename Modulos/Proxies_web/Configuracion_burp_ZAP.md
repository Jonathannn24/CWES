# Configuración — Burp Suite y ZAP

## Introducción
Tanto Burp como ZAP están disponibles para Windows, macOS y cualquier distribución de Linux. Ambos ya están instalados en su instancia de PwnBox y se puede acceder a ellos desde el dock inferior o el menú de la barra superior. Ambas herramientas están preinstaladas en distribuciones comunes de Penetration Testing Linux como Parrot o Kali.

Cubriré aquí el proceso de instalación y configuración básico para ambas herramientas.

---

## Burp Suite

### Descarga e instalación
- Descargar desde la página oficial de descargas de Burp.
- Hay instaladores para **Windows**, **Linux** y **macOS**.  
- También hay un **JAR** multiplataforma que puede ejecutarse con Java:

```bash
java -jar </path/to/burpsuite.jar>
```

> **Nota:** Burp y ZAP dependen de Java Runtime Environment (JRE). Si no está incluido, deberá instalar Java en su sistema.

### Inicio y proyecto
Al iniciar Burp, se le pedirá crear un nuevo proyecto.  
- **Versión Community**: sólo proyectos temporales (no persistentes).  
- **Versión Pro/Enterprise**: opción de proyectos en disco para guardar el progreso.

Para empezar rápido:
1. Seleccione **Temporary project**.
2. Use **Burp Defaults** (o cargue un archivo de configuración si lo desea).
3. Presione **Start Burp**.

> Si realiza escaneos grandes o utiliza funciones Pro (por ejemplo Active Scan), podría interesarle guardar proyectos en disco (disponible en Pro).

### Ajustes visuales
- Tema oscuro: `Burp > Settings > User interface > Display` → seleccionar **Dark** en *Theme*.

---

## OWASP ZAP

### Descarga e instalación
- Descargar desde la página oficial de ZAP.  
- También disponible como **JAR** multiplataforma y ejecutable con:

```bash
java -jar </path/to/zaproxy.jar>
```

- En sistemas con paquete, puede arrancarse con:

```bash
zaproxy
```

### Inicio y proyecto
Al iniciar ZAP se le preguntará por persistencia de sesión:
- Puede elegir **no persistir** (proyecto temporal) para pruebas rápidas.

### Ajustes visuales
- Tema oscuro: `Tools > Options > Display` → seleccionar **Flat Dark** en *Look and Feel*.

---

## Recomendaciones comunes

- Ambas herramientas están incluidas en PwnBox y en muchas distros de pentesting (Kali, Parrot).
- Si no tiene Burp instalado, la opción del JAR es multiplataforma y sencilla si dispone de Java.
- Use **projectos temporales** para pruebas rápidas; use proyectos persistentes para trabajos largos que desee retener.
- Para un entorno gráfico cómodo active el tema oscuro en ambas herramientas si lo prefiere.

---

## Comandos útiles
- Ejecutar Burp JAR:
```bash
java -jar /ruta/a/burpsuite.jar
```

- Ejecutar ZAP JAR:
```bash
java -jar /ruta/a/zaproxy.jar
```

- Iniciar ZAP si está instalado como paquete:
```bash
zaproxy
```

---

## Enlaces de interés
- Página de descargas de Burp Suite: _(buscar en el sitio oficial PortSwigger)_
- Página de descargas de OWASP ZAP: _(sitio oficial de OWASP ZAP)_

---

## Resumen (rápido)
- **Burp Suite**: muy usado en pentesting web; la versión Community es potente, Pro añade muchas funciones automatizadas.
- **ZAP**: alternativa gratuita y de código abierto con muchas capacidades comparables; ideal si no desea licencias.
- Ambos requieren Java o vienen en instaladores con dependencias incluidas; se pueden usar en Windows/macOS/Linux y están preinstalados en PwnBox/Kali/Parrot.
