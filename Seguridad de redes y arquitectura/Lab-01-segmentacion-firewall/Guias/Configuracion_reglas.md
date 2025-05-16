# 🔥 Configuración de Reglas de Firewall

## 🎯 Objetivo

Definir reglas precisas en el firewall WatchGuard que controlen el tráfico entre las VLANs segmentadas, permitiendo solo las comunicaciones necesarias bajo el principio de mínimo privilegio.

---

## 🔐 Principios aplicados

- **Mínimo privilegio:** El acceso entre VLANs solo se permite si es requerido y justificado.
- **Segmentación lógica:** Cada VLAN tiene su rol específico (usuarios, CCTV, servidores, etc.).
- **Regla final de denegación:** Todo lo que no está explícitamente permitido, está bloqueado.
- **Monitoreo activado:** Todas las reglas relevantes tienen habilitado el log para auditoría.

---

## 📋 Reglas configuradas (resumen)

| Nº | Acción  | Política                           | Desde                  | Hacia                    | Servicio(s)                         |
|----|---------|-------------------------------------|------------------------|--------------------------|-------------------------------------|
| 1  | Permitir| HTTP/HTTPS Proxy                   | VLAN10, VLAN20, VLAN30 | Any-External             | tcp:80 / tcp:443                    |
| 2  | Denegar | Deny inter-VLAN (varias reglas)    | VLAN10–40 entre sí     | VLAN10–40 entre sí       | Any                                 |
| 3  | Permitir| DNS hacia Internet o VLAN99        | VLAN10–30, VLAN99      | Any-External, VLAN99     | tcp/udp:53                          |
| 4  | Permitir| Ping general                       | VLAN10–30              | Any                      | ICMP                                |
| 5  | Permitir| DNS/LDAP/SMB desde VLANs al AD     | VLAN10–40              | VLAN20 (AD)              | tcp/udp:53, 389, 445                |
| 6  | Permitir| Kerberos/RPC desde VLANs al AD     | VLAN10–40              | VLAN20 (AD)              | tcp/udp:88, 135                     |
| 7  | Permitir| RPC Dynamic                        | VLAN10–40              | VLAN20 (AD)              | tcp/udp:49152–65535                 |
| 8  | Permitir| HTTP/HTTPS hacia el AD             | VLAN10–40              | VLAN20                   | tcp:80, 443                         |
| 9  | Permitir| VPN (IKEv2-Users) hacia AD         | IKEv2-Users            | VLAN20 (10.10.20.3)      | DNS, HTTP, LDAP, Kerberos, SMB...  |
| 10 | Denegar | Denegar resto de tráfico VPN       | IKEv2-Users            | VLAN20                   | Any                                 |

---

## 🧪 Observaciones clave

- Existen múltiples **reglas de denegación explícita** entre VLANs como mecanismo de control fuerte.
- Se habilitan servicios mínimos por VLAN hacia el AD (como DNS, LDAP, SMB, Kerberos) para autenticación.
- Los usuarios remotos vía VPN (IKEv2) tienen permisos específicos, no acceso total.
- El **logging está activado** para todas las reglas críticas, facilitando auditoría de tráfico.

---

## 🧠 Ejemplo de regla detallada

**Nombre de la política:** `Allow_LDAP_to_AD_VLAN30`  
**Origen:** VLAN30  
**Destino:** VLAN20 (Servidor AD)  
**Servicio:** LDAP (tcp:389 udp:389)  
**Acción:** Allow  
**Comentario:** Permite autenticación LDAP desde VLAN30 hacia el AD  
**Logging:** Habilitado  

---

## 📸 Capturas asociadas

- 📷 Políticas activas en WatchGuard: `imagenes/reglas_firewall.png`
- 📷 Validaciones de tráfico desde VLAN10 hacia VLAN30 mostrando denegación

---

## ✅ Resultado esperado

- Solo se permite comunicación necesaria según el rol de cada VLAN.
- Todo el tráfico no autorizado es bloqueado y registrado.
- El diseño cumple con el principio de mínimo privilegio y segmentación segura.

