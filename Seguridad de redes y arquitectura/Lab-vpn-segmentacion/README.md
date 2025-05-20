# 🔐 Laboratorio: VPN con Segmentación y Monitoreo

<p align="center">
  <img src="img/vpn.png" width="800px">
</p>
Este laboratorio demuestra cómo implementar una solución de acceso remoto segura utilizando VPN (IKEv2/OpenVPN), aplicando segmentación de red mediante VLANs y monitoreando el tráfico autorizado y denegado a través de reglas de firewall y análisis de logs.

> 🧠 **Propósito:** Simular un entorno empresarial que asegure la conectividad remota con principios de mínimo privilegio y control de acceso.

---

## 🎯 Objetivos Específicos

- Implementar una VPN funcional para conexión remota de usuarios.
- Restringir el acceso a la red interna según la VLAN de destino.
- Validar el tráfico permitido con herramientas de red.
- Registrar y analizar intentos de conexión exitosos y fallidos.

---

## 🧪 Componentes del Entorno

| Componente | Descripción |
|------------|-------------|
| 🔐 VPN Server | IKEv2 en WatchGuard / OpenVPN en Linux |
| 🌐 VLANs | Segmentación por tipo de usuario y servicio |
| 🧱 Firewall | Reglas por subred y servicio |
| 📈 Logs | Auditoría de accesos remotos y tráfico |
| 🖥️ Cliente VPN | Windows 10/11 o Linux Ubuntu |

---

## 🌐 Estructura de Red

<p align="center">
  <img src="img/Diagrama conexion.png" width="800px">
</p>


## 📂 Archivos

- [`Guía_Técnica.md`](./Guía_Técnica.md): Detalle paso a paso de la implementación.
- [`Glosario.md`](./Glosario.md): Términos técnicos utilizados.

---

👤 Autor: Carlos Benítez  
📅 Fecha: 2025-05-19  
🔐 Proyecto: CbTech.sec – Seguridad de red.
