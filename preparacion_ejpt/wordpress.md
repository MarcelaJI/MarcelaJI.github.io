---
layout: default
title: Preparación EJPTv2
---

# Wordpress

WordPress es un sistema de gestión de contenido (CMS) de código abierto, gratuito y muy popular que permite crear y gestionar sitios web. Se utiliza principalmente para construir blogs, sitios web corporativos, tiendas en línea, y mucho más. Su facilidad de uso y la gran cantidad de temas y plugins disponibles lo convierten en una herramienta versátil y accesible para usuarios con diferentes niveles de experiencia.

---

## 🕵️Identificación de la versión de WordPress y sus componentes

```bash
nmap -sV --script http-wordpress-enum <url> # Detección de la versión de WordPress y plugins.
nmap -sV --script "http-wordpress* and not http-wordpress-brute" <url> # Escaneo de vulnerabilidades en WordPress.
nmap -sV --script http-wordpress-users <url> # Enumeración de usuarios de WordPress.
nmap --script=http-wordpress-enum --script-args http-wordpress-enum.root=/ -p 80,443 <URL> # Escaneo completo para confirmar el uso de WordPress.
nmap --script=http-vuln* -p 80,443 <url> # Detección de vulnerabilidades específicas en WordPress y sus plugins.
```

También podemos intentar enumerar plugins con la herramienta curl:

```bash
curl -s -X GET "http://192.168.100.50" | grep -oP 'plugins/\K.*' | sort -u
```

## Checklist de WordPress ✔️

Para comprobar si existe un panel de inicio de sesión:


- url/wp-admin/login.php
- url/wp-admin/wp-login.php
- url/wp-login.php

Otros directorios clave a revisar en cualquier sitio web:


- url/robots.txt
- url/sitemap.xml
- url/CHANGELOG.txt


Cuando hayamos logrado la intrusión: 

```bash
cat wp-config.php | grep 'DB_USER\|DB_PASSWORD'
```

 Si al acceder al servicio web notamos que no carga correctamente, es posible que se esté utilizando Virtual Hosting. En este caso, deberemos añadir el dominio al que apunta realmente en nuestro archivo /etc/hosts. Para ello, agregamos la IP de la web junto con el dominio correspondiente, por ejemplo: 10.0.0.10 wordpress.htb.

---

## 🛠️ Escaneo básico de WordPress con Metasploit

```bash
use auxiliary/scanner/http/wordpress_version # Cargar el módulo.
set RHOSTS <url>
set RPORT 80
set TARGETURI /
run
```

## 🕵️ Enumeración de usuarios en WordPress

```bash
use auxiliary/scanner/http/wordpress_users_enum
set RHOSTS <url>
set RPORT 80
set TARGETURI /
run
```

## 🔑 Ataque de fuerza bruta con Metasploit

```bash
search auxiliary/scanner/http/wordpress_login_enum
```


```bash
set RHOSTS <url>
set USERNAME <nombre_usuario> # Nombre de usuario objetivo.
set PASS_FILE /usr/share/wordlists/rockyou.txt # Diccionario de contraseñas.
exploit
```

## 🛠️ Otras herramientas para auditar WordPress

### WPScan

WPScan es una herramienta especializada en la enumeración y auditoría de sitios basados en WordPress. Permite detectar vulnerabilidades, usuarios, plugins y temas instalados.

Ejemplo de uso:

```bash
wpscan --url <url_wordpress> # Análisis básico de WordPress.
wpscan --url <url_wordpress> -e vp,u # Enumeración de plugins vulnerables y usuarios.
wpscan --url <url_wordpress> -e t # Enumeración de temas instalados.
```

💡 Una buena práctica durante la auditoría de WordPress es revisar el código fuente de la página. Allí podemos encontrar rutas como /uploads, analizar si hay directory listing, identificar temas, plugins y posibles filtraciones de información (information leakage), vhosts, entre otros.

💡 También es recomendable examinar publicaciones de blogs u otras secciones del sitio web en busca de nombres de usuario que puedan ser utilizados en ataques de fuerza bruta.

Si encontramos nombres de usuario potenciales, debemos almacenarlos en un archivo .txt para su posterior análisis o uso como wordlist.

## 🔑 Fuerza bruta en el panel de inicio de sesión de WordPress

```bash
wpscan --url http://127.0.0.1:8080/ -U <user> -P /usr/share/wordlists/rockyou.txt # Uso de diccionario de contraseñas.
wpscan --url http://127.0.0.1:8080/ --passwords <ruta_diccionario.txt> --usernames <ruta_usuarios.txt> # Ataque con múltiples usuarios.
```

Ataque de fuerza bruta con Hydra

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt 127.0.0.1 -s 8080 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In:F=incorrect"
```


Ataque a múltiples usuarios:

```bash
hydra -L <lista_usuarios.txt> -P <diccionario.txt> <url> -s 8080 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In:F=incorrect"
```

---


<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
