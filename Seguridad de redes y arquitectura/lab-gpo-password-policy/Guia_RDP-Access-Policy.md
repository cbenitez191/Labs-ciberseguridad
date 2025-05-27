# 📘 RDP Access Policy – Directiva de Acceso por Escritorio Remoto.

## 🎯 Objetivo.

Establecer una política de seguridad para controlar el uso del protocolo de Escritorio Remoto (RDP) dentro del entorno corporativo, asegurando que solo usuarios autorizados y desde redes confiables puedan conectarse remotamente a los equipos del dominio.

Esta política se aplica a:

- Todos los equipos bajo control de Active Directory (servidores y estaciones Windows 10/11).
- Usuarios que requieren acceso remoto para tareas administrativas o de soporte técnico.
- Segmentos de red definidos como confiables (ej. VLAN de administración).

La política limita:

- El acceso por RDP únicamente a miembros de grupos autorizados (`Remote Desktop Users`).
- Las conexiones remotas al puerto TCP 3389 desde redes específicas.
- El uso no supervisado o no autorizado del Escritorio Remoto, alineándose con buenas prácticas de seguridad y cumplimiento normativo.

---

## 🧱 Entorno Aplicable.

- Controlador de Dominio: Windows Server 2022  
- Clientes: Estaciones con Windows 10  
- Infraestructura segmentada por VLAN  
- Firewall y GPO ya en funcionamiento

## ✅ ¿Qué permite esta política?

1. Acceso remoto controlado a través de RDP (Remote Desktop Protocol) hacia equipos del     dominio, únicamente por usuarios autorizados.
2. La posibilidad de conectarse remotamente a servidores o estaciones de trabajo, pero solo si:

- El usuario pertenece al grupo Remote Desktop Users (o un grupo personalizado autorizado).
- La conexión proviene desde una red o segmento autorizado (por ejemplo, VLAN de  administración).
- El equipo tiene habilitado RDP mediante GPO.

3. El uso de firewall y auditoría para:

- Permitir conexiones RDP solo desde IPs confiables.
- Registrar eventos de inicio de sesión exitoso y fallido en el visor de eventos para trazabilidad.


---

## 🛠️ Configuración mediante GPO.

### 1. Crear la GPO.

- Abrir `gpmc.msc`
- Crear una nueva GPO con nombre sugerido: `RDP Access Policy`
- Vincularla a la OU que contiene los equipos donde se aplicará

---

### 2. Habilitar RDP solo en estaciones seleccionadas.

```python
Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Deskyop Sesion Host/Connections

> Allow users to connect remotely by using Remote Desktop Services → `Enabled`
```

### 3. Limitar acceso RDP solo a miembros de un grupo.

```python
Computer Configuration/Windows Settings/Segurity Settings/Restricted Groups

> Agregar el grupo `Remote Desktop Users` y establecer que solo miembros autorizados (ej. `SoporteTI`) estén incluidos.
```

### 4. Controlar firewall para RDP.

```python
Computer Configuration/Policies/Windows Settings/Segurity Settings/Windows Defender Firewall with Advance Security -LDA

- Crear una regla para permitir TCP puerto `3389` únicamente desde IPs confiables (ej. segmento de administración).
- También puede configurarse mediante:
  > powershell
  New-NetFirewallRule -DisplayName "Allow RDP - Administración" -Direction Inbound -Protocol TCP -LocalPort 3389 -RemoteAddress 10.10.20.3/24 -Action Allow

```

## 5. Auditoría de Accesos por RDP. 

```python
Computer Configuration/Windows Settings/Segurity Settings/Advanced Audit Policy Configuration 

> Logon/Logoff > Audit Logon (Success y Failure)
```

Validar eventos en el visor:

- ID 4624: Inicio de sesión exitoso
- ID 4625: Fallo de inicio de sesión