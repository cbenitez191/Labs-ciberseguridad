# 🧪 Validación y Pruebas Realizadas – RDP Access Policy.

## 🎯 Objetivo.

Verificar que la política de acceso remoto por RDP se aplique correctamente en los equipos del dominio, limitando el acceso a usuarios autorizados y redes definidas, con registro de auditoría y cumplimiento del principio de mínimo privilegio según **ISO/IEC 27001**.

---

## 1. Verificar aplicación de GPO.

<p align="center">
  <img src="./img/longitud contraeña.png" width="800px">
</p>


**Comando en estación cliente:**
```powershell
gpresult /r
```

### 📌 Validación:

- Confirmar que la GPO RDP Access Policy esté aplicada correctamente.

## 2. Confirmar habilitación de RDP.

```plaintext
System Properties > Remote > Allow remote connections
```
### 📌 Validación:

- RDP debe estar habilitado (checkbox marcado).
- Política de GPO debe estar activa (no editable localmente).


## 3. Verificar grupo Remote Desktop Users.

```powershell
net localgroup "Remote Desktop Users"
```

### 📌 Validación:

- Solo los usuarios autorizados deben aparecer en el grupo.
- Usuarios no autorizados deben ser excluidos.

## 4. Intento de conexión desde IP autorizada.


### 📌 Validación:

- Desde un host en la VLAN de administración (10.10.30.x), conectarse por RDP.
- ✅ Acceso permitido si el usuario pertenece al grupo.


## 5. Intento de conexión desde IP no autorizada.

### 📌 Validación:

- Desde una red no permitida (ej. VLAN de invitados), intentar conexión RDP.
- ❌ Acceso debe ser rechazado por regla de firewall.

## 6. Verificar eventos de auditoría.

```plaintext
Event Viewer > Windows Logs > Security
```

### 📌 Eventos esperados:

- ID 4624: Inicio de sesión exitoso
- ID 4625: Intento fallido de inicio de sesión
- ID 4778/4779: Sesión iniciada o finalizada por RDP

---
## 🔎 Comandos utilizados.

```powershell
gpupdate /force
gpresult /r
net localgroup "Remote Desktop Users"
Get-NetFirewallRule -DisplayName "*RDP*"
```

## ✅ Conclusión.

La política fue validada exitosamente. Se comprobó que:

- El acceso remoto por RDP solo es posible desde redes autorizadas.
- Solo usuarios previamente definidos pueden conectarse.
- Todos los accesos están debidamente auditados y registrados.
- Se refuerza así el cumplimiento de los controles A.9.2.3, A.9.4.2 y A.12.4.1 de ISO/IEC   27001, aplicando el principio de mínimo privilegio y manteniendo visibilidad sobre el uso del Escritorio Remoto