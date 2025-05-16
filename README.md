<p align="center">
  <img src="https://github.com/cbenitez191/cbenitez191/blob/main/img/about_me.gif?raw=true" alt="About Me" width="300px">
</p>

# 🧪 Laboratorios de Ciberseguridad

Este repositorio contiene una colección de laboratorios prácticos orientados a la implementación, prueba y documentación de conceptos fundamentales en ciberseguridad ofensiva y defensiva.

Cada entorno ha sido diseñado y documentado como parte de mi proceso de aprendizaje y profesionalización en el área, aplicando buenas prácticas como la segmentación de red, principio de mínimo privilegio, y el uso de herramientas especializadas.

---

## 🎯 Objetivo del repositorio

- Consolidar y demostrar conocimientos técnicos en redes, seguridad y hacking ético.
- Practicar en entornos controlados sin riesgo legal ni de infraestructura.
- Crear contenido reutilizable como evidencia para portafolio profesional.
- Compartir configuraciones y guías con la comunidad técnica.

---

## 📂 Laboratorios disponibles

### 🧰 Preparación de entornos e instalación de herramientas.

Laboratorios orientados a la creación de entornos de práctica, instalación de sistemas operativos y herramientas clave para ciberseguridad.

| Nº  | Nombre del laboratorio                                              | Descripción breve                                                                 |
|-----|---------------------------------------------------------------------|------------------------------------------------------------------------------------|
| 01  | [Instalación de Kali Linux en VirtualBox](./lab-01-kali-virtualbox)               | Instalación paso a paso de Kali Linux como base para laboratorios de pentesting. |
| 02  | [Configuración de red interna y NAT para laboratorios](./lab-02-redes-virtualbox) | Cómo crear una red aislada para entornos de ataque y defensa en VirtualBox.      |
| 03  | [Instalación y prueba de Snort IDS](./lab-03-snort-instalacion)                   | Instalación básica de Snort como sistema de detección de intrusos y prueba de funcionamiento. |
| 04  | [Instalación de Wireshark y captura de tráfico](./lab-04-wireshark)               | Uso de Wireshark para análisis de paquetes y visualización de tráfico de red.    |
| 05  | [Instalación de Nmap y escaneos básicos](./lab-05-nmap-basico)                    | Escaneos de red y servicios para reconocimiento de objetivos.                     |
| 06  | [Instalación de Metasploit Framework](./lab-06-metasploit-instalar)               | Preparación del entorno y ejecución de pruebas locales con Metasploit.            |
| 07  | [Guía de uso de Burp Suite para interceptar tráfico web](./lab-07-burp-basico)    | Intercepción y análisis de peticiones web usando Burp Suite Community Edition.   |
| 08  | [Configuración de OpenVAS para escaneo de vulnerabilidades](./lab-08-openvas)     | Instalación y configuración inicial de OpenVAS como escáner de vulnerabilidades.  |
| 09  | [Guía práctica de Gobuster para enumeración web](./lab-09-gobuster-guia)          | Uso de Gobuster para descubrir rutas ocultas y extensiones en servidores web.     |
| 10  | [Instalación de Ubuntu Server paso a paso](./lab-10-ubuntu-server)                | Instalación y configuración inicial de Ubuntu con prácticas básicas de hardening. |
| 11  | [Instalación de Windows Server 2019 + Active Directory](./lab-11-windows-server-ad) | Instalación de Windows Server con roles de AD, DNS y configuración de red.       |
| 12  | [Creación de usuarios y políticas básicas en Windows Server](./lab-12-usuarios-gpos) | Gestión de cuentas, grupos y GPOs para control de acceso y contraseñas seguras.  |


### 🧱 Seguridad de redes y arquitectura.

