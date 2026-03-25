---
layout: default
title: Preparación EJPTv2
---

## 📂 Puerto 21 - FTP (File Transfer Protocol) 🔄

Es el puerto estándar para el protocolo FTP, usado para la transferencia de archivos entre clientes y servidores.
Permite subir, descargar y gestionar archivos en un servidor remoto.
FTP suele usar autenticación básica y transmite datos en texto claro, lo que puede ser un riesgo de seguridad.

---


## Reconocimiento del puerto 21 🔍

Si encontramos el puerto 21 abierto, debemos centrarnos en verificar si el acceso mediante el usuario anonymous está habilitado. Para ello, podemos utilizar los scripts de Nmap:

```bash 
ls -lah /usr/share/nmap/scripts | grep "ftp-*"
nmap --script=ftp-anon -p 21 <ip_objetivo>
nmap --script "ftp-*" -p 21 <ip_objetivo>
```

- ls -lah /usr/share/nmap/scripts | grep "ftp-*": Listamos todos los scripts NSE de Nmap relacionados con FTP, útiles para escaneos específicos de ese servicio.
- nmap --script=ftp-anon -p 21 <ip_objetivo>: Identificar si un servidor FTP permite acceso anónimo, lo cual puede ser un riesgo de seguridad.
- nmap --script "ftp-*" -p 21 <ip_objetivo>: Realiza un escaneo completo de pruebas y enumeración FTP usando múltiples scripts para detectar vulnerabilidades, configuraciones y detalles del servicio.

---

Si el reporte indica que el acceso anónimo (anonymous) está habilitado, nos conectamos al FTP así:

```bash
ftp <ip_objetivo>
```

Al pedir usuario, se escribe:

```bash
anonymous
```

Y como contraseña, usualmente se escribe anonymous o simplemente se presiona Enter.


Si el inicio de sesión con el usuario anonymous no estuviera habilitado, podríamos utilizar la herramienta Hydra para realizar pruebas de acceso mediante la siguiente sintaxis:

```bash
hydra -l <username> -P /usr/share/wordlists/rockyou.txt ftp://<IP>
```

Una vez que hayamos conseguido acceder al servicio FTP, independientemente del método utilizado, es fundamental conocer y utilizar una serie de comandos clave para interactuar con el sistema y verificar qué opciones están disponibles.

```bash
ls - # Listar los directórios o archivos que hay disponibles. 
get <nombre_archivo> - # Descargar archivo nombrado.
put <nombre_archivo> - # Este comando debemos ver si lo tenemos disponible y nos servirá para subir archivos desde nuestra máquina atacante al servicio 21.
wget -m ftp://anonymous:anonymous@<ip> # Descargarmos todo el contenido del directório FTP.
```

---

## 💥 Explotación FTP con Metasploit Framework

Metasploit ofrece múltiples módulos para atacar servidores FTP vulnerables, especialmente aquellos con acceso anónimo habilitado o versiones con exploits conocidos.

```bash
use auxiliary/scanner/ftp/ftp_version # Enumeración FTP
set RHOSTS <ip_target>/24 # ip de la máquina víctima.
set THREADS 50 
exploit 
---
use auxiliary/scanner/ftp/ftp_login # Fuerza bruta FTP.
set RHOSTS <ip_target> # ip de la máquina víctima.
set USER_FILE /path/to/users.txt # Seleccionamos diccionario de usuarios.
set PASS_FILE /path/to/passwords.txt # Seleccionamos diccionario de contraseñas.
set THREADS 10 
exploit o run
```

---
