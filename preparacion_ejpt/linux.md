---
layout: default
title: Preparación EJPTv2
---

# Escala de privilegios en Linux 


## Información del Sistema

```bash
uname -a # Información detallada del kernel y sistema operativo.
cat /etc/issue / cat /etc/*-release # Versión de la distribución.
hostname # Nombre del host.
echo $PATH # Ver como está el path.
env # Variable del entorno.
lscpu # Descubrir información adicional del sistema.
```

## Información de Usuario y Grupos

```bash
whoami # Identificar usuario actual
ls -la /home/ # Directorios de usuarios.
grep "*sh$" /etc/passwd # Ver que usuarios tienen shells de inicio de sesión.
id # id de usuarios y grupos
cat /etc/passwd | grep /bin/bash # Lista usuarios del sistema y filtramos por los que tengan una bash
cat /etc/group # Listar grupos.
history # Muestra el historial de comandos
```

## Información de Red

```bash
ifconfig / ip a # Muestra interfaces de red.
netstat -antup # Conexiones activas y puertos abiertos.
route / ip route # Tabla de enrutamiento.
cat /etc/resolv.conf # Configuración DNS.
arp -a # Tabla ARP.
```

##  Archivos y Directorios Sensibles

```bash
ls -l ~/.ssh # Lista el contenido del servicio SSH.
ls -l /tmp /var/tmp /dev/shm # Buscar archivos temporales.
find / -perm -4000 2>/dev/null # Buscar archivos con binarios SUID.
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null # Buscar archivos con binarios SUID.
find / -perm -2000 2>/dev/null # Archivos SGID.
find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null # Búsqueda de archivos de historial
find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null # Buscar archivos grabables.
find / type -f -name "*.conf" 2>/dev/null # Archivos de configuración.
find / -type d -name ".*" -ls 2>/dev/null # Buscar directorios ocultos.
find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null | grep <username> # Buscar archivos ocultos.
find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null # Directorios escribibles.
find / -writable -type d 2>/dev/null # Directorios escribibles.
find / -type f -name "*.sh" 2>/dev/null | grep -v "src\|snap\|share" # Buscar binarios .sh
apt list --installed | tr "/" " " | cut -d" " -f1,3 | sed 's/[0-9]://g' | tee -a installed_pkgs.list # Enumeración de servicios y componentes internos de Linux
for i in $(curl -s https://gtfobins.github.io/ | html2text | cut -d" " -f1 | sed '/^[[:space:]]*$/d');do if grep -q "$i" installed_pkgs.list;then echo "Check GTFO for: $i";fi;done # Comprobar en GTFOBINS
cat wp-config.php | grep 'DB_USER\|DB_PASSWORD' # credenciales de la base de datos MySQL dentro de los archivos de configuración de WordPress
find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null # .config en proc y mail,
sudo -l # Busca binarios que podamos utilizar como el usuario con máximos privilegios (root).
```

##  Procesos y Servicios

```bash
ps au # Procesos en ejecución.
ps aux | grep root # Ver que procesos está ejecutando root.
top # Procesos en tiempo real.
service --status-all # Estado de servicios.
systemctl list-units # Unidades sustemd activas.
```

##  Tareas Programadas

```bash
ctrontab -l # Tareas cron del usuario actual.
ls -la /etc/cron.daily/
ls -la /etc/cron* # Archivos cron del sistema.
cat /etc/crontab  # Configuración cron del sistema.
```

##  Logs y Auditoría

```bash
cat /var/log/auth.log # Logs de autenticación.
cat /var/log/syslog # Logs del sistema.
last # Últimos inicios de sesión.
```

##  Información de Seguridad

```bash
cat /etc/shadow # Hashes de contraseñas (requiere root)
iptables -L # Reglas de firewall.
cat /etc/ssh/sshd_config # Configuración SSH
```

---

### Material adicional:

[GTFOBins](https://gtfobins.github.io) -> Con esta web podemos buscar tanto loos binarios SUID y los archivos que podamos ejecutar como el usuario con máximos privilegios al utilizar **sudo -l**.

---


<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
