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
