# 🛡️ Implementación de Políticas de Seguridad con GPO – Windows Server.

<p align="center">
  <img src="./img/Arbol GPO.png" width="800px">
</p>

## 🎯 Objetivo.

Aplicar una serie de políticas de seguridad en un entorno de dominio Windows Server mediante el uso de directivas de grupo (GPO), centralizando el control desde una o varias políticas organizadas. Esta implementación busca fortalecer la postura de seguridad de las estaciones cliente y servidores, alineándose con los controles de acceso y protección del dominio **A.9** y **A.12** de la norma **ISO/IEC 27001**.



## 🧱 Entorno Técnico.

- Controlador de Dominio: Windows Server 2019/2022  
- Estaciones cliente: Windows 10 / 11  
- Herramientas utilizadas:  
  - Group Policy Management Console (GPMC)  
  - RSOP (Resultant Set of Policy)  
  - Visor de eventos  
  - Línea de comandos (`gpupdate`, `gpresult`)  

## 🗂️ Estructura del Proyecto.

```python
Lab-GPO-PasswordPolicy/
├── README.md                  # Documentación general del laboratorio
├── Guia_Configuracion_GPO.md  # Guía técnica paso a paso
├── Pruebas_Realizadas.md      # Evidencia de validación y resultados
└── img/                       # Capturas del entorno y configuración
```

## 🛠️ Alcance y configuración

Todas las configuraciones se aplican desde GPOs creadas en el servidor de dominio. Se inició con una política base denominada `Password Policy`, y se continuará ampliando con otras políticas específicas como:

- `RDP Access Policy`
- `SQL Access Restrictions`
- `Desktop Restrictions Policy`
- `Control Panel Lockdown`
- Entre otras.

## 🔒 Políticas implementadas (actuales y planificadas)

| Nº  | Categoría                          | Descripción resumida                                               |
|-----|------------------------------------|---------------------------------------------------------------------|
| 1   | Contraseña                         | Longitud mínima, complejidad, vencimiento, historial                |
| 2   | Bloqueo de cuenta                  | Intentos fallidos, duración del bloqueo, contador                   |
| 3   | Auditoría de eventos               | Registro de cambios de contraseña, bloqueos de cuenta               |
| 4   | Control de sesión remota (RDP)     | Permitir o denegar RDP solo a grupos autorizados                    |
| 5   | Restricciones a SQL Server         | Limitar accesos desde estaciones específicas                        |
| 6   | Personalización del escritorio     | Bloqueo de cambio de fondo de pantalla                              |
| 7   | Panel de control y configuración   | Deshabilitar acceso a herramientas administrativas                  |
| 8   | Registro de eventos                | Activación de auditoría para inicios de sesión y cambios críticos   |


## 🧪 Validación y Evidencias

Se realizaron pruebas prácticas desde estaciones cliente para confirmar la aplicación efectiva de las políticas:

- Uso de `gpresult /r` y `rsop.msc` para validar la aplicación de GPO
- Verificación de eventos en el visor (`eventvwr.msc`)
- Capturas de pantalla como evidencia de cambios aplicados
- Reportes generados (`gpresult /h`) como respaldo técnico

## 📌 Beneficios de la implementación

- Centralización del control de seguridad
- Reducción de superficie de ataque en estaciones cliente
- Cumplimiento de buenas prácticas y normativa internacional
- Mejora de la trazabilidad y auditoría del entorno Windows


## 🔗 Referencias

- [Microsoft – Group Policy Overview](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/gpresult)
- [ISO/IEC 27001:2013 – Controles A.9 y A.12](https://www.iso.org/standard/54534.html)

✅ **Todas las configuraciones son gestionadas mediante GPO, con enfoque modular para facilitar mantenimiento, escalabilidad y cumplimiento normativo.**

---

👤 Autor: Carlos Benítez  
📅 Fecha: 2025-05-21  
🔐 Proyecto: CbTech.sec – Seguridad de red.