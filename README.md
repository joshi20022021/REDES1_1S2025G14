# REDES1_1S2025G14
## Area de administración clientes
### Area
#### enable 
#### configure t
#### vtp mode client
#### vtp domain G14_technet
#### vtp password secure2025
#### spanning-tree mode pvst
#### spanning-tree mode rapid-pvst
### Recepción
#### enable 
#### configure t
#### vtp mode transparent
#### vtp domain G14_technet
#### vtp password secure2025

### Vlan

#### vlan 12
#### name Ventas
#### exit

#### vlan 22
#### name Soporte
#### exit

#### vlan 32
#### name Gerencia
#### exit

#### vlan 42
#### name Seguridad
#### exit


## Visualizar configuraciones

#### show vtp status
#### show vlan brief
### show interfaces trunk

enable
configure t
vtp mode client
vtp domain G14_technet
vtp password secure2025



##Detalle de los comandos Usados

###Area de Infraestructura

## **1️⃣ Configuración de `MSW8` y `MSW9` con EtherChannel**

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
