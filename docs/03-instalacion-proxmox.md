# 03-instalacion-proxmox

## Objetivo
Configurar maquina virtual en Virtualbox (adaptadores, red Host-Only, virtualizacion anidada, KVM), instalar proxmox y configuracion de interfaces dentro de proxmox.

## Procedimiento
 - Punto 3

Descargar ISO de proxmox, crear VM sin el instalador y configurar VM de la siguiente manera:
    - 6 GB de RAM
    - 80 GB de disco dinamico
    - 2 nucleos de CPU
    - Nested VT-X/AMD-X
    - Paravirtualizacion KVM
    - Adaptador 1 NAT
    - Adaptador 2 Host-Only

Una vez configurada la maquina se inserta la ISO de proxmox,en la instalcion sera asignara el hostname como pve-martinez.lab.test y la interfaz de gestion nic0/vmbr0 (10.0.2.15).

Una vez instalado se configura para que responda a la red Host-Only y configurar los adaptadores de red.
- En /etc/hosts cambiar segunda linea y poner:
192.168.56.10 pve-martinez.lab.test pve-martinez (solo habra que cambiar la ip inicial).

-  En /etc/networks/interfaces debera quedar tal que asi:
auto lo
iface lo inet loopback

iface enp0s3 inet manual
iface enp0s8 inet manual

auto nic0
iface nic0 inet static
    address 10.0.2.15/24
    gateway 10.0.2.2
    bridge-ports enp0s3
    bridge-stp off
    bridge-fd 0

auto nic1
iface nic1 inet static
    address 192.168.56.10/24
    bridge-ports enp0s8
    bridge-stp off
    bridge-fd 0
    post-up sysctl -w net.ipv4.ip_forward=1
    post-up iptables -t nat -A POSTROUTING -s 192.168.56.0/24 -o vmbr0 -j MASQUERADE
    post-down iptables -t nat -D POSTROUTING -s 192.168.56.0/24 -o vmbr0 -j MASQUERADE
source /etc/network/interfaces.d/*

Una vez hecho esto se puede hacerder a proxmox deste la maquina externa con la ip 192.168.56.10.

- Punto 4

Al ver los almacenamientos disponibles en promox se pueden distinguir 2:
    - Local, carpeta dentro de la maquina donde se puede guardar todo tipo de archivos.
    - Local-LVM, es un almacenamiento especifico para las maquinas virutales y contenedores lxc de proxmox.

- Reparto de recursos
| Elemento | CPU/vCPU | RAM | Disco | Justificacion |
|---|---|---|---|---|
| Proxmox | 2 Nucleos | 2 GB | 10 GB | Es lo que mas recursos debe tener ya que es lo que gestiona todo lo demas |
| srv-aso | 1 Nucleo | 2 GB +- | 10 GB | Es lo minimo necesario para que funcione y poco mas, no hay necesidad para mas |
| cli-linux | 1 Nucleo | 2 GB +- | 10 GB | Es lo minimo necesario para que funcione y poco mas, no hay necesidad para mas |
| Plantilla, ISOs y copias | No aplica | No aplica | 30 GB| Deberia guardar una copia de todo lo demas asique como minimo debe tener el almacenamiento de los 3 juntos |
| Margen de operacion | 0 | 0 +- | 20 GB | |

Por el momento solo existe el usuario root el cual tiene acceso a todo.

## Evidencias
Captura de proxmox funcionando y configuracion en evidencias-03-Intalacion-Proxmox.

## Conclusion
Maquian virtual configurada con proxmox instalado y a la espera de empezar paso 4.
[Volver al indice](../README.md)
