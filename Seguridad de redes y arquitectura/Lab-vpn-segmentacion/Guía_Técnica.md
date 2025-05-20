# 🔐 Laboratorio: Implementación de VPN con Segmentación y Monitoreo.

## 🎯 Objetivo

Configurar una VPN segura (IKEv2/OpenVPN), aplicar segmentación por VLAN y validar el tráfico autorizado mediante reglas de firewall y análisis de logs.

---

## 🧪 Entorno del Laboratorio

- **Firewall:** WatchGuard (o pfSense)
- **Red Interna VLANs:**
  - VLAN10 – Usuarios (`10.10.10.0/28`)
  - VLAN20 – Servidores (`10.10.20.0/29`)
  - VLAN30 – Administración (`10.10.30.0/28`)
  - VLAN40 – Invitados (`10.10.40.0/28`)
- **VPN Pool:** `10.10.99.0/29`
- **Cliente VPN:** Windows/Linux

---

## 🔧 Fase 1: Preparación.

1. Identificar y documentar la estructura de red y VLANs.
2. Configurar direccionamiento IP interno para la VPN.
3. Tener control del firewall o servidor VPN.

---

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

3. En la sección **IKEv2**, haz clic en el botón:
![Descarga perfil cliente](./img/Configuración%20VPN%20Mobile.png)

4. Guarda el archivo ZIP que contiene:
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

---

## 🧩 Fase 3: Segmentación de Acceso.

### 🔒 Reglas de Firewall.

![Póliticas segmentadas VPN](./img/Politicas%20VPN.png)

✅ Permitir: VPN → VLAN20 (puertos específicos)

❌ Denegar: VPN → VLAN10, VLAN30, VLAN40

### 🌐 Servicios habilitados.

- DNS (53)
- LDAP (389)
- RDP (3389)
- SMB (445)
- HTTP/HTTPS (80/443)

---

## 🧪 Fase 4: Validación del Acceso.

Desde el cliente conectado a la VPN, realiza las siguientes pruebas para verificar el control de acceso segmentado:

```bash
ping 10.10.20.3         # Acceso permitido (Servidor en VLAN20)
ping 10.10.10.5         # Acceso denegado (Usuario en VLAN10)
nmap -Pn 10.10.20.3     # Verificar puertos abiertos
nslookup ad.local       # Confirmar resolución DNS

---

### 📊 Fase 5: Monitoreo y Logs

- Habilitar el logging en todas las reglas del firewall relacionadas con la VPN.
- Registrar eventos de acceso permitido y acceso denegado.
- (Opcional) Enviar los logs a un servidor externo como Syslog, Wazuh o Graylog para análisis centralizado.

```bash
Ejemplo de registros:

2025-05-19 10:15:22 - VPN user carlos.b - acceso a 10.10.20.3:3389
2025-05-19 10:15:35 - intento bloqueado a 10.10.10.5

---