# Inventario investigado y viabilidad

## Contexto de la observacion

- Fecha y sistema utilizado: 6/10 Linux
- Modalidad, equipo anfitrion y VM VirtualBox si procede: PENDIENTE.
- Version de Proxmox prevista: PENDIENTE.

## Inventario inicial

| Area | Dato observado y evidencia | Especificacion y fuente | Limite o diferencia | Justificacion |
|---|---|---|---|---|
| CPU | CPU: Intel Pentium G4560 3.50 GHz| 2 núcleos / 4 hilos, 64 bits, con VT-x.| Al momento de crear las VM los 2 núcleos se quedaran cortos. | Datos obtenidos de: BIOS, pagina oficial de proxmox|
| RAM | CRUCIAL CRUCIAL DDR4 4096MB 2400MHz x2 | 2 GB como mínimo para el servicio proxmox mas lo asignado a las VM | Para este proyecto los 8 GB de ram serviran bien| Datos obtenidos de: BIOS, pagina oficial de proxmox |
| Almacenamiento | THOSHIBA DT01ACA050 500 GB | Los requisitos recomendados es SSD, no lo cumple | No es el recomendado pero sirve perfectamente para la tarea | Datos obtenidos de: BIOS, pagina oficial de proxmox |
| Red | RTL8111 eth0 1Gbit/s | No dispone de redundancia ni targetas de red adicionales | Para crear un solo nodo cumple su función, además de abarcar 1 GB requerido | Datos obtenidos de: comando lshw, pagina oficial de proxmox|
| Plataforma | x64, UEFI BIOS.| Cumple perfectamente, arquitectura x64 y BIOS en modo UEFI| | Datos obtenidos de: BIOS, pagina oficial de proxmox |

## 1. Puedo instalar Proxmox en este equipo?

Contrastar el inventario con requisitos oficiales de la version prevista.
Responder por separado y justificar con datos y fuentes:

- Puedo instalar y arrancar Proxmox: Segun los requisitos recomendados, el equipo puede arrancar proxmox.
- Puedo ejecutar el servidor ASO y el cliente del proyecto: PENDIENTE.
- Condiciones o comprobaciones pendientes: PENDIENTE.

## 2. Que limitaciones tendre con este hardware?

Analizar RAM, CPU, disco y red para las cargas previstas. Identificar lo
medido y lo estimado. 
En VirtualBox, investigar host real y VM: version,
RAM reservada al anfitrion, vCPU, VDI, espacio fisico y red local.
No se utiliza el Proxmox del centro como recurso.

### Reparto de recursos

| Elemento | CPU/vCPU | RAM | Disco | Justificacion |
|---|---|---|---|---|
| Proxmox | | | | |
| srv-aso | | | | |
| cli-linux | | | | |
| Plantilla, ISOs y copias | No aplica | No aplica | | |
| Margen de operacion | | | | |

Mostrar calculos de RAM y disco, reparto de vCPU, unidades y supuestos.
Explicar las cargas que pueden funcionar simultaneamente.

| Limitacion | Evidencia o estimacion | Consecuencia | Medida y limite que permanece |
|---|---|---|---|
| | | | |

## 3. Que componentes son mas criticos en mi servidor y por que?

Ordenar al menos tres componentes para este equipo y su servicio.
Distinguir cuello de botella, disponibilidad e integridad de los datos.

| Prioridad y componente | Funcion | Efecto si es insuficiente | Efecto si falla | Evidencia y justificacion |
|---|---|---|---|---|
| 1. | | | | |
| 2. | | | | |
| 3. | | | | |

Componente que mejoraria primero y motivo para priorizarlo frente a otro:
PENDIENTE.

## Fuentes tecnicas

Consultar al menos tres fuentes primarias, incluyendo Proxmox y
fabricante o plataforma virtual. Relacionarlas con las tres respuestas.

| Fuente y URL | Version/modelo y fecha de consulta | Afirmacion respaldada | Aplicacion al nodo |
|---|---|---|---|
| | | | |

## Dictamen de viabilidad

Apto, apto con condiciones o no apto para la propuesta actual: PENDIENTE.

Sintetizar las tres respuestas y las condiciones pendientes de comprobar.

## Evidencias y revision docente

Enlazar salidas revisadas desde ../evidencias/. Un listado automatico no
sustituye la investigacion. Registrar la pregunta de defensa y respuesta.

[Volver al indice](../README.md)
