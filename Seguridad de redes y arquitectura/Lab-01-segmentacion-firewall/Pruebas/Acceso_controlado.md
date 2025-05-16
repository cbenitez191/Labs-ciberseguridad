
# 🔐 Prueba de Acceso Controlado hacia el Servidor AD

### 🎯 Objetivo

Verificar que las VLANs autorizadas pueden acceder únicamente a los servicios específicos habilitados en el servidor de Active Directory (AD).

---

### 🧪 Entorno

- Servidor AD: 10.10.20.3 – VLAN20
- Clientes: VLAN10 (Administración), VLAN30 (Usuarios), VLAN40 (Invitados)
- Servicios permitidos en el firewall: DNS, LDAP, Kerberos, SMB, RPC, HTTP/HTTPS
- Firewall: WatchGuard con reglas específicas por servicio

---

### 🔧 Procedimiento

**Paso 1:** Comprobar resolución DNS desde un cliente en VLAN10.

```bash
nslookup ad.cbtech.local 10.10.20.3
```

→ Debe mostrar la IP del servidor AD, confirmando que el servicio DNS está permitido.

---

**Paso 2:** Realizar una consulta LDAP desde un cliente autorizado.

```bash
ldapsearch -x -H ldap://10.10.20.3 -b "dc=cbtech,dc=local"
```

→ El comando debe devolver información del directorio si el puerto 389 está habilitado.

---

**Paso 3:** Verificar acceso a puertos Kerberos, SMB y RPC.

```bash
nmap -Pn -p 88,135,445 10.10.20.3
```

→ Estos puertos deben aparecer como abiertos (`open`) desde las VLANs autorizadas.

---

**Paso 4:** Escanear todos los servicios permitidos en un solo comando.

```bash
nmap -Pn -p 53,389,445,88,135,80,443 10.10.20.3
```

→ Deben estar `open` únicamente los puertos que están definidos como permitidos.

---

**Paso 5:** Validar tráfico en el Traffic Monitor del firewall.

→ Solo deben aparecer registros de tráfico autorizado (DNS, LDAP, etc.) y no debe haber otros intentos de acceso.

