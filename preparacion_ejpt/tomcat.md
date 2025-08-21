---
layout: default
title: Preparación EJPTv2
--- 

# Tomcat 🌐

Apache Tomcat es un servidor de aplicaciones ampliamente utilizado para ejecutar aplicaciones web en Java. Debido a su popularidad, es un objetivo frecuente en auditorías de seguridad y pruebas de penetración.


---

## 🕵️ Identificación de la Versión de Apache Tomcat

Determinar la versión del servidor es fundamental para detectar posibles vulnerabilidades. Podemos hacerlo de varias maneras:

- Reconocimiento con Nmap

```bash
nmap -sV --script http-tomcat-enum <url>
```

- Reconocimiento con WhatWeb

```bash
whatweb -v <url> # Muestra detalles de la versión detectada.
```

- Accediendo al Panel de Administración

En muchos casos, la versión de Tomcat se puede encontrar directamente en su panel de administración:

```bash
http://<ip>:8080
```

Si la consola de administración es accesible, generalmente aparece en la página principal o en la sección "Server Status".

---

### ✔ Check List - Apache Tomcat


- /manager/html (Consola de administración de Tomcat)


- /host-manager/html (Administrador de hosts virtuales)


- /examples/ (Directorio de ejemplos (puede contener código vulnerable)


- /docs/ (Documentación del servidor (posible información sensible)


- /conf/tomcat-users.xml (Archivo de configuración de usuarios)


- /logs/ (Registros del servidor)


- /backups/ (Posibles copias de seguridad accesibles)

 *💡 Importante: Si el acceso a estos directorios no está restringido, puede representar una vulnerabilidad grave.


## 🔑 Enumeración de Usuarios en Apache Tomcat

Tomcat almacena credenciales en tomcat-users.xml. Si tenemos acceso, podemos enumerar los usuarios configurados:

```bash
cat /etc/tomcat*/tomcat-users.xml
```

Si no tenemos acceso directo, podemos intentar un escaneo con Metasploit:

```bash
use auxiliary/scanner/http/tomcat_mgr_login
set RHOSTS <url>
set USER_FILE /usr/share/wordlists/metasploit/tomcat_mgr_default_users.txt
set PASS_FILE /usr/share/wordlists/rockyou.txt
run
```

💡 Explicación:

✔ tomcat_mgr_login → Escanea credenciales por defecto de Tomcat.

✔ USER_FILE y PASS_FILE → Diccionarios de usuario y contraseña.

