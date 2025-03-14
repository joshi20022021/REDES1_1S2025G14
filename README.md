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
```






##Detalle de los comandos Usados

###Area de Infraestructura

## Configuracion area de estructura**

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
