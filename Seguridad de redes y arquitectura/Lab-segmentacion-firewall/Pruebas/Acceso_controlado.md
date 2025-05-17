# 🔐 Prueba de acceso controlado hacia el Servidor AD

---

### 🎯 Objetivo.

Verificar que las VLANs autorizadas pueden acceder únicamente a los servicios específicos habilitados en el servidor de Active Directory (AD), según las políticas configuradas en el firewall.

---

### 🧪 Entorno.

- **Servidor AD:** 10.10.20.3 – VLAN20  
- **Clientes:**  
  - VLAN10 – Usuarios internos  
  - VLAN30 – Usuarios administrativos  
  - VLAN40 – Invitados  
- **Firewall:** WatchGuard FireboxV  
- **Servicios permitidos:** DNS, LDAP, Kerberos, SMB, RPC, HTTP/HTTPS

---
![Políticas configuradas en WatchGuard](../imagenes/politicas-firewall.png)

### 🔐 Políticas de Firewall aplicadas.

| VLAN Origen | Destino (VLAN20) | Servicios permitidos                          |
|-------------|------------------|-----------------------------------------------|
| VLAN10      | Servidor AD      | DNS (53), LDAP (389), HTTP/HTTPS (80/443)     |
| VLAN30      | Servidor AD      | DNS, LDAP, Kerberos (88), SMB (445), RPC (135), HTTP/HTTPS |
| VLAN40      | Bloqueada        | Ningún servicio permitido (todo el tráfico denegado) |

---

### 🔧 Procedimiento.

### 🖼️ Evidencia: Políticas del firewall.

![Políticas configuradas en WatchGuard](../imagenes/politicas-firewall.png)

### 🖼️ Evidencia: Ping desde VLAN10 al servidor AD.

![Respuesta de ping desde VLAN10](../imagenes/ping-vlan10-ad.png)

- Desde VLAN10 y VLAN30 puede estar permitido (según política).
- Desde VLAN40 debe estar bloqueado.

### 🖼️ Evidencia: Ping denegado de VLAN10 hacia VLAN40.

![Ping denegado de VLAN10 a VLAN40](../imagenes/ping-vlan10-a-vlan40-denegado.png)

### 🖼️ Evidencia: Acceso al servidor web (HTTP/HTTPS).

![Acceso exitoso al servidor web](../imagenes/acceso-web-server.png)
