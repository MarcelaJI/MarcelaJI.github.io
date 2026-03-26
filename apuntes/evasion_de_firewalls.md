---
layout: default
title: Apuntes
---

## Técnicas de evasión de Firewalls (MTU, Data Length, Source Port, Decoy, etc.)

Un *firewall* es un sistema (software o hardware) que controla el tráfico de red, permitiendo o bloqueando conexiones según reglas de seguridad.

- En *nmap* el parámetro ```-f``` nos ayuda a fragmentar paquetes, con el objetivo de evadir algunos firewalls o sistemas de detección.

```bash
nmap -p22 192.168.211.1 -f
```

Lo que podemos hacer por ejemplo en wireshark filtrar por:

```bash
ip.flags.mf == 1
```

Esta es una forma de filtrar por paquetes fragmentados y los que no son fragmentados se igualan a 0

```bash
ip.flags.mf == 0
```

En algunos casos cuando un puerto esté filtrado podemos usar este parámetro para evadir el firewall.

- Podemos utilizar el parámetro ```--mtu ``` -> implica ajustar el tamaño de los paquetes que se envían para evitar la detección por parte del Firewall. Tiene que ser múltiplo de 8, por ejemplo: 8,16, 24 etc.

Lo podemos hacer tal que así:

```bash
nmap -p22 192.168.211.1 --mtu 8
```

- Podemos utilizar el parámetro ```-D``` (Decoy) -> nos permite enviar paquetes falsos a la red para confundir a los sistemas de detección por parte del Firewall. permite al usuario configurar manualmente un puerto de origen aleatorio o un puerto específico para evadir la detección de Firewall.

Lo podemos hacer tal que así:

```bash
nmap -p22 192.168.211.1 -D 192.168.111.215
```

Lo podemos comprobar en wireshark con estos parámetros:

```bash
tcp.port == 22
```

Y podemos ver que una dirección IP de origen a tramitado un paquete al destino y así el firewall no sabe a que dirección IP apuntar, así mismo podemos poner muchas direcciones IP para evadir la detección del Firewall.

- Podemos utilizar el parámetro ```--source-port``` -> nos ayuda a configurar manualmente el número de puerto de origen de los paquetes enviados, permite especificar manualmente un puerto de origen aleatorio o un puerto específico para evadir la detección del Firewall.

Lo podemos hacer tal que así:

```bash
nmap -p22 192.168.211.1. --open -T5 -v -n --source-port 53
```

- Podemos utilizar el parámetro ```--datalength``` -> se basa en ajustar la longitud de los datos enviados para que sean lo suficientemente cortos como para pasar por el firewall sin ser detectados.

Así:

```bash
nmap -p22 192.168.211.1 --data-length 21
```

- Podemos utilizar el parámetro ```--spoof-mac```-> se basa en cambiar la dirección MAC del paquete para evitar la detección del Firewall.

Así:

```bash
nmap -p22 192.168.211.1 --spoof-mac Dell -Pn
```

O:

```bash
nmap -p22 192.168.211.1 --spoof-mac 00:11:22:33:44:55 -Pn
```

- Podemos utilizar el parámetro ```-sS```-> es una técnica para hacer escaneos sigilosos y evitar la detección del Firewall. Permite a los usuarios realizar un escaneo de tipo SYN sin establecer una conexión completa, lo que permite evitar la detección del Firewall.

Así:

```bash
nmap -p- --open -sS --min-rate 5000 -v -n -Pn 192.168.211.1 
```





---
