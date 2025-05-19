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
### 🔐 Políticas de Firewall aplicadas.

| VLAN Origen | Destino (VLAN20) | Servicios permitidos                          |
|-------------|------------------|-----------------------------------------------|
| VLAN10      | Servidor AD      | DNS (53), LDAP (389), HTTP/HTTPS (80/443)     |
| VLAN30      | Servidor AD      | DNS, LDAP, Kerberos (88), SMB (445), RPC (135), HTTP/HTTPS |
| VLAN40      | Bloqueada        | Ningún servicio permitido (todo el tráfico denegado) |

---

### 🖼️ Evidencia: Políticas del firewall.

<p align="center">
  <img src="../imagenes/Politicas firewall 1.png" width="800px">
</p>

 📌 **Descripción:** Captura del panel de políticas del firewall WatchGuard. Se observan las reglas configuradas para controlar el acceso por VLAN, permitiendo servicios específicos únicamente a VLAN10 y VLAN30. VLAN40 se encuentra explícitamente bloqueada para evitar cualquier tipo de comunicación hacia el servidor AD.
 
### 🖼️ Evidencia: Ping desde VLAN40 al servidor AD.

<p align="center">
  <img src="../imagenes/Comunicacion vlan 40 a vlan 20.png" width="800px">
</p>

> 📌 **Descripción:** Resultado exitoso de una prueba de conectividad ICMP (ping) desde una máquina en VLAN40 hacia el servidor AD (10.10.20.3). Valida que la política del firewall permite el tráfico desde esta red hacia el servidor.

---
- Desde VLAN10 y VLAN30 puede realizar ping ala red de servidores de acuerdo con las políticas.
- Desde las VLAN (10,30,40) debe estar bloqueada la comunicación .

### 🖼️ Evidencia: Ping denegado de VLAN10 hacia VLAN40.

<p align="center">
  <img src="../imagenes/Comunicacion vlan 10 y vlan 40 off.png" width="800px">
</p>

> 📌 **Descripción:** Captura del acceso exitoso a un servidor web (HTTP/HTTPS) alojado en el servidor AD desde una estación cliente. Confirma que los servicios HTTP/HTTPS han sido permitidos correctamente en el firewall para las VLAN autorizadas.

---

### 🖼️ Evidencia: Acceso al servidor web (HTTP/HTTPS).

<p align="center">
  <img src="../imagenes/Conexion VPN user 1 acces HTTP.png" width="800px">
</p>

> 📌 **Descripción:** Captura del acceso exitoso a un servidor web (HTTP/HTTPS) alojado en el servidor AD desde una estación cliente. Confirma que los servicios HTTP/HTTPS han sido permitidos correctamente en el firewall para las VLAN autorizadas.

---
