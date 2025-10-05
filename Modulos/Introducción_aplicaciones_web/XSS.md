# Scripting entre sitios (XSS)

HTML Injection las vulnerabilidades a menudo se pueden utilizar para realizar también **Scripting entre sitios (XSS)** ataques mediante inyección de código JavaScript a ejecutar en el lado del cliente. Una vez que podamos ejecutar código en la máquina de la víctima, potencialmente podremos obtener acceso a la cuenta de la víctima o incluso a su máquina. XSS es muy similar a HTML Injection en la práctica. Sin embargo, XSS implica la inyección de código JavaScript para realizar ataques más avanzados en el lado del cliente, en lugar de simplemente inyectar código HTML. Hay tres tipos principales de XSS:

| Tipo | Descripción |
|------|-------------|
| **Reflected XSS** | Ocurre cuando la entrada del usuario se muestra en la página después del procesamiento (por ejemplo, resultado de búsqueda o mensaje de error). |
| **Stored XSS** | Ocurre cuando la entrada del usuario se almacena en la base de datos del back-end y luego se muestra al recuperarla (por ejemplo, publicaciones o comentarios). |
| **DOM XSS** | Ocurre cuando la entrada del usuario se muestra directamente en el navegador y se escribe en un objeto DOM HTML (por ejemplo, nombre de usuario o título de página vulnerable). |

En el ejemplo que vimos para HTML Injection, no hubo desinfección de entrada alguna. Por lo tanto, es posible que la misma página sea vulnerable a ataques XSS. Podemos intentar inyectar la siguiente carga útil de **DOM XSS** en JavaScript, que debería mostrarnos el valor de la cookie para el usuario actual:

```javascript
#"><img src=/ onerror=alert(document.cookie)>
```

Una vez que ingresamos nuestra carga útil y presionamos _OK_, veremos que aparece una ventana de alerta con el valor de la cookie:

> Esta carga útil está accediendo al árbol de documentos HTML y recuperando el valor `document.cookie`. Cuando el navegador procese nuestra entrada, se considerará nuevo DOM, y nuestro JavaScript se ejecutará, mostrándonos el valor de la cookie en una ventana emergente.

Un atacante puede aprovechar esto para robar sesiones basadas en cookies y enviárselas a sí mismo, intentando usar el valor de la cookie para autenticarse en la cuenta de la víctima. El mismo ataque se puede utilizar para ejecutar otros tipos de acciones maliciosas contra los usuarios de una aplicación web. XSS es un tema amplio que se tratará en profundidad en módulos posteriores.
