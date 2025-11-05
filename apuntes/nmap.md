---
layout: default
title: Apuntes
---

# Nmap y sus diferentes modos de escaneo

**Nmap** es una herramienta de escaneo de red gratuita de código abierto que se utiliza en pruebas de penetración (pentesting) para explorar y auditar redes y sistemas informáticos.

Con **Nmap**, los profesionales de seguridad pueden identificar los hosts conectados a una red, los servicios que se están ejecutando en ellos y las vulnerabilidades que podrían ser explotadas por un atacante. La herramienta es capaz de detectar una amplia gama de dispositivos, incluyendo enrutadores, servicios web, impresoras, cámaras IP, sistemas operativos y otros dispositivos conectados a una red.

Asimismo, esta herramienta posee una variedad de funciones y características avanzadas que permiten a los profesionales de seguridad adaptar la misma a sus necesidades específicas. Estas incluyen técnicas de escaneo agresivas, capacidades de scripting personalizadas, y un conjunto de herramientas auxiliares que pueden ser utilizadas para obtener información adicional sobre los hosts objetivo.

Para englobar todos los puertos con **Nmap**, ejecutamos:

```bash
nmap -p- <IP>
```

Para englobar los puertos más comunes ejecutamos:

```bash
nmap --top-ports 500 <IP>
```

Y para ver solo puertos abiertos ejecutamos:

```bash
nmap -p- --open <IP>
```
---

Estos son algunos de los parámetros más comunes para hacer escaneos con **nmap**:

- Con el parámetro -v, le digo que me haga el escaneo en modo verbose, lo que significa es aumentar el nivel de mensajes detallado (-vvv para aumentar el efecto).

- Con el parámetro -n, le digo que no me haga resolución DNS.

- Con el parámetro -T, ajustamos la velocidad del escaneo.

- Con el parámetro -Pn, para que dé por hecho que el host está activo.

- Con el parámetro --min-rate 5000, Nmap establece la velocidad mínima de envío de paquetes por segundo durante un escaneo, es decir que le estoy diciendo a Nmap: "No envíes menos de 5000 paquetes por segundo durante el escaneo". En conclusión este parámetro nos ayuda cuando necesitamos escaneos rápidos en situaciones donde necesitamos velocidad y eficiencia.

- Con el parámetro -sC se refiere al uso de scripts NSE predeterminados, este parámetro le dice a **Nmap**: "Ejecuta los scripts predeterminados del motor de scripts de Nmap(NSE: Nmap Scripting Engine).", así mismo con el parámetro **--script**, permite a Nmap ejecutar scripts del Nmap Scripting Engine (NSE). A diferencia de -sC (que ejecuta solo los scripts predeterminados), --script te da control total sobre qué scripts usar. Ejemplo:

```bash
nmap --script=default
nmap --script=auth
nmap --script=vuln
```

- Para hacer un escaneo sigiloso con -sT, de Three-Wall Handshake, podemos hacer una captura con **tcpdump**, para luego ver que está pasando en el **wireshark** con la captura que hemos hecho y ver como está el proceso del Three-Wall Handshake. 

Para poder ver la interfaz de la red podemos ejecutar varias opciones por ejemplo:

```bash
ifconfig
```
o

```bash
ip addr show
```

Lo que hacemos es, antes de ejecutar **Nmap**, en una terminal aparte ejecutamos:

```bash
tcpdump -i enp0s3 -w Captura.cap -v
```

Que el parámetro -i es para poner la interface de red, y -w de write para que se escriba en Captura.cap y -v de verbose.

Cuando lo ejecutamos, ejecutamos también Nmap para que se capture el tráfico según el puerto que hayamos ejecutado para que se capture.
Luego para abrir **wireshark** y ver como ha ido el -sT,  lo abrimos en segundo plano ejecutando:

```bash
wireshark Captura.cap &>/dev/null & disown
```

Con esto le estoy diciendo que las salidas de error me las envíe a dev/null ya que no me interesa verlas y además que el proceso me lo haga en disown es decir, en segundo plano para que wireshark no dependa de la terminal si no de una proceso aparte , y así si cierro la terminal que wireshark no se cierre.

Para enumerar activos o equipos que estén configurados dentro de la red ejecutamos:

```bash
arp-scan -I enp0s3 --localnet
```

- También se puede hacer con **Nmap** -sn, lo que hace es un barrido con ping para saber si el equipo está encendido o no. Por ejemplo:

```bash
nmap -sn 192.168.1.0/24
```

- Para ver las versiones y hacer que el escaneo sea más óptimo en una fase de reconocimiento, ejecutamos:

```bash
nmap -p22,80 -sV
```

- Detección del sistema operativo y servicios que corren detrás, aunque no es muy recomendable usarlo porque hace muchas peticiones y es muy agresivo:   

```bash
nmap -O o nmap -A
```

- Para hacer un escaneo silencioso ejecutamos:

```bash
nmap -sS
```

- Si queremos exportar un resultado ejecutamos:

```bash
nmap -oN <archivo.txt> <IP>
```

Un escaneo completo inicial y recomendado podría ser:

```bash
nmap -p- --open -sS --min-rate 5000 -Pn -n -vvv -oN result.txt <IP>
```

---



<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>>



    

