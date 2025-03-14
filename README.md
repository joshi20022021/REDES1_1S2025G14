# 📌 Universidad de San Carlos de Guatemala  
### 🏛 Facultad de Ingeniería - Escuela de Ciencias y Sistemas  
### 🖥 Laboratorio Redes De Computadoras 1, Sección: N  

## 👤 Andrés Alejandro Agosto Méndez**  
## 🎓 Carnet: **202113580**  
## 👤 Nombre: **Edgar Josías Cán Ajquejay**  
## 🎓 Carnet: **202112012** 

## 🏥 **Proyecto 1**  
---
# 📌 Tabla de Direccionamiento IP

| **Dirección IP**      | **Dispositivo**              |
|----------------------|----------------------------|
| 192.168.52.4        | PC-PT Recepcion4           |
| 192.168.52.3        | PC-PT Recepcion3           |
| 192.168.52.2        | PC-PT Recepcion2           |
| 192.168.52.1        | PC-PT Recepcion1           |
| 192.168.12.5        | PC-PT Ventas5              |
| 192.168.12.2        | PC-PT Ventas2              |
| 192.168.12.1        | PC-PT Ventas1              |
| 192.168.22.3        | PC-PT Soporte Tecnico 3    |
| 192.168.22.2        | PC-PT Soporte Tecnico 2    |
| 192.168.22.5        | Laptop-PT Soporte Tecnico 5 |
| 192.168.32.3        | PC-PT Gerencia3            |
| 192.168.32.4        | PC-PT Gerencia4            |
| 192.168.32.2        | PC-PT Gerencia2            |
| 192.168.32.1        | PC-PT Gerencia1            |
| 192.168.42.7        | PC-PT Seguridad7           |
| 192.168.42.5        | PC-PT Seguridad5           |
| 192.168.42.3        | Laptop-PT Seguridad3       |
| 192.168.42.6        | Laptop-PT Seguridad6       |
| 192.168.42.8        | Laptop-PT Seguridad8       |
| 192.168.22.4        | PC-PT Soporte Tecnico 4    |

# 📸 Capturas de la implementacion de las topologias
## 🌐 Protocolos VTP
### AREA CENTRAL
![](CAPTURAS/VTPSERVIDOR.png)

### AREA DE ADMINISTRACION
![](CAPTURAS/VTPTRANSPARENTE.png)

### AREA DE DESARROLLO 
![](CAPTURAS/VTPCLIENTE01.png)

### AREA DE GERENCIA
![](CAPTURAS/VTPCLIENTE02.png)

### AREA DE INFRAESTRUCTURA
![](CAPTURAS/VTPCLIENTE02.png)

##Detalle de los comandos Usados

## 🏢 **Área Central (Backbone)**
#### **Modo Servidor:** `Switch Servidor`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode server
vtp password secure2025
exit
show vtp status
```
#### **Modo Servidor:** `Switch Servidor`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode server
vtp password secure2025
exit
show vtp status
```
#### **Modo Cliente: MSW1, MSW2, MSW3, MSW4, MSW9, MSW10**
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode server
vtp password secure2025
exit
show vtp status
```
#### **Configurar VLANs en el Servidor**
```bash
enable
configure terminal
vlan 10
name Backbone1
vlan 20
name Backbone2
vlan 30
name Backbone3
vlan 40
name Backbone4
exit
show vlan brief
```
### **Configurar Trunking en los switches**
#### **Switch Servidor**
```bash
enable
configure terminal
interface range FastEthernet0/1 - 6
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20,30,40
exit
```

#### **MSW1, MSW2, MSW3, MSW4, MSW9, MSW10**
```bash
enable
configure terminal
interface range FastEthernet0/1 - 6
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20,30,40
exit
show interfaces trunk
```

#### **Configuración en MSW1 y MSW2 (LACP)**
```bash
enable
configure terminal
interface range FastEthernet0/3 - 5
channel-group 14 mode active
exit
interface port-channel 14
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 10,20,30,40
exit
show etherchannel summary
```

#### **Configurar STP Root Bridge en el Servidor**
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root primary
spanning-tree vlan 30 root primary
spanning-tree vlan 40 root primary
exit
```

#### **Verificar STP**
```bash
show spanning-tree vlan 10
show spanning-tree vlan 20
show spanning-tree vlan 30
show spanning-tree vlan 40
```

# Configuración del Área de Administración 📌

## Configuración de VTP en Modo Cliente
#### **Modo Cliente:** `SW0, SW1, SW2, SW3, SW4, MSW5, MSW6, MSW7`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025
exit
show vtp status
```

#### **Modo transparente SW5**
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode transparent
vtp password secure2025
exit
```

#### **configurar vlans**
```bash
enable
configure terminal
vlan 12
name Ventas
vlan 22
name Soporte
vlan 32
name Gerencia
vlan 42
name Seguridad
exit
show vlan brief
```

