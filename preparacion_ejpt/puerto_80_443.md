---
layout: default
title: Preparación EJPTv2
---

## Puerto 80/443 - HTTP/HTTPS

Al realizar un escaneo de puertos, es común encontrar los puertos 80 y 443 abiertos. Para analizar los servicios y versiones en ejecución en estos puertos, utilizaremos la herramienta Nmap, lo que nos permitirá identificar cabeceras, tecnologías y otros detalles relevantes.

```bash
ls -la /usr/share/nmap/scripts/ | grep -e "http" # Ver los scripts de Nmap para HTTP.
```

## 📜 Scripts Específicos de Nmap

Una vez obtenido el informe de servicios y versiones de cada puerto, es importante recordar que Nmap incluye scripts especializados para un análisis más profundo. Estos scripts nos permiten identificar configuraciones específicas y posibles vulnerabilidades.

```bash
nmap -p80,443 <ip_victima> -sCV
nmap -p80,443 <ip_victima> --script=http-headers
nmap -p80,443 <ip_victima> --script=http-title
nmap -p80,443 <ip_victima> --script=http-server-header
nmap -p80,443 <ip_victima> --script=http-methods
nmap -p80,443 --script=http-headers,http-title,http-server-header,http-methods <ip_victima>
```

### 🔍 Detección de Vulnerabilidades en Servidores Web

Para detectar posibles vulnerabilidades en servidores HTTP, utilizamos el siguiente comando:

```bash
nmap -p 80,443 --script=http-vuln* <ip_victima>
```

### 🔐 Fuerza Bruta en Autenticación HTTP

```bash
nmap -p 80,443 --script=http-brute <ip_victima>
```

---

## 🛠 Reconocimiento con Metasploit

```bash
msfconsole -q # Iniciar Metasploit en modo silencioso.
use auxiliary/scanner/http/http_version
set RHOSTS <ip_victima>
set RPORT 80
exploit
```

```bash
msfconsole -q
use auxiliary/scanner/http/http_version
set RHOSTS <ip_victima>
set RPORT 443
exploit
```

Estos comandos proporcionan una visión inicial del servidor web. Luego, podemos utilizar WhatWeb para identificar tecnologías web en sitios o servidores.

## 🔍 Características Principales de WhatWeb

- Identificación de CMS como WordPress, Joomla, Drupal.
- Detección de frameworks como Laravel, Django, Ruby on Rails.
- Reconocimiento de servidores web (Apache, Nginx, IIS).
- Extracción de versiones de software y posibles vulnerabilidades.
- Posibilidad de escaneo sigiloso o agresivo.

```bash
whatweb <url> # Análisis básico.
whatweb -v <url> # Escaneo detallado con más información.
```

## 🔍 Nikto: Escaneo de Vulnerabilidades Web en Puertos 80 y 443

Nikto es una herramienta de escaneo de seguridad web que permite detectar vulnerabilidades en servidores HTTP y HTTPS, incluyendo configuraciones incorrectas, software obsoleto y archivos sensibles expuestos.

```bash
nikto -h <url> -p 80 # Escaneo básico del puerto 80.
nikto -h <url> -p 443 -ssl # Escaneo con detección SSL/TLS.
nikto -h <url> -p 80,443 # Escaneo en ambos puertos simultáneamente.
nikto -h <url> -p 443 -Display V # Escaneo con más detalles.
nikto -h <url> -p 443 -nossl # Evitar advertencias SSL.
```

### 🚀 Automatización del Escaneo con Múltiples Objetivos

Si tienes una lista de IPs/Dominios, puedes usar un archivo targets.txt:

```bash
nikto -h targets.txt
```

### 🎯 Análisis con la Herramienta Curl:

```bash
curl -v http://<ip/dominio> # Consulta básica del puerto 80.
curl -v https://<ip/dominio> # Consulta básica del puerto 443.
curl -I http://<ip/dominio> # Extracción de encabezados HTTP.
```

Después de realizar múltiples escaneos y emplear diversas herramientas para identificar tecnologías, versiones, CMS y otros componentes, procederemos a analizar en detalle los distintos CMS detectados. Asimismo, exploraremos herramientas adicionales que permitan obtener información más específica sobre cada URL en proceso de auditoría.

## Fuzzing, CMS y Herramientas

💡 Uno de los aspectos más relevantes al analizar una aplicación web es la identificación del CMS (Sistema de Gestión de Contenidos) utilizado. Esto nos permitirá seleccionar las herramientas más adecuadas para llevar a cabo la auditoría de seguridad, aunque en muchos casos se emplearán metodologías similares.

Los CMS más comunes que probablemente encontraremos incluyen WordPress, Joomla y Drupal.

---
