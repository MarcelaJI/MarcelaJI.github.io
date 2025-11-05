---
layout: default
title: Preparación EJPTv2
---

# 🚀 WINDOWS POST EXPLOTACIÓN 

La post-explotación es una fase crítica en las pruebas de penetración que ocurre después de obtener acceso inicial a un sistema. Esta etapa es fundamental para comprender el alcance real de una vulnerabilidad y evaluar el impacto potencial en la seguridad del sistema.

---

## 📝 La fase de post-explotación se centra en tres objetivos principales:

- Recolección de información del sistema comprometido.

- Escalada de privilegios.

- Movimiento lateral en la red.

## Técnicas de Reconocimiento del Sistema

-  Información del sistema

```bash
systeminfo  # Información general del sistema
wmic os get Caption, Version, BuildNumber  # Versión del sistema operativo
hostname  # Nombre del host
dir C:\Users  # Usuarios en el sistema
```

-  Información del usuario

```bash
whoami  # Usuario actual
whoami /priv  # Privilegios del usuario actual
net user  # Usuarios del sistema
net localgroup Administrators  # Usuarios con privilegios de administrador
```


- Si encontramos usuarios con privilegios, podemos intentar elevar privilegios usando exploits conocidos.

 Explotación del Kernel

```bash
systeminfo | findstr /B /C:"OS Version"  # Verificar versión del sistema operativo
wmic qfe get HotFixID  # Listar parches instalados
```

Consultar la siguiente web para exploits conocidos: [Exploit-DB](https://www.exploit-db.com/)


- 🔍 Búsqueda de Credenciales

```bash
findstr /si password *.txt *.ini *.config  # Buscar contraseñas en archivos de configuración
reg query HKLM /f password /t REG_SZ /s  # Buscar credenciales en el registro
```

- Análisis de Historial

```bash
type C:\Users\<usuario>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt  # Historial de comandos de PowerShell
type C:\Users\<usuario>\ntuser.dat.LOG1  # Registro de actividad del usuario
```

- Buscar Claves SSH

```bash
dir /s /b C:\Users\*.ssh\id_rsa  # Buscar claves privadas SSH
dir /s /b C:\Users\*.ssh\authorized_keys  # Claves autorizadas
```

- Configuraciones SUID/SGID (Equivalente a Windows: Archivos con permisos elevados)

```bash
icacls C:\Windows\System32  # Ver permisos de archivos del sistema
icacls C:\Users\<usuario> /grant Everyone:F  # Modificar permisos (requiere privilegios elevados)
```

- Tareas Programadas

```bash
schtasks /query /fo LIST /v  # Listar tareas programadas
dir C:\Windows\Tasks  # Ver tareas programadas manualmente
dir C:\Windows\System32\Tasks  # Tareas programadas por el sistema
```

- Servicios y Configuraciones Sensibles

```bash
wmic service list brief  # Listar servicios en ejecución
net start  # Ver servicios iniciados
Get-WmiObject Win32_Service | Select-Object Name, StartName  # Ver servicios con cuentas privilegiadas
```

- Configuración de Red y Conexiones

```bash
ipconfig /all  # Configuración de red
netstat -ano  # Conexiones activas y procesos asociados
arp -a  # Tabla ARP
route print  # Tabla de enrutamiento
```

- Archivos y Directorios Sensibles

```bash
dir /s /b C:\Users\*\AppData\Roaming\Microsoft\Windows\Recent  # Archivos recientes
dir /s /b C:\Users\*\Documents\  # Documentos del usuario
dir /s /b C:\Users\*\Desktop\  # Escritorio de los usuarios
dir /s /b C:\Windows\System32\config  # Archivos de configuración
```


- Archivos de Configuración de Tareas Programadas

```bash
dir /s /b C:\Windows\System32\Tasks  # Listar tareas programadas
dir /s /b C:\Windows\Tasks  # Listar tareas ocultas
```

--- 


<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>


