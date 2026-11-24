# 03-instalacion-proxmox

## Objetivo
Configurar maquina virtual en Virtualbox (adaptadores, red Host-Only, virtualizacion anidada, KVM), instalar proxmox y configuracion de interfaces dentro de proxmox.

## Procedimiento
 - Punto 1

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

- Punto 2

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

- Punto 3

Ahora es el momento de crear un usuario en proxmox con permisos limitados.

| Cuenta | Donde se utiliza | Rol y Permisos | Ambito | Para que las necesitas |
|---|---|---|---|---|
| root | Panel de Proxmox | Administración completa | Instalación de Proxmox | Preparación y recuperación del nodo |
| invitado | Panel de Proxmox | Solo permisos de lectura del | nodo | /nodes/pve-martinez | Usuario de prueba de permisos |

- Para crear el primer usuario primero vamos a:

Datacenter-Permissions-Users-Add

Nombre: ejemplo1-lectura
Importante ponerle la opcion PVE Proxmox para que solo funcione dentro de proxmox.
Asigar una contraseña

(Captura en evidencias 3-3.1 Usuario creado con etorno grafico.png)

Este usuario tiene los permisos estandar, para asignarle permisos solo de lectura que creara un rol con los permisos necesarios.

- Para crear este rol vamos a:

Datacenter-Permissions-Roles-Create

Nombre: aulalectura
El unico que permiso necesario para la lectura del nodo es Sys.Audit

(Captura en evidencias 3-3.2 Rol creado con entorno grafico.png)

Para asignar el rol al usuario vamos a:

Datacenter-Permissions-Add

Path: /nodes/pve-martinez
User: ejemplo1-lectura
Rol: Aulalectura
Importante quitar el propagate para que no adquiera mas permisos de lo debido

(Captura en evidencias 3-3.3 Rol asignado a ejemplo1-lectura.png.png)

Para crear los usuarios por terminal el comando principal es:

Crear usuario sin contraseña:

- pveum user add demo2-lectura@pve --comment "segundo usuario"

Asignar contraseñ a demo2-lectura:
- pveum passwd de2-lectura

Para crear y administrar los permisos y roles del usuario:

Crear rol:
- pveum rol add aulalectura2 --privs "Sys.Audit"

Asignar rol:
- pveum acl modift /nodes/pve-martinez -users demo2-lectura@pve --roles aulalectura2 --propagate0

Una vez creado y asigando los roles para comprobar que se han aplicado bien:

Comprobar rol y permisos de demo2-lectura:
- pveum user permissions demo2-lectura --path /nodes/pve-martinez

(Captura de pantalla con proceso en 3-3.4 Creacion de usuario y administracion de permisos terminal.png)

## Evidencias
Captura de proxmox funcionando y configuracion en evidencias-03-Intalacion-Proxmox.

## Conclusion
Maquian virtual configurada con proxmox instalado y a la espera de empezar paso 4.
[Volver al indice](../README.md)
