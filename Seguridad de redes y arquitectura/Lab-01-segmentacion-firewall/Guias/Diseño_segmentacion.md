# 🧱 Diseño de segmentación de red.

## 📐 Topología de red.

La siguiente imagen muestra el diseño lógico de la red segmentada, incluyendo los enlaces entre el firewall, el switch y las diferentes VLANs:

(ver `/imagenes/topologia_red.png`)


## 🎯 Objetivo.

Implementar una arquitectura de red segmentada que permita mejorar la seguridad, organización y eficiencia de los recursos tecnológicos, aplicando el principio de mínimo privilegio y facilitando la administración del tráfico mediante VLANs y políticas de firewall.

## 🎯 Justificación.

La segmentación reduce la superficie de ataque y evita que un equipo comprometido tenga acceso libre a toda la red. Cada segmento se aísla y se controla mediante el firewall.

La segmentación de red permite:

- Limitar el movimiento lateral de amenazas dentro de la red.
- Aislar sistemas críticos de otros menos confiables.
- Aplicar reglas de acceso más estrictas por segmento.
- Mejorar la visibilidad y el control del tráfico.
- Reducir la superficie de ataque frente a intrusiones.

---

## 🔧 Descripción de VLANs y subredes.

La red se dividió en cinco segmentos lógicos utilizando VLANs, cada uno con su propia subred y propósito específico:

| VLAN | Nombre           | Subred           | Propósito                 |
|------|------------------|------------------|---------------------------|
| 10   | VLAN 10          | 10.10.10.0/28    | PCs user                  |
| 20   | VLAN 20          | 10.10.20.0/28    | PCs user                  |
| 30   | VLAN 30          | 10.10.30.0/25    | PCs user                  |
| 40   | VLAN 40          | 10.10.40.0/29    | Servidores                |


## 🧑‍🔧 Criterios de asignación.

- Cada VLAN fue asignada a puertos físicos específicos en el switch (ver guía de configuración).
- Los dispositivos fueron configurados manualmente o mediante DHCP según el segmento.
- El firewall actúa como puerta de enlace para todas las VLANs y gestiona el tráfico entre ellas.

## 📌 Buenas prácticas aplicadas.

- Separación de roles y funciones por VLAN.
- Control de acceso inter-VLAN mediante firewall.
- Regla final de denegación (“deny all”) para tráfico no explícitamente permitido.
- Registro de tráfico permitido y bloqueado en el firewall.

---

## ✅ Resultado esperado

Una infraestructura segmentada, con cada red aislada lógicamente y únicamente con los accesos estrictamente necesarios habilitados mediante reglas de firewall.
