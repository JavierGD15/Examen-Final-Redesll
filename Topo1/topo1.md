# VLAN

- **Vlan 10**: ingenieros
- **Vlan 20**: CAD
- **Vlan 30**: recepcionista
- **Vlan 40**: socios
- **Vlan 50**: asistentes

# Dispositivos 
- Conexión a Cloud
- 16 PC 
- 1 SW capa 3
- 1 SW capa 2

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

interface range gi1/0/1
 switchport mode trunk
 switchport trunk allowed vlan all
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
exit
```

## Switch capa 2

```
enable
write erase

configure terminal
vtp mode client
vtp domain EternalSpring


interface fa0/1
switchport mode trunk

interface Fa0/10
switchport mode access
switchport access vlan 10
exit

interface Fa0/11
switchport mode access
switchport access vlan 20
exit

interface Fa0/12
switchport mode access
switchport access vlan 30
exit

interface Fa0/13
switchport mode access
switchport access vlan 40
exit

interface Fa0/14
switchport mode access
switchport access vlan 50
exit
```
<img width="556" alt="image" src="https://github.com/user-attachments/assets/87f38eb2-8c76-4917-98d5-da33b2826402">

