# 📌 Universidad de San Carlos de Guatemala  
### 🏛 Facultad de Ingeniería - Escuela de Ciencias y Sistemas  
### 🖥 Laboratorio Redes De Computadoras 1, Sección: N  

## 👤 Nombre: **Andrés Alejandro Agosto Méndez**  
## 🎓 Carnet: **202113580**  
## 👤 Nombre: **Edgar Josías Cán Ajquejay**  
## 🎓 Carnet: **202112012** 

## 🏥 **Proyecto 2**  

# Configuración de la red CUNDECH

## Tabla de VLANs y Subredes de CUNDECH

| Área         | VLAN | Subred            | Gateway IP      |
|--------------|------|-------------------|-----------------|
| Biblioteca   | 42   | 192.168.14.0/25   | 192.168.14.1    |
| Estudiantes  | 12   | 192.168.14.128/26 | 192.168.14.129  |
| Docentes     | 22   | 192.168.14.192/27 | 192.168.14.193  |
| Seguridad    | 32   | 192.168.14.224/29 | 192.168.14.225  |

---

## 🖥️ CONFIGURACION SWITCH SW7
```bash
enable
configure terminal

! Configuración VTP
vtp domain Grupo14
vtp password usac2025
vtp mode server

! Crear VLANs
vlan 12
 name Estudiantes
vlan 22
 name Docentes
vlan 32
 name Seguridad
vlan 42
 name Biblioteca

! Puertos de acceso
interface fa0/5
 switchport mode access
 switchport access vlan 12
 no shutdown

interface fa0/4
 switchport mode access
 switchport access vlan 12
 no shutdown

! Troncales
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown
```

## 🖥️ SWITCH SW8

```bash
enable
configure terminal

! Configuración VTP
vtp domain Grupo14
vtp password usac2025
vtp mode client

! Puertos de acceso
interface fa0/4
 switchport mode access
 switchport access vlan 22
 no shutdown

interface fa0/3
 switchport mode access
 switchport access vlan 22
 no shutdown

! Troncales
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown
```

## 🖥️ SWITCH SW6

```bash
enable
configure terminal

! Configuración VTP
vtp domain Grupo14
vtp password usac2025
vtp mode client

! Puertos de acceso
interface fa0/5
 switchport mode access
 switchport access vlan 32
 no shutdown

interface fa0/4
 switchport mode access
 switchport access vlan 42
 no shutdown

interface fa0/3
 switchport mode access
 switchport access vlan 42
 no shutdown

! Troncales
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown
```

## 🖥️ SWITCH MULTICAPA MS8

```bash
enable
configure terminal

! Habilitar ruteo
ip routing

! Configurar VLANs virtuales (puertas de enlace)
interface vlan 12
 ip address 192.168.14.129 255.255.255.192
 no shutdown

interface vlan 22
 ip address 192.168.14.193 255.255.255.224
 no shutdown

interface vlan 32
 ip address 192.168.14.225 255.255.255.248
 no shutdown

interface vlan 42
 ip address 192.168.14.1 255.255.255.128
 no shutdown

! Troncales hacia otros switches
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

interface fa0/4
 switchport mode trunk
 switchport trunk allowed vlan 12,22,32,42
 no shutdown

! VTP como cliente
vtp domain Grupo14
vtp password usac2025
vtp mode client
```

## 🖥️ PCs y direcciones IP 

| PC           | IP Address       | Gateway        | Máscara          |
|--------------|------------------|----------------|------------------|
| Seguridad2   | 192.168.14.226   | 192.168.14.225 | 255.255.255.248  |
| Biblioteca3  | 192.168.14.2     | 192.168.14.1   | 255.255.255.128  |
| Biblioteca4  | 192.168.14.3     | 192.168.14.1   | 255.255.255.128  |
| Estudiantes6 | 192.168.14.130   | 192.168.14.129 | 255.255.255.192  |
| Estudiantes7 | 192.168.14.131   | 192.168.14.129 | 255.255.255.192  |
| Docentes6    | 192.168.14.194   | 192.168.14.193 | 255.255.255.224  |
| Docentes7    | 192.168.14.195   | 192.168.14.193 | 255.255.255.224  |
