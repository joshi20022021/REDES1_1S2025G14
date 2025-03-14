

##Detalle de los comandos Usados

# Configuración del Área de Administración 📌

## Configuración de VTP en Modo Cliente
### **Modo Cliente:** `SW0, SW1, SW2, SW3, SW4, MSW5, MSW6, MSW7`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025
exit
```
verificar configuracion
```bash
show vtp status
```
Modo transparente SW5
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode transparent
vtp password secure2025
exit
```
configurar vlans
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
vlan recepcion
```bash
enable
configure terminal
vlan 52
name Recepcion
exit
```
Configurar interfaces como Trunk en los switches de la administración
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
Configurar MSW5 como el switch root para STP
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42,52 root primary
exit
```
Configurar MSW6 como root secundario
```bash
enable
configure terminal
spanning-tree vlan 12,22,32,42,52 root secondary
exit
```
Verificar STP
```bash
show spanning-tree vlan 12
show spanning-tree vlan 22
show spanning-tree vlan 32
show spanning-tree vlan 42
show spanning-tree vlan 52
```

###Area de Infraestructura

## Configuración del Área de estructura**

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
SW6
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
SW8
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

## 🛠 Paso 1: Configurar VTP en los Switches
### **Modo Cliente:** `SW8, SW9, SW10, MSW11`
```bash
enable
configure terminal
vtp domain G14_technet
vtp mode client
vtp password secure2025
exit
```
configurar VLANS
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
Configurar Trunking
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
Configurar EtherChannel (LACP)
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
Configurar STP (PVST)
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42 root primary
exit
```
Verificar STP
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
Configurar VLANs
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
Configurar Trunking en los switches
SW11
```bash
enable
configure terminal
interface range FastEthernet0/1, FastEthernet0/2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
```
SW12
```bash
enable
configure terminal
interface range FastEthernet0/1, FastEthernet0/2
switchport mode trunk
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 12,22,32,42
exit
```
SW13
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
Configurar EtherChannel
Configuración en SW11 y SW12 LACP
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
Configurar STP (PVST/RSTP)
```bash
enable
configure terminal
spanning-tree mode pvst
spanning-tree vlan 12,22,32,42 root primary
exit
```
Verificar STP
```bash
show spanning-tree vlan 12
show spanning-tree vlan 22
show spanning-tree vlan 32
show spanning-tree vlan 42
```

