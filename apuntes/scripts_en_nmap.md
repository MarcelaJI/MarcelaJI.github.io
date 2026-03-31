---
layout: default
title: Apuntes
---

## Uso de scripts y categorías en nmap para aplicar reconocimiento

En Nmap podemos automatizar tareas utilizando scripts personalizados. El parámetro --script de Nmap nos permite seleccionar un conjunto de scripts para ejecutar en un objetivo de escaneo específico.

Existen diferentes categorías de scripts disponibles en Nmap, cada una diseñada para realizar una tarea específica. Algunas de las categorías más comunes incluyen:

- **default**: Esta es la categoría predeterminada en Nmap, que incluye una gran cantidad de scripts de reconocimiento básicos y útiles para la mayoría de los escaneos.
- **discovery**: Esta categoría se enfoca en descubrir información sobre la red, como la detección de hosts y dispositivos activos, y la resolución de nombres de dominio.
- **safe**: Esta categoría incluye scripts que son considerados seguros y que no realizan actividades invasivas que puedan desencadenar una alerta de seguridad en la red.
- **intrusive**: Esta categoría incluye scripts más invasivos que pueden ser detectados fácilmente por un sistema de detección de intrusos o un Firewall, pero que pueden proporcionar información valiosa sobre vulnerabilidades y debilidades en la red.
- **vuln**: Esta categoría se enfoca específicamente en la detección de vulnerabilidades y debilidades en los sistemas y servicios que se están ejecutando en la red.

---

Podemos compactar estos dos parámetros que es justamente lo mismo como si lanzáramos -sC y -sV por separado 

```bash
nmap -p22 -sCV 192.168.211.1
```

Estos scripts están en los scripts básicos que suele lanzar -sC automáticamente 

```bash
locate ftp-anon.nse
locate http-robots.txt.nse
```

---

Podemos filtrar por categorías y así buscar scripts:

```bash
locate .nse | xargs grep "categories" | grep -oP '".*?"' | sort -u
```

Podemos englobar dos categorías tal que así:

```bash
nmap -p22 192.168.111.1 --script="vuln and safe"
```

Así solo lanzamos scripts que pertenecen a la categoría *vuln and safe* simultáneamente

---

Con:

```bash 
lsof -i:80
```

Puedo validar si ese puerto está en uso 

Para montarme un servidor lo hacemos tal que así:

```bash
python3 -m http.server 80
```

Para saber el PID que es el identificador de este proceso

```bash 
lsof -i:80
pwdx 1355887
```

Podemos utilizar el siguiente script para hacer fuzzing en el servidor que nos acabamos de montar:

```bash
nmap -p80 192.168.111.42 --script http-enum
```

