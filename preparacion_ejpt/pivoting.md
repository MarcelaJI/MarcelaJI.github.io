---
layout: default
title: Preparación EJPTv2
---

# Pivoting con Metasploit utilizando una máquina Windows 📡

El pivoting es una técnica esencial en la fase de post-explotación que permite a un atacante moverse lateralmente dentro de una red comprometida, utilizando un sistema ya infiltrado como punto de apoyo. En entornos Windows, Metasploit facilita este proceso mediante el uso de sesiones Meterpreter, tunelización y Port forwarding para acceder a sistemas internos que no son visibles desde el exterior.

----

## 📝 Objetivos principales del Pivoting:

🌐 Expandir el acceso dentro de la red interna.

🔥 Evadir restricciones de segmentación y firewalls.

🔒 Acceder a recursos internos que permanecen ocultos desde el exterior.

## Configuración de Pivoting en Metasploit

- Identificación de la red interna

El primer paso consiste en identificar las redes accesibles desde la máquina comprometida.

```bash
ipconfig          # Obtener información de interfaces y redes disponibles.
route print       # Ver las rutas de la tabla de enrutamiento.
arp -a            # Identificar hosts en la misma subred.
```

Una vez identificada una red interna, dejamos la sesión en segundo plano con Ctrl + Z. Verificamos las sesiones activas:

```bash
sessions -l       # Listar las sesiones activas.
```


- Escaneo de la red interna

Desde Metasploit, usamos el módulo ARP Scanner para descubrir equipos activos en la red interna:

```bash
use windows/gather/arp_scanner   # Identificar equipos activos en la red interna.
set RHOSTS <ip_víctima_windows/24>
set SESSION <session_id>          # Obtenido con sessions -l.
run
```

Esto nos mostrará las direcciones IP detectadas dentro del rango de red de la máquina Windows comprometida.

## Enrutamiento del tráfico con Autoroute

Ahora, configuramos el tráfico para que desde la máquina intermedia se reenvíe el tráfico hacia la máquina víctima final utilizando el módulo Autoroute:

```bash
use multi/manage/autoroute
show options                # Ver opciones disponibles.
set SESSION <session_id>    # Obtener con sessions -l.
run
```

Con esto, establecemos una ruta a través de la máquina intermedia, permitiendo el movimiento lateral dentro de la red.

## Escaneo de puertos de la máquina víctima final

Una vez configurado el enrutamiento, realizamos un escaneo de puertos para identificar los servicios expuestos por la máquina víctima final:

```bash
use scanner/portscan/tcp
show options                # Ver opciones necesarias.
set RHOSTS <ip_víctima_final>
run
```

## Configuración de Port Forwarding

Ahora, configuramos el port forwarding para redirigir tráfico desde la máquina víctima final hacia nuestro equipo atacante:

```bash
use post/windows/manage/portproxy
show options                # Ver opciones necesarias.
set CONNECT_ADDRESS <ip_víctima>   # IP de la máquina víctima final.
set CONNECT_PORT <puerto_víctima>  # Puerto de la víctima a atacar.
set LOCAL_ADDRESS 0.0.0.0          # Siempre usar 0.0.0.0.
set LOCAL_PORT <puerto_local>       # Puerto local donde recibir el tráfico.
set SESSION <session_id>            # Obtenido con sessions -l.
run
```

## Acceso al puerto redirigido

Por último, accedemos al puerto redirigido desde nuestro navegador utilizando la IP de la máquina intermedia y el puerto configurado:

```bash
<ip_máquina_intermedia>:<puerto_local>   # Ejemplo: 10.10.10.9:5000
```

Con esto, habremos establecido un túnel para acceder a los servicios internos de la red comprometida, superando las restricciones impuestas por firewalls y segmentaciones.

--- 
 