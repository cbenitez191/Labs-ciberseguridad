# 🔐 Laboratorio: Implementación de VPN con Segmentación y Monitoreo.

## 🎯 Objetivo.

Configurar una VPN segura (IKEv2/OpenVPN), aplicar segmentación por VLAN y validar el tráfico autorizado mediante reglas de firewall y análisis de logs.



## 🧪 Entorno del Laboratorio.

- **Firewall:** WatchGuard (o pfSense)
- **Red Interna VLANs:**
  - VLAN10 – Usuarios (`10.10.10.0/28`)
  - VLAN20 – Servidores (`10.10.20.0/29`)
  - VLAN30 – Administración (`10.10.30.0/28`)
  - VLAN40 – Invitados (`10.10.40.0/28`)
- **VPN Pool:** `10.10.99.0/29`
- **Cliente VPN:** Windows/Linux

## 🔧 Fase 1: Preparación.

1. Identificar y documentar la estructura de red y VLANs.
2. Configurar direccionamiento IP interno para la VPN.
3. Tener control del firewall o servidor VPN.

## 🛠️ Fase 2: Configuración del Servidor VPN.

### ▶️ En WatchGuard (IKEv2).

- Activar el servicio VPN IKEv2.
- Crear un pool de direcciones para clientes VPN: `172.16.100.0/25`.
- Generar certificado o usar CA interna.
- Agregar usuarios locales o con autenticación LDAP.
- Definir DNS interno y dominio: `10.10.20.3. Cbtech.sec`.


## 📥 Descarga del Perfil de Cliente VPN (IKEv2) desde WatchGuard.

El firewall WatchGuard permite exportar el perfil de cliente VPN IKEv2 preconfigurado, lo cual simplifica la instalación en los dispositivos cliente.

### 🧭 Pasos para descargar el perfil:

1. Ingresa al portal de administración web del firewall:
2. Dirígete a:  
**VPN > Mobile VPN > Mobile VPN**

3. En la sección **IKEv2**, haz clic en el botón **PERFIL DEL CLIENTE**:
<p align="center">
  <img src="./img/Configuración%20VPN%20Mobile.png" width="800px">
</p>

5. Guarda el archivo ZIP que contiene:
- Certificados
- Script de instalación
- Archivo de configuración `.epf` o `.mobileconfig`
5. Extrae el contenido del ZIP en el cliente Windows.
6. Ejecuta el instalador incluido o sigue el proceso de instalación manual desde: `Configuración → Red e Internet → VPN`
7. Usa las credenciales asignadas por el administrador para establecer conexión.
> ⚠️ **Nota:** Si se usa un certificado digital, este debe instalarse en el almacén de certificados de Windows antes de la conexión.

---

## ✅ Ventajas del perfil de cliente.

- Ahorra tiempo al evitar la configuración manual.
- Contiene los certificados y parámetros necesarios para una conexión segura.
- Compatible con sistemas Windows, macOS, Android (con strongSwan) y iOS.

## 🧩 Fase 3: Segmentación de Acceso.

### 🔒 Reglas de Firewall.

<p align="center">
  <img src="./img/Politicas%20VPN.png" width="800px">
</p>

✅ Permitir: VPN → VLAN20 (puertos específicos).
❌ Denegar: VPN → VLAN10, VLAN30, VLAN40.

### 🌐 Servicios habilitados.

- DNS (53)
- LDAP (389)
- RDP (3389)
- SMB (445)
- HTTP/HTTPS (80/443)


## 🧪 Fase 4: Validación del Acceso.

Desde el cliente conectado a la VPN, realiza las siguientes pruebas para verificar el control de acceso segmentado:

- Acceso permitido (Servidor en VLAN20).
- Acceso denegado (Usuario en VLAN10).
- Verificar puertos abiertos.
- Confirmar resolución DNS.


```bash
ping 10.10.20.3         
ping 10.10.10.5         
nmap -Pn 10.10.20.3     
nslookup ad.Cbetech.sec       
```

### 📊 Fase 5: Monitoreo y Logs.

- Habilitar el logging en todas las reglas del firewall relacionadas con la VPN.
- Registrar eventos de acceso permitido y acceso denegado.
- (Opcional) Enviar los logs a un servidor externo como Syslog, Wazuh o Graylog para análisis centralizado.
  

```python
Ejemplo de registros:

2025-05-21 11:52:16 Allow 172.16.100.1 10.10.20.3 dns/udp 61978 53 External VLAN20 Allowed 61 127 (Allow IKEv2-Users-DNS-00) proc_id="firewall" rc="100" msg_id="3000-0148" src_user="user1@Firebox-DB" record_type="A" question="wpad.Cbtech.sec"
2025-05-21 11:52:16 Allow 172.16.100.1 10.10.20.3 dns/udp 58178 53 External VLAN20 Allowed 63 127 (Allow IKEv2-Users-DNS-00) proc_id="firewall" rc="100" msg_id="3000-0148" src_user="user1@Firebox-DB" record_type="A" question="cbtech.cbtech.sec"
2025-05-21 11:52:16 Deny 172.16.100.1 104.89.170.158 http/tcp 49895 80 External External Denied 52 127 (Unhandled External Packet-00) proc_id="firewall" rc="101" msg_id="3000-0148" tcp_info="offset 8 S 3456553609 win 255" geo_dst="USA" src_user="user1@Firebox-DB" duration="0" sent_bytes="52" rcvd_bytes="0"
2025-05-21 11:54:58 Deny 172.16.100.1 104.89.170.143 http/tcp 49905 80 External External Denied 52 127 (Unhandled External Packet-00) proc_id="firewall" rc="101" msg_id="3000-0148" tcp_info="offset 8 S 2828439270 win 255" geo_dst="USA" src_user="user1@Firebox-DB" 2025-05-21 11:56:39 Deny 172.16.100.1 10.10.10.5 echo-request/icmp External VLAN10 Denied 60 127 (Unhandled External Packet-00) proc_id="firewall" rc="101" msg_id="3000-0148" src_user="user1@Firebox-DB" duration="0" sent_bytes="60" rcvd_bytes="0" type="8"

```


