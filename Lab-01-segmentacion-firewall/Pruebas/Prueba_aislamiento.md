# 🧪 Prueba de Aislamiento entre VLANs

## 🎯 Objetivo

Verificar que el tráfico entre VLANs se encuentra correctamente restringido según las políticas de firewall aplicadas, garantizando el aislamiento lógico y cumplimiento del principio de mínimo privilegio.

---

## 🧪 Entorno

- VLAN10 – Administración (PC técnico)
- VLAN30 – Usuarios
- VLAN40 – Invitados
- Firewall WatchGuard con reglas explícitas de denegación entre VLANs

---

## 🔧 Procedimiento

Desde un equipo ubicado en VLAN10 (IP: 192.168.10.10), se ejecutan pruebas de conectividad hacia otras VLANs (por ejemplo, VLAN30 y VLAN40) usando herramientas de red como `ping` y `nmap`.

### 1. Prueba de ping (ICMP)

```bash
ping 192.168.30.10
ping 192.168.40.10
