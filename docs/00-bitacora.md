# Bitacora de sesiones

La bitacora es el registro cronologico del trabajo. Anade una entrada al final
de cada sesion y conserva las anteriores. Escribe datos comprobables y enlaza
las evidencias utiles; evita frases generales como "he trabajado en Proxmox".

## Sesion 01 - 6/10

- Objetivo: iniciar GitHub y la documentacion Markdown.
- Acciones realizadas: repositorio creado y primer commit: configuraciones, cambios o investigacion.
- Decisiones y motivos: repositorio creado: eleccion realizada y alternativas valoradas.
- Pruebas y resultados: comandos en pagina github: resultado esperado, comando o metodo y resultado obtenido.
- Documentos o evidencias: [Ficha inicial](00-ficha-inicial.md).
- Incidencias y solucion o estado pendiente: Ningun problema.
- Siguiente paso: preparar y empezar el proxmox en maquina fisica y virtual : accion concreta para la proxima sesion.

## Sesion 02 - 13/10

- Objetivo: Completar Informacion sobre equipo local y requisitos proxmox
- Acciones realizadas: Obtención de informacion de maquina fisica y comparativa con requerimiento proxmox
- Decisiones y motivos: Repositorio creado: eleccion realizada y alternativas valoradas.
- Pruebas y resultados: Toda la informacion la he podido obtener de la BIOS, menos la targeta de red que he usado el comando lshw.
- Documentos o evidencias: [Inventario Hardware](01-inventario-hardware.md).
- Incidencias y solucion o estado pendiente: Ningun problema.
- Siguiente paso: el siguiente paso es empezar a preparar proxmox en VirtualBox

## Sesion 03 - 20/10

- Objetivo: Diseñar la estructura y diagrama de red.
- Acciones realizadas: Markdown rellenado con todos los elementos (VirtualBox, VM/Proxmox) con IPs y descripciones breves.
- Decisiones y motivos: He actuado mas libremente en cuanto a representar la informacion en el markdown, me ha parecido mas comodo de esta manera.
- Pruebas y resultados: He utilizado la informacion de la web del projecto (Taller Proxmox y Conocer Proxmox)
- Documentos o evidencias: [Diagrama Red](02-diagrama-red.md).
- Incidencias y solucion o estado pendiente: Ningun problema.
- Siguiente paso: Lo sigueinte es empezar con la instalacion de proxmox en virtualbox.

## Sesion 04 - 27/10

- Objetivo: Crear e instalar maquina proxmox y comprobarcion en navegador
- Acciones realizadas: Maquina creara y configurada y proxmox instalado y comprobado con capturas en evidencias.
- Decisiones y motivos: He configurado la maquina antes de inciar la instalacion para que no de errores.
- Pruebas y resultados: He ido tirando a base de prueba y error probando todo lo evidente, direcciones IP, adaptador mal configurado y red Host-Only creada.
- Documentos o evidencias: [Instalacion Proxmox](03-instalacion-proxmox.md).
- Incidencias y solucion o estado pendiente: El primer problema a sido que he descargado mal la ISO, me he descargado para ARM64, aparte de eso ningun problema a destacar.
- Siguiente paso: Lo sigueinte sera confgurar y crear las maquinas cli-linux y server-aso dentro de proxmox.

## Sesion 05 - 10/11

- Objetivo: Volver a crear maquina proxmox con nueva configuracion.
- Acciones realizadas: Maquina creada, configurada y proxmox instalado, configurado y listo para crear maquinas srv-aso y cli-linux.
- Decisiones y motivos: He decidido utilizar 2 nucleos de CPU, 6 GB de RAM y 80 de almacenamiento dinamico.
- Pruebas y resultados: He probado a acceder desde el navegador con la IP de administracion cambiada y funciona correctamente.
- Documentos o evidencias: [Instalacion Proxmox](03-instalacion-proxmox.md).
- Incidencias y solucion o estado pendiente: Ninguno
- Siguiente paso: Lo sigueinte sera configurar y crear las maquinas cli-linux y server-aso dentro de proxmox.

## Sesion 06 - 17/11

- Objetivo: Completar el punto 3 y 4, Terminar de configurar Proxmox, comprobar y registrar informacion como el almacenamiento, los recursos disponibles y el funcionamiento de red.
- Acciones realizadas: Registrar informacion relevante: almacenamiento recursos y configuracion de red.
- Decisiones y motivos: Tendre que subir los nucleos a 4 para repartir los recursos de la maquina.
- Pruebas y resultados: Toda la informacion este guardarda y registrada en [Instalacion Proxmox](03-instalacion-proxmox.md)
- Documentos o evidencias: [Instalacion Proxmox](03-instalacion-proxmox.md).
- Incidencias y solucion o estado pendiente: Ninguno
- Siguiente paso: Crear plantillas para contenedores.


Anadir una entrada con esta estructura en cada sesion. El historial de
GitHub registra los commits; no hace falta incluir el hash del propio
commit dentro de su entrada de bitacora.



[Volver al indice](../README.md)
