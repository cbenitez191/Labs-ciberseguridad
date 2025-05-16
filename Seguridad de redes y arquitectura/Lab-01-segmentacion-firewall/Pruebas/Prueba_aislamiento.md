
# 🧪 Pruebas de Segmentación y Reglas de Firewall

Este documento contiene las pruebas realizadas para validar el correcto funcionamiento de la segmentación de red mediante VLANs y las reglas configuradas en el firewall.

---

## 🔒 Prueba 1: Aislamiento entre VLANs

### 🎯 Objetivo

Comprobar que no exista comunicación entre VLANs distintas sin autorización explícita en el firewall.

### 🧪 Entorno

- VLAN10 (Administración) – 192.168.10.10
- VLAN30 (Usuarios) – 192.168.30.10
- VLAN40 (Invitados) – 192.168.40.10
- Firewall: WatchGuard

---

### 🔧 Procedimiento

**Paso 1:** Ejecutar ping desde VLAN10 hacia VLAN30 y VLAN40.

```bash
ping 192.168.30.10
ping 192.168.40.10
```

→ Debe mostrar `Request timed out` o `100% packet loss`, indicando que el ICMP fue bloqueado.

---

**Paso 2:** Escanear puertos desde VLAN10 hacia hosts en VLAN30 y VLAN40.

```bash
nmap -Pn -p 22,80,443 192.168.30.10
nmap -Pn -p 22,80,443 192.168.40.10
```

→ Los resultados deben mostrar todos los puertos como `filtered` o `closed`.

---

**Paso 3:** Verificar los registros de tráfico bloqueado en el firewall (Traffic Monitor o Log Server).

→ Se deben observar intentos bloqueados entre VLANs por las políticas `deny`.

---

## 🔐 Prueba 2: Acceso controlado hacia el Servidor AD

### 🎯 Objetivo

Verificar que las VLANs autorizadas pueden acceder únicamente a los servicios específicos habilitados en el servidor de Active Directory (AD).

### 🧪 Entorno

- Servidor AD: 10.10.20.3 – VLAN20
- Clientes desde VLAN10, VLAN30, VLAN40
- Servicios habilitados: DNS, LDAP, Kerberos, SMB, RPC, HTTP/HTTPS

---

### 🔧 Procedimiento

**Paso 1:** Verificar resolución DNS desde un cliente autorizado.

```bash
nslookup ad.cbtech.local 10.10.20.3
```

→ Debe devolver correctamente la IP del servidor AD.

---

**Paso 2:** Realizar consulta LDAP contra el servidor AD.

```bash
ldapsearch -x -H ldap://10.10.20.3 -b "dc=cbtech,dc=local"
```

→ Debe devolver entradas del directorio, confirmando conectividad.

---

**Paso 3:** Escanear puertos permitidos desde un cliente hacia el servidor AD.

```bash
nmap -Pn -p 53,389,445,88,135 10.10.20.3
```

→ Los puertos configurados como permitidos deben aparecer como `open`.

---

**Paso 4:** Verificar en los registros del firewall el tráfico autorizado y bloqueado.

→ Solo los servicios definidos en las reglas deben aparecer como permitidos.
