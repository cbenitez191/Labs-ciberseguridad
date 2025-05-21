# 🔐 Implementación de Políticas de Contraseñas y GPO en Windows Server

<p align="center">
  <img src="./img/Arbol GPO.png" width="800px">
</p>

## 🎯 Propósito

Este laboratorio tiene como finalidad diseñar y aplicar políticas de contraseñas seguras utilizando Directivas de Grupo (GPO) en un entorno de dominio con Windows Server, alineando la configuración a estándares reconocidos como ISO/IEC 27001, NIST SP 800-53 e ISO/IEC 27002.

## 🧱 Entorno Técnico

- Controlador de Dominio: Windows Server 2019/2022  
- Estaciones cliente: Windows 10 / 11  
- Herramientas utilizadas:  
  - Group Policy Management Console (GPMC)  
  - RSOP (Resultant Set of Policy)  
  - Visor de eventos  
  - Línea de comandos (`gpupdate`, `gpresult`)  

## 🗂️ Estructura del Proyecto

```python
Lab-GPO-PasswordPolicy/
├── README.md                  # Documentación general del laboratorio
├── Guia_Configuracion_GPO.md  # Guía técnica paso a paso
├── Pruebas_Realizadas.md      # Evidencia de validación y resultados
└── img/                       # Capturas del entorno y configuración
```

## ⚙️ Objetivos Específicos

- Configurar políticas de contraseñas seguras en GPO  
- Aplicar directivas por Unidad Organizativa (OU)  
- Validar el correcto despliegue en estaciones cliente  
- Auditar eventos relacionados con bloqueos de cuenta y cambios de credenciales  
- Asegurar cumplimiento de normativas de seguridad  

## 📜 Normas y Controles Aplicados

- **ISO/IEC 27001** - A.9.2.1: Gestión de credenciales de usuario  
- **NIST SP 800-53 Rev. 5** - IA-5: Authenticator Management  
- **CIS Controls v8** - Control 5: Account Management  

## 🛡️ Buenas Prácticas Recomendadas

- Contraseñas con mínimo de 12 caracteres  
- Activar complejidad de contraseña (letras, números, símbolos)  
- Bloqueo automático tras intentos fallidos  
- Auditoría de cambios de contraseña  
- Pruebas en entorno controlado antes de aplicar en producción  

---

> Este proyecto forma parte de un ejercicio práctico orientado al fortalecimiento de controles de acceso y gestión segura de identidades en entornos Windows empresariales.

>👤 Autor: Carlos Benítez  
>📅 Fecha: 2025-05-21  
>🔐 Proyecto: CbTech.sec – Seguridad de red.