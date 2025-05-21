# 📘 Configuración de Políticas de Contraseñas vía GPO.

## 🎯 Objetivo

Integrar políticas robustas de contraseñas mediante Directivas de Grupo (GPO) en el entorno ya desplegado, con el fin de reforzar el control de acceso y alinear la infraestructura a los requisitos de **ISO/IEC 27001**, **NIST SP 800-53** y **CIS Controls v8**.

Este procedimiento se aplica sobre un entorno operativo compuesto por:
- 🔐 Firewall implementado y segmentación activa
- 🎛️ Switch MikroTik configurado con VLANs
- 👥 Usuarios conectados a dominio desde Windows 10
- 🖥️ Controlador de dominio en Windows Server 2022

## 🛠️ Procedimiento de Configuración.

### 1. Acceder a la Consola GPMC.

En el controlador de dominio, abrir la consola:

```powershell
gpmc.msc
```

### 2. Crear y vincular la GPO.

- Selecciona la OU que contiene a los usuarios o utiliza `Group Policy Objects`.
- Clic derecho → Crear GPO, la vinculas al OU o desde el grupo de políticas la direccionas.
- Nombre sugerido: `Password Policy`

>⚠️ Asegúrate de vincular solo a OUs de usuarios finales, no a cuentas administrativas o de servicio.

### 3. Configurar directiva de contraseñas

<p align="center">
  <img src="./img/Password Policy.png" width="800px">
</p>

Ruta dentro de la GPO:

```python
Computer Configuration/Policies/Windows Settings/Account Policies
> Password Policy
```

| Política                          | Valor                  |
| --------------------------------- | ---------------------- |
| Longitud mínima de la contraseña  | 20 caracteres          |
| Requisitos de complejidad         | Habilitado             |
| Historial de contraseñas          | 24 contraseñas previas |
| Duración mínima de la contraseña  | 1 día                  |
| Duración máxima de la contraseña  | 60 días                |
| Cifrado reversible de contraseñas | Deshabilitado          |


### 4. Configurar directiva de bloqueo de cuentas

<p align="center">
  <img src="./img/Password Policy2.png" width="800px">
</p>

Ruta dentro de la GPO:

```python
Computer Configuration/Policies/Windows Settings/Account Policies
> Account Lockout Policy
```

| Política                              | Valor                |
|---------------------------------------|----------------------|
| Umbral de bloqueo de cuenta           | 3 intentos fallidos  |
| Duración del bloqueo                  | 30 minutos           |
| Restablecer contador de bloqueo       | 30 minutos           |
| Permitir el bloqueo de cuenta admin   | Habilitado (`Enabled`) |

### 5. Habilitar la auditoría de eventos de seguridad en GPO.

<p align="center">
  <img src="./img/gpo auditoria.png" width="800px">
</p>

Ruta dentro de la GPO:

```python
Computer Configuration/Policies/Windows Settings/Local Policy
> Audit Policy
```
| Política                                          | Valor         |
| ------------------------------------------------- | ------------- |
| **Auditar eventos de inicio de sesión de cuenta** | Éxito y error |
| **Auditar eventos de inicio de sesión**           | Éxito y error |
| **Auditar acceso a servicios de directorio**      | Éxito         |
| **Auditar cambio de cuenta de usuario**           | Éxito y error |

📌 Esto activará el registro de eventos como:

- 4720 – Creación de cuenta
- 4723 – Cambio de contraseña
- 4740 – Bloqueo de cuenta
- 47234624/4625 – Inicios de sesión correctos/fallidos

## 🔒 Resumen de Políticas de Contraseña Configuradas

| Nº  | Política                                       | Valor Configurado          | Objetivo de Seguridad                                          | ISO/IEC 27001 (Anexo A)              |
|-----|------------------------------------------------|-----------------------------|----------------------------------------------------------------|---------------------------------------|
| 1   | Longitud mínima de la contraseña.               | 20 caracteres               | Aumentar la entropía de la contraseña.                         | A.9.2.1 – Gestión de credenciales     |
| 2   | Requisitos de complejidad.                      | Habilitado                  | Forzar uso de mayúsculas, minúsculas, números, símbolos.       | A.9.2.1 – Gestión de credenciales     |
| 3   | Historial de contraseñas.                       | 24 contraseñas anteriores   | Prevenir reutilización de contraseñas.                         | A.9.2.1 – Gestión de credenciales     |
| 4   | Duración mínima de la contraseña.               | 1 día                       | Evitar cambios sucesivos para eludir el historial.             | A.9.2.4 – Gestión del acceso de usuarios |
| 5   | Duración máxima de la contraseña.               | 60 días                     | Reforzar la renovación periódica.                              | A.9.4.2 – Control de acceso del sistema |
| 6   | Umbral de bloqueo de cuenta.                    | 3 intentos fallidos         | Prevenir ataques de fuerza bruta.                              | A.9.4.3 – Gestión del uso del sistema  |
| 7   | Duración del bloqueo de cuenta.                 | 30 minutos                  | Limitar intentos tras bloqueo.                                 | A.9.4.3 – Gestión del uso del sistema  |
| 8   | Restablecer contador de bloqueo.                | 30 minutos                  | Reiniciar intentos tras período de espera.                     | A.9.4.3 – Gestión del uso del sistema  |
| 9   | Cifrado reversible de contraseñas.              | Deshabilitado               | Evitar almacenamiento inseguro de contraseñas.                 | A.10.1.1 – Política de uso de cifrado  |
| 10  | Auditoría de cambios y bloqueos (eventos).      | ID 4723, 4740               | Registrar eventos en el visor de seguridad del sistema.        | A.12.4.1 – Registro de eventos         |

## 🧠 Nota.

Las políticas de contraseñas implementadas mediante GPO en entornos Windows Server sí constituyen controles de acceso, ya que afectan directamente los mecanismos de autenticación dentro de la organización.

Estas políticas:

- Fortalecen la seguridad en el inicio de sesión (contraseñas seguras, complejidad, rotación).
- Ayudan a prevenir accesos no autorizados mediante bloqueos y límites de intentos.
- Se alinean a los controles del Anexo A de ISO/IEC 27001, especialmente al dominio A.9 - Control de acceso.
- No reemplazan controles de autorización (permisos, roles, ACLs), pero los complementan eficazmente.

>📌 Por tanto, aplicar estas políticas forma parte del cumplimiento técnico y normativo en la gestión segura del acceso a sistemas y datos.
---
