# .well-known

El estándar **.well-known**, definido en [RFC 8615](https://datatracker.ietf.org/doc/html/rfc8615), sirve como un directorio estandarizado dentro del dominio raíz de un sitio web.  
Esta ubicación, accesible a través de la ruta `/.well-known/`, centraliza **metadatos críticos**, archivos de configuración e información relacionada con servicios, protocolos y mecanismos de seguridad.

Al establecer una ubicación consistente, `.well-known` simplifica el proceso de descubrimiento y acceso para navegadores, aplicaciones y herramientas de seguridad.  
Esto permite a los clientes localizar automáticamente archivos específicos construyendo la URL adecuada, por ejemplo:  
`https://example.com/.well-known/security.txt`.

El **Internet Assigned Numbers Authority (IANA)** mantiene un registro de URI bajo `.well-known`, cada una con un propósito definido por distintas especificaciones y estándares.

---

## Ejemplos de URI comunes

| Sufijo URI | Descripción | Estado | Referencia |
|-------------|-------------|---------|-------------|
| **security.txt** | Contiene información de contacto para reportar vulnerabilidades. | Permanente | [RFC 9116](https://datatracker.ietf.org/doc/html/rfc9116) |
| **/change-password** | URL estándar para redirigir a los usuarios a la página de cambio de contraseña. | Provisional | [W3C Spec](https://w3c.github.io/webappsec-change-password-url/#the-change-password-well-known-uri) |
| **openid-configuration** | Configuración de OpenID Connect sobre OAuth 2.0. | Permanente | [OpenID Discovery 1.0](http://openid.net/specs/openid-connect-discovery-1_0.html) |
| **assetlinks.json** | Verificación de propiedad de activos digitales (apps, etc.). | Permanente | [Digital Asset Links Spec](https://github.com/google/digitalassetlinks/blob/master/well-known/specification.md) |
| **mta-sts.txt** | Política SMTP MTA-STS para mejorar la seguridad del correo. | Permanente | [RFC 8461](https://datatracker.ietf.org/doc/html/rfc8461) |

---

Esta es solo una pequeña muestra de las muchas URI registradas en IANA.  
Cada entrada ofrece pautas específicas de implementación, garantizando un enfoque estandarizado para el uso del mecanismo `.well-known`.

---

## Reconocimiento web y `.well-known`

En el **reconocimiento web**, las URI bajo `.well-known` pueden revelar **endpoints y configuraciones** útiles para pruebas de penetración.  
Un caso especialmente interesante es `openid-configuration`.

El `openid-configuration` forma parte del protocolo **OpenID Connect Discovery**, una capa de identidad sobre **OAuth 2.0**.  
Cuando una aplicación cliente desea autenticarse mediante OpenID Connect, puede obtener la configuración del proveedor accediendo a:  
`https://example.com/.well-known/openid-configuration`

El endpoint devuelve un documento JSON con metadatos sobre endpoints, métodos de autenticación, emisión de tokens y más:

```json
{
  "issuer": "https://example.com",
  "authorization_endpoint": "https://example.com/oauth2/authorize",
  "token_endpoint": "https://example.com/oauth2/token",
  "userinfo_endpoint": "https://example.com/oauth2/userinfo",
  "jwks_uri": "https://example.com/oauth2/jwks",
  "response_types_supported": ["code", "token", "id_token"],
  "subject_types_supported": ["public"],
  "id_token_signing_alg_values_supported": ["RS256"],
  "scopes_supported": ["openid", "profile", "email"]
}
```

---

## Información que puede obtenerse

- **Authorization Endpoint:** URL usada para solicitudes de autorización de usuario.  
- **Token Endpoint:** URL donde se emiten los tokens.  
- **Userinfo Endpoint:** Endpoint que proporciona la información del usuario.  
- **JWKS URI:** Dirección del *JSON Web Key Set* (claves criptográficas del servidor).  
- **Supported Scopes y Response Types:** Permiten conocer funcionalidades y limitaciones del sistema.  
- **Algoritmos de firma soportados:** Detalles relevantes para evaluar medidas de seguridad.

---

## Conclusión

Explorar el registro de la **IANA** y experimentar con las distintas `.well-known` URI puede revelar configuraciones críticas.  
Como en el caso de `openid-configuration`, estas rutas estandarizadas ofrecen **acceso estructurado a metadatos esenciales**, ayudando a trazar un mapa detallado de la postura de seguridad de un sitio web.
