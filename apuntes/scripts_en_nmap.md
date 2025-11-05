---
layout: default
title: Apuntes
---

# Uso de scripts y categorías en nmap para aplicar reconocimiento

Una de las características más poderosas de **Nmap** es su capacidad para automatizar tareas utilizando **scripts personalizados**. Los scripts de Nmap permiten a los profesionales de seguridad automatizar las tareas de reconocimiento y descubrimiento en la red, además de obtener información valiosa sobre los sistemas y servicios que se están ejecutando en ellos. El parámetro **–script** de Nmap permite al usuario seleccionar un conjunto de scripts para ejecutar en un objetivo de escaneo específico.

Existen diferentes categorías de scripts disponibles en Nmap, cada una diseñada para realizar una tarea específica. Algunas de las categorías más comunes incluyen:

- **default**: Esta es la categoría predeterminada en Nmap, que incluye una gran cantidad de scripts de reconocimiento básicos y útiles para la mayoría de los escaneos.
- **discovery**: Esta categoría se enfoca en descubrir información sobre la red, como la detección de hosts y dispositivos activos, y la resolución de nombres de dominio.
- **safe**: Esta categoría incluye scripts que son considerados seguros y que no realizan actividades invasivas que puedan desencadenar una alerta de seguridad en la red.
- **intrusive**: Esta categoría incluye scripts más invasivos que pueden ser detectados fácilmente por un sistema de detección de intrusos o un Firewall, pero que pueden proporcionar información valiosa sobre vulnerabilidades y debilidades en la red.
- **vuln**: Esta categoría se enfoca específicamente en la detección de vulnerabilidades y debilidades en los sistemas y servicios que se están ejecutando en la red.

En conclusión, el uso de scripts y categorías en Nmap es una forma efectiva de automatizar tareas de reconocimiento y descubrimiento en la red. El parámetro **–script** permite al usuario seleccionar un conjunto de scripts personalizados para ejecutar en un objetivo de escaneo específico, mientras que las diferentes categorías disponibles en Nmap se enfocan en realizar tareas específicas para obtener información valiosa sobre la red.

Podemos ejecutar por ejemplo:

```bash
nmap -p22 192.168.111.1 -sCV
```

podemos buscar scripts con locate .nse

Para buscar según la categoría podemos ejecutar:

```bash
locate .nse | xargs grep "categories"
```

Para ordenar esas categorías y además que nos muestre cuantas hay ejecutamos:

```bash
locate .nse | xargs grep "categories" | grep -oP '".*?"' | sort -u | wc -l
```

Podemos combinar categorías y así es menos agresivo, ejecutando:

```bash
nmap -p22 192.168.111.1 --script="vuln and safe"
```

---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>>

