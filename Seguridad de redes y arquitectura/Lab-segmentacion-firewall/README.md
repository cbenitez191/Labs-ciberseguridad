# 🧱 Segmentación de red y Reglas de Firewall.
## 🕸️ Topología de red

<p align="center">
  <img src="imagenes/Topologia de red.png" width="600px">
</p>

Este laboratorio demuestra cómo aplicar segmentación de red utilizando VLANs y establecer reglas de firewall basadas en el principio de mínimo privilegio. Forma parte de mi portafolio de ciberseguridad práctica.

## 🎯 Objetivos
- Dividir una red en múltiples segmentos (VLANs)
- Crear reglas específicas en el firewall
- Aislar tráfico no autorizado y permitir solo lo necesario
- Verificar comunicación entre segmentos

## 🧰 Herramientas utilizadas.
- Switch MikroTik (RouterOS)
- Firewall WatchGuard
- Equipos virtuales (Windows server, Windows, RouterOs, FireboxV.)

## 🧠 Principios aplicados.
- Mínimo privilegio
- Defense in depth (defensa en capas)
- Zero Trust (confianza cero)

## 📂 Estructura.

```bash
/lab-13-segmentacion-firewall
├── README.md
├── /guias
│   ├── instalacion_entorno_virtual.md
│   ├── configuracion_vlan_mikrotik.md
│   └── configuracion_reglas_firewall.md
├── /pruebas
│   ├── prueba_aislamiento.md
│   └── prueba_acceso_controlado.md
├── /imagenes
│   ├── topologia_red.png
│   ├── reglas_firewall.png
│   └── nmap_resultados.png
```
---

👤 Autor: Carlos Benítez  
📅 Fecha: 2025-05-19  
🔐 Proyecto: CbTech.sec – Seguridad de red.