| Nº  | Nombre del laboratorio                                                      | Descripción breve                                                                 |
|-----|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| 13  | [Segmentación de red y reglas de firewall](./lab-13-segmentacion-firewall) | Creación de VLANs, configuración en switch y firewall aplicando mínimo privilegio. |
| 14  | [VPN con segmentación y monitoreo](./lab-14-vpn-segmentacion)              | Configuración de VPN (IKEv2/OpenVPN), acceso segmentado y validación de tráfico con logs. |
| 15  | [Políticas de contraseñas y GPO en Windows Server](./lab-15-gpo-password-policy) | Aplicación de políticas seguras mediante GPO y endurecimiento de contraseñas. |
| 16  | [Auditoría de logs en Windows y Linux](./lab-16-logs-auditoria)            | Activación y revisión de logs de seguridad, autenticación, cambios y accesos sospechosos. |
| 17  | [Monitoreo con Wazuh como SIEM](./lab-17-wazuh-siem)                       | Implementación de Wazuh para monitoreo centralizado de eventos y alertas. |
| 18  | [Escaneo de vulnerabilidades interno](./lab-18-vulnerabilidades-nmap-nessus) | Identificación de servicios expuestos y fallas de configuración con Nmap y Nessus. |
| 19  | [Detección de intrusos con Suricata IDS](./lab-19-suricata-ids)            | Implementación de IDS para detectar tráfico malicioso y alertas en tiempo real. |
| 20  | [Hardening básico de sistemas Linux](./lab-20-linux-hardening)             | Aplicación de buenas prácticas de seguridad en servidores Linux: SSH, puertos, usuarios y permisos. |
| 21  | [Firewall de aplicaciones web con ModSecurity](./lab-21-modsecurity-waf)   | Protección de sitios web mediante reglas OWASP CRS y ModSecurity en Apache/Nginx. |
| 22  | [Backups seguros con cifrado en Linux](./lab-22backups-cifrados)          | Creación de políticas y scripts de respaldo automatizado y cifrado con GPG. |


### 🧪 Pentesting.

| Nº  | Nombre del laboratorio                                                  | Descripción breve                                                                 |
|-----|-------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| 23  | [Ataques a Metasploitable2 desde Kali](./lab-23-metasploitable2)       | Escaneo, explotación y post-explotación de vulnerabilidades conocidas en una VM vulnerable. |
| 24  | [Explotación de EternalBlue en Windows 7](./lab-24-eternalblue-win7)   | Detección y explotación de la vulnerabilidad MS17-010 utilizando Metasploit.      |
| 25  | [Escaneo y explotación de NaviServer vulnerable](./lab-25-naviservice-scan) | Análisis de servicios web inseguros usando Nmap, Gobuster y Metasploit.      |
| 26  | [Captura de flags en Kioptrix VM](./lab-26-kioptrix-vm-ctf)            | Escenario tipo CTF: escalada de privilegios, explotación de Apache y SUID abuse.  |
| 27  | [Exploración de CMS Monkey vulnerable](./lab-27-monkeycms-exploit)     | Reconocimiento, carga de shells y explotación de vulnerabilidades en CMS inseguros. |
| 28  | [Toma de control de Jenkins sin autenticación](./lab-28-jenkins-attack) | Descubrimiento y ejecución remota de comandos en entornos CI mal configurados.    |
| 29  | [Resolución de TheFinals en HackVM](./lab-29-hackvm-thefinals)         | Reconocimiento, explotación web, escalada de privilegios y captura de flags en entorno simulado. |
| 30  | [Sniffing y ataques MITM en red virtual](./lab-30-mitm-sniffing)       | Ataques tipo ARP spoofing para capturar tráfico en entornos LAN virtuales. |
| 31  | [Crackeo de contraseñas con Hashcat y John](./lab-31-password-cracking)| Ataques de fuerza bruta y diccionario sobre hashes extraídos de sistemas. |
| 32  | [Fuzzing y escaneo web con ffuf y Nikto](./lab-32-web-scanning)        | Enumeración avanzada de rutas y vulnerabilidades web. |
| 33  | [Automatización de exploits con Metasploit](./lab-33-msf-automatizado) | Uso de scripts `.rc` en Metasploit para automatizar ataques y pruebas. |

> ⚠ Algunos laboratorios requieren VirtualBox o Docker instalado previamente.


---

## 🧑‍💻 Autor.

**Carlos Benítez**  
Técnico en redes, estudiante autodidacta de ciberseguridad, apasionado por crear entornos de práctica que fortalezcan habilidades reales.  
🔗 [LinkedIn](https://www.linkedin.com/in/cbenitez191/) | 💻 [GitHub](https://github.com/cbenitez191/cbtech.sec) | 🐦 [X / Twitter](https://x.com/Cbtech_Sec)

---

## 📝 Licencia.

Contenido educativo libre. Si compartes o reutilizas, por favor da el crédito correspondiente.

---

