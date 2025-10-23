# Transferencias de Zona DNS (Resumen)

**Qué es**  
Una **transferencia de zona DNS (AXFR)** copia todos los registros DNS de una zona (dominio y subdominios) desde un servidor DNS primario a un secundario. Si está mal configurada, puede filtrar todos los subdominios, direcciones IP y registros sensibles.

---

## Flujo básico (AXFR)
1. El servidor secundario solicita la transferencia (`AXFR`) al primario.  
2. El primario responde con el registro **SOA** (Start of Authority).  
3. El primario envía todos los registros de la zona: `A`, `AAAA`, `CNAME`, `MX`, `NS`, `TXT`, `SRV`, etc.  
4. Finaliza la transferencia y el secundario envía un ACK.

---

## Por qué es peligrosa
- Revela **subdominios ocultos** (dev, test, admin, backups, etc.).  
- Expone **direcciones IP** y recursos internos.  
- Muestra **servidores de nombres** y pistas sobre el proveedor de hosting.  
- Permite mapear la infraestructura completa del objetivo fácilmente.

---

## Remediación / Buenas prácticas
- **Permitir AXFR solo** desde servidores secundarios autorizados (lista blanca de IPs).  
- Deshabilitar transferencias de zona públicas.  
- Monitorear intentos de AXFR y alertar.  
- Mantener políticas de acceso y registrar cambios en la configuración DNS.

---

## Cómo probar (con autorización)

### Usar `dig` para solicitar AXFR
```bash
dig axfr @nameserver targetdomain.com
```

**Ejemplo**
```bash
dig axfr @nsztm1.digi.ninja zonetransfer.me
```
Si el servidor permite AXFR verás todos los registros de la zona (A, MX, NS, TXT, PTR, SRV...).

### Interpretación rápida
- Si obtienes una lista de registros: transferencia exitosa → **información sensible expuesta**.  
- Si obtienes `REFUSED` o `TRANSFER FAILED`: transferencia denegada (correcto).

---
---

## Referencias útiles
- `dig` (DNS utility) — ejemplos y opciones (`axfr`, `@server`, `+short`, `+trace`)  
- Documentación del servidor DNS usado (BIND, PowerDNS, Microsoft DNS) para configurar controles AXFR.
