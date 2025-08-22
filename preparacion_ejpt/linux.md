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

