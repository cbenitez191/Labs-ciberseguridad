# 🌐 Configuración de VLANs en Switch y Firewall

## 🎯 Objetivo

Configurar correctamente las VLANs en el switch y el firewall para lograr una segmentación efectiva de la red, asegurando que cada dispositivo esté aislado según su función y ubicación lógica dentro de la infraestructura.

---

## 🛠 Dispositivos utilizados

- **Switch:** MikroTik (RouterOS v6)
- **Firewall:** WatchGuard Firebox (administración básica desde Web UI)
- **Clientes:** PCs y cámaras conectados a puertos físicos

---

## 🧱 VLANs definidas

| VLAN | Nombre         | Subred           | Puertos asignados (ejemplo) |
|------|----------------|------------------|-----------------------------|
| 10   | VLAN 10        | 10.10.10.0/28    | ether2, ether3              |
| 20   | VLAN 20        | 10.10.20.0/28    | ether4                      |
| 30   | VLAN 30        | 10.10.30.0/25    | ether5                      |
| 40   | VLAN 40        | 10.10.10.0/29    | ether6                      |


---

## 🔧 Configuración en MikroTik

### 1. Crear las VLANs

Ir a: **Interfaces → VLANs → Add (+)**

Crear una VLAN por cada red, especificando:
- `Name`: vlan10, vlan20, etc.
- `VLAN ID`: según tabla
- `Interface`: ether1 (conectado al firewall)

### 2. Activar VLAN Filtering en el bridge

Ir a: **Bridge → Configuración**
- Marcar `Use IP Firewall`
- Activar `VLAN Filtering`

### 3. Asignar puertos al bridge y etiquetar

Ejemplo para Administración:

- ether2 (sin tag): puerto de acceso
- ether1 (trunk): pasa todas las VLANs al firewall

Ir a: **Bridge → Ports**
- ether2: pvid=10
- ether1: trunk, tagged con todas las VLANs

---

## 🔥 Configuración en el Firewall WatchGuard

### 1. Crear interfaces VLAN

Ir a: **Network → Interfaces → Add → VLAN**

Para cada VLAN:
- Asignar nombre y VLAN ID correspondiente
- Especificar interfaz física (ej. eth1)
- Asignar IP gateway de la subred (ej. 192.168.10.1/24 para VLAN 10)
- Marcar `Enable DHCP` si deseas que el firewall asigne IPs

### 2. Verificar rutas

El firewall debe tener una ruta para cada subred creada. Normalmente se configuran automáticamente.

---

## 🔌 Verificación

### Desde un equipo en cada VLAN:

```bash
ipconfig (Windows) / ip a (Linux)
ping <gateway de la VLAN>
