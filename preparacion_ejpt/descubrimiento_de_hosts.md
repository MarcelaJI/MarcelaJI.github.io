---
layout: default
title: Preparación EJPTv2
---

# Descubrimiento de Hosts 🔍🖥️

El descubrimiento de hosts es la fase inicial de reconocimiento en la que se identifica qué dispositivos o sistemas están disponibles en una red.
Su objetivo es **mapear el alcance real del objetivo** antes de profundizar en el escaneo de puertos o vulnerabilidades.

Este proceso generalmente consiste en enviar paquetes específicos (ICMP, TCP, UDP) para provocar una respuesta que confirme que un host está activo.
La información obtenida incluye **direcciones IP vivas** y, en ocasiones, detalles básicos como el sistema operativo o la latencia.

## Comandos para descubrir equipos activos en nuestra red:

```bash
- ip a # Muestra la configuración y estado de todas las interfaces de red del sistema
- ifconfig # Permite ver direcciones IP, máscaras de red, estado (UP/DOWN), y estadísticas de tráfico 
- netdiscover -r <ip>/24 # Descubrimiento pasivo y activo de hosts en una red local
- fping -a -g <ip>/24 # Permite enviar pings ICMP a múltiples hosts de forma rápida y en paralelo
- masscan -p<puertos> -Pn <rango_de_red> # Descubrimiento de hosts al buscar puertos comunes (como 80, 443, 22) y ver quién responde
- arp-scan -I <interfaz_de_red> --localnet --ignoredups # Herramienta para descubrimiento de hosts en la red local usando ARP requests
- nmap -sn <ip>/24 # Escaneo de descubrimiento de hosts (sin escaneo de puertos). Manda paquetes ICMP a ese segmento de red
- nmap -sS --min-rate 5000 -p- --open <ip> -oN tcp_scan.txt # Podemos añadir multiples ips separadas por ","
- grep '^[0-9]' tcp_scan.txt | cut -d '/' -f1 | sort -u | xargs | tr ' ' ',' # Una lista limpia y única de IPs separadas por comas, útil para pasar a otras herramientas o scripts.
- nmap --open -p<puertos> -sC -sV <ips> -Pn -On full_scan.txt` # escaneo profundo para identificar servicios, versiones y puertos abiertos, con salida guardada para análisis posterior

```

---

## Análisis de Hosts

Una vez identificadas las direcciones IP, debemos analizarlas en detalle. Para ello, utilizaremos Nmap y determinaremos qué puertos están activos en cada host con el siguiente comando:

```bash
nmap -p- --open -T5 -sS -Pn -n -vvv <ip> -oN <output_name.txt
```

- -p- → escanea todos los puertos (1-65535).

- --open → muestra solo puertos abiertos.

- -T5 → modo de escaneo muy rápido (máxima velocidad).

- -sS → escaneo SYN (half-open scan), sigiloso y rápido.

- -Pn → no realiza ping previo, asume host activo.

- -n → no resuelve nombres DNS (más rápido).

- -vvv → salida muy detallada (nivel de verbosidad 3).

- (ip) → IP objetivo.

- -oN <output_name.txt> → guarda resultados en archivo texto legible.

Escaneo rápido y completo de puertos para encontrar servicios abiertos sin generar demasiada atención.

---


## 🔎 Puertos más comunes que podemos encontrar:

| Puerto | Protocolo | Servicio común | Descripción breve                       |
| ------ | --------- | -------------- | --------------------------------------- |
| 21     | TCP       | FTP            | Transferencia de archivos               |
| 22     | TCP       | SSH            | Acceso remoto seguro                    |
| 23     | TCP       | Telnet         | Acceso remoto no seguro                 |
| 25     | TCP       | SMTP           | Envío de correo                         |
| 53     | TCP/UDP   | DNS            | Resolución de nombres                   |
| 80     | TCP       | HTTP           | Web no segura                           |
| 110    | TCP       | POP3           | Correo entrante                         |
| 143    | TCP       | IMAP           | Correo entrante                         |
| 1521   | TCP       | Oracle DB      | Puerto por defecto para Oracle Database |
| 443    | TCP       | HTTPS          | Web segura                              |
| 445    | TCP       | SMB            | Compartición de archivos                |
| 3306   | TCP       | MySQL          | Base de datos                           |
| 3389   | TCP       | RDP            | Escritorio remoto Windows               |
| 5900   | TCP       | VNC            | Control remoto                          |

---

## 🔍 Análisis de Servicios y Versiones con Nmap

```bash
nmap -p<puertos> -sCV -oN <ip> <output_name.txt>
```

Escaneo detallado para identificar servicios, versiones y obtener información extra con scripts.

---

📜 Scripts específicos de Nmap por servicio

| Servicio   | Puerto común | Script(s) útiles (`--script=`)                                                  | Descripción                                                              |
| ---------- | ------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| HTTP/HTTPS | 80, 443      | `http-title`, `http-server-header`, `http-enum`, `http-methods`, `http-headers` | Enumera páginas, métodos, cabeceras y servidor web.                      |
| FTP        | 21           | `ftp-anon`, `ftp-syst`, `ftp-banner`                                            | Comprueba acceso anónimo, tipo de sistema y banner FTP.                  |
| SSH        | 22           | `ssh-hostkey`, `ssh2-enum-algos`                                                | Muestra claves del host y algoritmos permitidos.                         |
| SMTP       | 25           | `smtp-enum-users`, `smtp-commands`, `smtp-open-relay`                           | Enumera usuarios, comandos y verifica relay abierto.                     |
| DNS        | 53           | `dns-recursion`, `dns-service-discovery`                                        | Comprueba recursión y descubre servicios.                                |
| SMB        | 445          | `smb-enum-shares`, `smb-enum-users`, `smb-os-discovery`, `smb-security-mode`    | Enumera recursos compartidos, usuarios, SO y configuración de seguridad. |
| MySQL      | 3306         | `mysql-info`, `mysql-users`, `mysql-databases`                                  | Muestra versión, usuarios y bases de datos accesibles.                   |
| Oracle DB  | 1521         | `oracle-tns-version`, `oracle-enum-users`                                       | Muestra versión TNS y enumera usuarios.                                  |
| RDP        | 3389         | `rdp-enum-encryption`, `rdp-vuln-ms12-020`                                      | Enumera cifrados y prueba vulnerabilidad MS12-020.                       |
| VNC        | 5900         | `vnc-info`, `vnc-title`                                                         | Muestra información del servidor VNC y su banner.                        |

---

Un ejemplo de como podríamos ejecutar cualquier script:

```bash
nmap -p80 --script=http-title <ip_objetivo>
```

---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>