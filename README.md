# Prática de Simulação de Ambiente Hierárquico — Configurações de VLANs Tipo Acesso (Atividade 06)

**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia de Rondônia (IFRO) — *Campus* Porto Velho Zona Norte  
**Curso:** Superior de Tecnologia em Redes de Computadores  
**Disciplina:** Comutação de Redes Locais (TCN.0639)  
**Docente:** Prof. Jhordano Malacarne Bravim  
**Autor(a):** Mariane Gonçalves Dantas 
**Ferramenta:** Cisco Packet Tracer

## 1. Objetivo da Atividade
Configurar duas VLANs nos 4 switches da **Camada de Acesso** (`Switch4`, `Switch5`, `Switch6` e `Switch7`) do ambiente hierárquico simulado, segmentando os domínios de *broadcast* conforme o seguinte padrão:
* **VLAN 10 (`Alunos`):** Atribuída a todas as **portas ímpares** de acesso conectadas aos computadores (`PC0` a `PC3`) e ao servidor (`Server0`).
* **VLAN 20 (`Visitantes`):** Atribuída a todas as **portas pares** de acesso conectadas aos notebooks (`Laptop0` a `Laptop3`).

## 2. Diagrama da Topologia

<img width="847" height="626" alt="Print Packet Tracer" src="https://github.com/user-attachments/assets/5176690c-52df-4046-a569-c5b4be5b5811" />

## 3. Fundamentação e Documentação Técnica

Uma **VLAN (*Virtual Local Area Network*)** segmenta logicamente um switch físico em múltiplos domínios de *broadcast* isolados em Camada 2. Dispositivos em VLANs diferentes não trocam quadros diretamente entre si, elevando a segurança e o desempenho da rede local.

### 3.1 Tabela de VLANs Registradas
| VLAN ID | Nome da VLAN | Dispositivos Atendidos | Critério de Portas | Sub-rede IPv4 | Máscara |
| :---: | :---: | :--- | :--- | :---: | :---: |
| **10** | `Alunos` | Computadores (`PC0` a `PC3`) e `Server0` | Portas **Ímpares** (`Fa0/1, Fa0/3...`) | `192.168.10.0/24` | `255.255.255.0` |
| **20** | `Visitantes` | Notebooks (`Laptop0` a `Laptop3`) | Portas **Pares** (`Fa0/2, Fa0/4...`) | `192.168.20.0/24` | `255.255.255.0` |

### 3.2 Mapeamento das Interfaces da Camada de Acesso
| Switch no Diagrama | Hostname | Interface Física | Modo | VLAN Atribuída | Dispositivo Conectado | Endereço IPv4 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| `Switch4` (ACESSO 1) | `ACESSO1` | `FastEthernet0/1` | `access` | `10 (Alunos)` | `PC0` | `192.168.10.11/24` |
| `Switch4` (ACESSO 1) | `ACESSO1` | `FastEthernet0/2` | `access` | `20 (Visitantes)` | `Laptop0` | `192.168.20.11/24` |
| `Switch4` (ACESSO 1) | `ACESSO1` | `FastEthernet0/3` | `access` | `10 (Alunos)` | `Server0` | `192.168.10.10/24` |
| `Switch5` (ACESSO 2) | `ACESSO2` | `FastEthernet0/1` | `access` | `10 (Alunos)` | `PC1` | `192.168.10.12/24` |
| `Switch5` (ACESSO 2) | `ACESSO2` | `FastEthernet0/2` | `access` | `20 (Visitantes)` | `Laptop1` | `192.168.20.12/24` |
| `Switch6` (ACESSO 3) | `ACESSO3` | `FastEthernet0/1` | `access` | `10 (Alunos)` | `PC2` | `192.168.10.13/24` |
| `Switch6` (ACESSO 3) | `ACESSO3` | `FastEthernet0/2` | `access` | `20 (Visitantes)` | `Laptop2` | `192.168.20.13/24` |
| `Switch7` (ACESSO 4) | `ACESSO4` | `FastEthernet0/1` | `access` | `10 (Alunos)` | `PC3` | `192.168.10.14/24` |
| `Switch7` (ACESSO 4) | `ACESSO4` | `FastEthernet0/2` | `access` | `20 (Visitantes)` | `Laptop3` | `192.168.20.14/24` |

## 4. Comandos Sequenciais do Cisco IOS

```text
! Aplicar nos 4 switches de Acesso (trocando o hostname para ACESSO1, ACESSO2, ACESSO3 e ACESSO4)
enable
configure terminal
hostname ACESSO1

! 1. Criação e nomeação das VLANs
vlan 10
 name Alunos
exit
vlan 20
 name Visitantes
exit

! 2. Portas ímpares na VLAN 10 (Alunos)
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
exit
interface FastEthernet0/3
 switchport mode access
 switchport access vlan 10
exit

! 3. Portas pares na VLAN 20 (Visitantes)
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 20
exit

! 4. Gravação na NVRAM
end
copy running-config startup-config
```

## 5. Comandos de Validação
```text
show vlan brief
show interfaces FastEthernet0/1 switchport
```
