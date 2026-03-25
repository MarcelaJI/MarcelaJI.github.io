---
layout: default
title: Apuntes
---

## NMAP

*Nmap* es una herramienta de código abierto utilizada para analizar redes y realizar auditorias de seguridad. Con Nmap podemos identificar que hosts están conectados a una red, también los servicios que se están ejecutando y las vulnerabilidades que podrían ser explotadas por un atacante.

Para enumerar activos dentro de nuestra red local ejecutamos:

```bash
arp-scan -I ens33 --localnet
```

Con Nmap también lo podemos hacer con un barrido con ping para ver si el equipo en cuestión está encendido tal que así:

```bash
nmap -sn 192.168.111.0/24
```

Este comando ```route -n``` sirve para ver las tablas de red de tu sistema usando direcciones IP directamente (sin resolver nombres), lo que lo hace más rápido.

```bash
route -n
```


Para enumerar los primeros 100 puertos ejecutamos este parámetro:

```bash
nmap -p1-100 192.168.211.1
```

Y si queremos englobar todo el rango entero ejecutamos:

```bash
nmap -p1-65535 192.168.211.1 
```

o

```bash
nmap -p- 192.168.211.1
```

Para escanear los 500 puertos más comunes:

```bash
nmap --top-ports 500 192.168.211.1
```

Para que me reporte solo puertos abiertos:

```bash
nmap -p- --open 192.168.211.1
```

Para ganar agilidad en la velocidad del escaneo podemos ejecutar:

```bash
nmap -p- --open -T5 192.168.211.1 -v -n
```


Un escaneo por *UDP* es tal que así:

```bash
nmap --top-ports 500 --open -sU 192.168.211.1 -v -n 
```

Para ver la versión y servicios de puertos que ya sé que están abiertos ejecuto lo siguiente:

```bash
nmap -p22,80 -sV 192.168.211.1
```


Cabe mencionar que si no le especificamos a nmap nada por defecto tirará contra el protocolo *TCP*

Un puerto puede estar en diferentes estados tales como:

- Abierto: el puerto responde y acepta conexiones (hay un servicio enchufado).
- Cerrado: el puerto responde, pero no hay servicio disponible.
- Filtrado: el puerto no responde porque un firewall u otro sistema bloquea o descarta las peticiones.

## Estos son algunos parámetros de nmap:

- El parámetro ```-v``` activa el modo verbose, mostrando más detalles del escaneo en tiempo real.

- El parámetro ```-n``` nos permite no aplicar la resolución DNS.

- El parámetro ```-T``` nos ayuda a seleccionar la plantilla de temporizado y renderizado de forma que podemos ajustar la velocidad.

- El parámetro -Pn hace que no se compruebe si el host está activo, es decir, asume que el host está "vivo" y escanea directamente los puertos.

- El parámetro -O intenta detectar cual es el sistema operativo (es bastante agresivo)

- El parámetro -sT sirve para hacer un escaneo TCP completo (connect), es decir, intenta establecer la conexión completa con cada puerto para comprobar si está abierto. Básicamente enviamos SYN para iniciar conexión, si nos responde RST el puerto está cerrado y si responde SYN/ACK el puerto está abierto y se completa la conexión.

SYN -> (RST (cerrado) | SYN/ACK (abierto) -> ACK (established))

Si queremos ver como se establece esta conexión:

```bash
nmap -p- --open -T5 192.168.211.1 -v -n
```

En paralelo podemos ver el trafico con wireshark y hacer una captura de ello tal que así:

Para crear una captura en la terminal:

```bash
tcpdump -i ens33 -w Captura.cap -v 
```

- -i -> interfaz de red
- -w -> viene de write indicando a donde quiero depositar el contenido
- -v -> verbose 

Para ver nuestra interfaz de red ejecutamos:

```bash
iwconfig
```

Luego para ver nuestra captura ejecutamos wireshark:

```bash
wireshark Captura.cap &>/dev/null & disown
```

- ```&/dev/null``` -> oculta toda la salida (stdout y errores)
- ```&``` -> ejecuta el comando en segundo plano
- ```disown``` -> desvincula el proceso de la terminal (sigue corriendo aunque cerremos sesión)

Podemos aplicar este filtro en wireshark si queremos ver un puerto especifico por ejemplo el 22

```bash
tcp.port == 22
```






    