#### **vlan recepcion**
```bash
enable
configure terminal
vlan 52
name Recepcion
exit
```

#### **Configurar interfaces como Trunk en los switches de la administración**
```bash
enable
configure terminal
interface range FastEthernet0/1 - 2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42,52
exit
show interfaces trunk
```

#### **Configurar MSW5 como el switch root para STP**
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42,52 root primary
exit
```

#### **Configurar MSW6 como root secundario**
```bash
enable
configure terminal
spanning-tree vlan 12,22,32,42,52 root secondary
exit
```

#### **Verificar STP**
```bash
show spanning-tree vlan 12
show spanning-tree vlan 22
show spanning-tree vlan 32
show spanning-tree vlan 42
show spanning-tree vlan 52
```

###Area de Infraestructura

#### **Configuración del Área de estructura**

### **MSW8**
```bash
configure terminal
interface range FastEthernet0/3 - 5
channel-group 14 mode active
exit
interface port-channel 14
switchport mode trunk
switchport trunk allowed vlan 12,22,32,42
exit

configure terminal
interface range FastEthernet0/3 - 5
channel-group 14 mode active
exit
interface port-channel 14
switchport mode trunk
switchport trunk allowed vlan 12,22,32,42
exit

configure terminal
spanning-tree mode pvst
spanning-tree vlan 12 root primary
spanning-tree vlan 22 root primary
spanning-tree vlan 32 root primary
spanning-tree vlan 42 root primary
exit
```

#### **SW6**
```
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025

interface range FastEthernet0/1 - 2
switchport mode trunk
switchport trunk allowed vlan 12,22,32,42
exit

interface FastEthernet0/3
switchport mode access
switchport access vlan 12
exit

interface FastEthernet0/4
switchport mode access
switchport access vlan 22
exit
```

#### **SW8**
```
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025

interface FastEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 12,22,32,42
exit

interface FastEthernet0/2
switchport mode access
switchport access vlan 12
exit

interface FastEthernet0/3
switchport mode access
switchport access vlan 22
exit
```
# 🔧 Configuración de la Red - Área de Desarrollo 💻

### **Modo Cliente:** `SW8, SW9, SW10, MSW11`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025
exit
```

#### **configurar VLANS**
```bash
enable
configure terminal
vlan 12
name Ventas
vlan 22
name Soporte
vlan 32
name Gerencia
vlan 42
name Seguridad
exit
show vlan brief
```

#### **Configurar Trunking**
```bash
enable
configure terminal
interface range FastEthernet0/3 - 5
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
show interfaces trunk
```

#### **Configurar EtherChannel (LACP)**
```bash
enable
configure terminal
interface range FastEthernet0/3 - 5
channel-group 14 mode active
exit
interface port-channel 14
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
show etherchannel summary
```

#### **Configurar STP (PVST)**
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42 root primary
exit
```

#### **Verificar STP**
```bash
show spanning-tree vlan 12
show spanning-tree vlan 22
show spanning-tree vlan 32
show spanning-tree vlan 42
```

## 🏢 **Área de Gerencia**
### 🛠 Paso 1: Configurar VTP en los Switches
#### **Modo Cliente:** `SW11, SW12, SW13`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025
exit
show vtp status
```

#### **Configurar VLANs**
```bash
enable
configure terminal
vlan 12
name Ventas
vlan 22
name Soporte
vlan 32
name Gerencia
vlan 42
name Seguridad
exit
show vlan brief
```

### **Configurar Trunking en los switches**
#### **SW11**
```bash
enable
configure terminal
interface range FastEthernet0/1, FastEthernet0/2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
```

#### **SW12**
```bash
enable
configure terminal
interface range FastEthernet0/1, FastEthernet0/2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
```

#### **SW13**
```bash
enable
configure terminal
interface range FastEthernet0/1, FastEthernet0/2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
show interfaces trunk
```

### Configurar EtherChannel
#### **Configuración en SW11 y SW12 (LACP)**
```bash
enable
configure terminal
interface range FastEthernet0/3 - 5
channel-group 14 mode active
exit
interface port-channel 14
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
show etherchannel summary
```

#### **Configurar STP (PVST/RSTP)**
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42 root primary
exit
```
#### **Verificar STP**
```bash
show spanning-tree vlan 12
show spanning-tree vlan 22
show spanning-tree vlan 32
show spanning-tree vlan 42
```

# 📸 Capturas del ping entre hosts
### AREA CENTRAL
![](CAPTURAS/VTPSERVIDOR.png)

### AREA DE ADMINISTRACION
![](CAPTURAS/VTPTRANSPARENTE.png)

### AREA DE DESARROLLO 
![](CAPTURAS/VTPCLIENTE01.png)

### AREA DE GERENCIA
![](CAPTURAS/VTPCLIENTE02.png)

### AREA DE INFRAESTRUCTURA
![](CAPTURAS/VTPCLIENTE02.png)


