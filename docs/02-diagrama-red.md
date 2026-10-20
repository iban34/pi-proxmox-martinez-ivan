# 02-diagrama-red

## Objetivo
Diseñar el diagrama de red para la comunidacion de: las maquinas en proxmox, virtualbox y la maquina fisica.
Especificar: Elementos, Nonbre Indeficativo, IPs de cada elemento y pequeña una descripcion.
Puerto abierto para comunicacion de proxmox: 8006

## Recursos

| Elemento | Nombre | IP | Descripcion |
| --- | --- | --- | --- |
| Servidor ASO | srv-aso | 192.168.34.20/24 | VM en proxmox que hara de servidor |
| Cliente | cli-linux | 192.168.34.30/24 | VM en proxmox que hara de cliente |
| Nodo Proxmox | pve-martinez | --- | VM que aloja Proxmox la cual actua de gateway y con puerto 8006 abierto |
| VM/Adaptador 1 | vmbr0 | NAT | 10.0.2.15 | Adaptador que permite a proxmox y VM/LXC acceder a internet |
| VM/Adaptador 2 | vmbr1 | Host-Only | 192.168.34.1 | Adaptador que se encarga de permitirnos comunicarnos, desde fuera, con proxmox |

## Diagrama

Maquina Fisica/Clase -> VirtualBox -> VM-Proxmox-(pve-martinez) -> ServidorASO-(srv-aso)
                                                                -> Cliente-(cli-linux)

VM-Proxmox configurada con 2 adaptadores: 1 Red NAT para acceso a internet, 1 Host-Only para comunicacion interna.

Red Externa/Centro: 10.0.2.0
Red Interna Proxmox 192.168.34.0/24

flowchart TD
    A[Red Centro] --> B(VM-Proxmox  Pve-Martinez)
    B --> C{vmbr-0}
    C --> D{Cliente cli-linux}
    D --> E
    C --> E{ServidorASO srv-aso}

## Conclusion



[Volver al indice](../README.md)
