# VLAN

- **Vlan 10**: ingenieros
- **Vlan 20**: CAD
- **Vlan 30**: recepcionista
- **Vlan 40**: socios
- **Vlan 50**: asistentes

# Dispositivos 
- Conexión a Cloud
- Servidor Local
- 800 PC 
- 19 SW capa 3
- 15 SW capa 2

# Comandos Utilizados 

## Servidor VTP

```
enable 
write erase

conf t
no ip domain-lookup 
vtp version 2
vtp mode server
vtp domain EternalSpring

interface range fa0/1-3
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit

vlan 10
 name Ingenieros
exit

vlan 20
 name CAD
exit

vlan 30
 name Recepcionistas
exit

vlan 40
 name Socios
exit

vlan 50
 name Asistentes
exit

interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
exit

interface vlan 30
 ip address 192.168.30.1 255.255.255.0
 no shutdown
exit

interface vlan 40
 ip address 192.168.40.1 255.255.255.0
 no shutdown
exit

interface vlan 50
 ip address 192.168.50.1 255.255.255.0
 no shutdown
exit

ip routing

router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0
 network 192.168.50.0 0.0.0.255 area 0
 network 11.0.0.0 0.0.0.3 area 0
exit

```
## Clientes VTP
```
enable 
write erase

conf t
no ip domain-lookup 
vtp mode client
vtp domain EternalSpring

interface range fa0/1-6
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit


ip routing

router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0
 network 192.168.50.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.7 area 0
 network 11.0.0.0 0.0.0.3 area 0
exit
```

## Switches capa 2

```
enable
write erase
configure terminal
vtp mode client
vtp domain EternalSpring


interface fa0/1
switchport mode trunk

interface Fa0/2
switchport mode access
switchport access vlan 50
exit
exit

```

<img width="1333" alt="image" src="https://github.com/user-attachments/assets/3845c790-82d0-44c1-8494-fdccfedf2bc0">
