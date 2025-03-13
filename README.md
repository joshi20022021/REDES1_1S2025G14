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