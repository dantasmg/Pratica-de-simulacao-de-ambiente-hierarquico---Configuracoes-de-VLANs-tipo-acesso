# Prática de simulação de ambiente hierárquico - Configurações de VLANs tipo acesso 

## VLANs

| VLAN ID | Nome | Uso | Portas | Rede IP sugerida |
|---|---|---|---|---|
| 10 | Alunos | Computadores | Ímpares | 192.168.10.0/24 |
| 20 | Visitantes | Notebooks | Pares | 192.168.20.0/24 |

## Mapeamento das interfaces (camada de acesso)

| Switch | Interface | Modo | VLAN | Dispositivo | IP sugerido |
|---|---|---|---|---|---|
| ACESSO 1 | Fa0/1 | access | 10 (Alunos) | PC0 | 192.168.10.11/24 |
| ACESSO 1 | Fa0/2 | access | 20 (Visitantes) | Laptop0 | 192.168.20.11/24 |
| ACESSO 2 | Fa0/1 | access | 10 (Alunos) | PC1 | 192.168.10.12/24 |
| ACESSO 2 | Fa0/2 | access | 20 (Visitantes) | Laptop1 | 192.168.20.12/24 |
| ACESSO 3 | Fa0/1 | access | 10 (Alunos) | PC2 | 192.168.10.13/24 |
| ACESSO 3 | Fa0/2 | access | 20 (Visitantes) | Laptop2 | 192.168.20.13/24 |
| ACESSO 4 | Fa0/1 | access | 10 (Alunos) | PC3 | 192.168.10.14/24 |
| ACESSO 4 | Fa0/2 | access | 20 (Visitantes) | Laptop3 | 192.168.20.14/24 |

## Comandos Cisco IOS

### ACESSO 1

```
enable
configure terminal
hostname ACESSO1
vlan 10
name Alunos
exit
vlan 20
name Visitantes
exit
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
exit
interface FastEthernet0/2
switchport mode access
switchport access vlan 20
exit
end
copy running-config startup-config
```

### ACESSO 2

```
enable
configure terminal
hostname ACESSO2
vlan 10
name Alunos
exit
vlan 20
name Visitantes
exit
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
exit
interface FastEthernet0/2
switchport mode access
switchport access vlan 20
exit
end
copy running-config startup-config
```

### ACESSO 3

```
enable
configure terminal
hostname ACESSO3
vlan 10
name Alunos
exit
vlan 20
name Visitantes
exit
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
exit
interface FastEthernet0/2
switchport mode access
switchport access vlan 20
exit
end
copy running-config startup-config
```

### ACESSO 4

```
enable
configure terminal
hostname ACESSO4
vlan 10
name Alunos
exit
vlan 20
name Visitantes
exit
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
exit
interface FastEthernet0/2
switchport mode access
switchport access vlan 20
exit
end
copy running-config startup-config
```

## Validação

```
show vlan brief
show interfaces FastEthernet0/1 switchport
```
