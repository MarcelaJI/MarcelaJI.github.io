---
layout: default
title: Proyectos 42 Madrid
---

# Enumeración

La enumeración es la fase donde se recopila información detallada sobre un sistema objetivo, después del reconocimiento inicial. 

Después de la fase de descubrimiento del host y escaneo de puertos de una prueba de penetración, la siguiente fase lógica implicará la enumeración de servicios.

El objetivo de la enumeración de servicios es recopilar información adicional y más completa. Información específica detallada sobre los hosts/sistemas en una red y los servicios que se ejecutan en dichos hosts.

Esto incluye información como nombres de cuentas, recursos compartivos, configuraciones incorrectas, servicios y demás.

Al igual que la fase de escaneo, la enumeración implica conexiones activas a los dispositivos remotos en la red.

hay muchos protocolos en sistemas en red que un atacante puede atacar si han sido mal configurados o se han dejado habilitados. 

## Metodología de pruebas de penetración

![metodologia](../assets/img/metologia_pruebas.png)

---

## Escaneo y enumeración de puertos con NMAP


Nmap es un escáner de red gratuito y de código abierto que se puede utilizar para descubrir hosts en una red, así como para escanear objetivos en busca de puertos abiertos.

También se puede utilizar para enumerar los servicios que se ejecutan en puertos abiertos, así como el sistema operativo que se ejecuta en el sistema destino.

---

### Enumeración FTP

TTP (File tranfer Protocol) es un protocolo que utiliza el puerto 21, y se utiliza para facilitar el intercambio de archivos entre un servidor y un cliente/clientes.

También se utiliza frecuentemente como medio para tranferir archivos hacia y desde el directorio de un servidor web.

Podemos utilizar múltiples módulos auxiliares para enumerar información así como realizar ataques de fuerza bruta contra objetivos que ejecutan un servidor FTP.

La autenticación FTP utiliza una combinación de nombre de usuario y contraseña, sin embargo, en algunos casos se puede iniciar sesión de forma anónima en un servidor FTP configurado incorrectamente.

---

### Enumeración de SMB

SMB (Server Message Block) es un protocolo de intercambio de archivos de red que se utiliza para faciltar el intercambio de archivos y periféricos entre computadoras en una red local (LAN).

SMB usa el puerto 445 (TCP). Sin embargo, originalmente, SMB se ejecutaba sobre NetBIOS usando el puerto 139.

SAMBA es la implemnetación de SMB para Linux que los sistemas Windows accedan a recursos compartidos y dispositivos de Linux.

---

### Enumeración de servicios web

Un servidor web es un software que se utiliza para servir datos de sitios web en la web.

Los servidores web utilizan HTTP(Protocolo de tranferencia de hipertexto) para facilitar la comunicación entre los clientes y el servidor web.

HTTP es un protocolo de capa de aplicación que utiliza el puerto TCP 80 para la comunicación.

Ejemplos de servicios web populares: Apache, Nginxn y Microsoft IIS.

---


### Enumeración de MYSQL

MYSQL e sun sistema de gestión de bases de datos relacionales de código abierto basado en SQL(Lenguaje de consulta estructurado).

Se utiliza generalmente para almacenar registros, datos de clientes y también para almacenar datos de aplicaciones web.

MYSQL utiliza el puerto 3306 de forma predeterminada, sin embargo, como cualquier servicio, puede ser alojado en cualquier puerto abierto.

---

### Enumeración SSH

SSH (Secure Shell) es ¡un protocolo de administración remota que ofrece cifrado y es el sucesor de telnet.

Normalmente se utiliza para acceso remoto a servidores y sistemas.

SSH usa el puerto 22 por defecto, sin embargo, al igual que otros servicios, puede ser configurado para utilizar cualquier otro puerto abierto.

---

### Enumeración SMTP

SMTP (Simple Mail Transfer Protocol) es un protocolo de comunicación que se utiliza para la transmisión de correo electrónico.

SMTP usa el puerto 25 por defecto. También se puede configurar para ejecutarse en el puerto TCP 465 y 587.

Podemos utilizar los módulos auxiliares para enumerar la versión de SMTP así como las cuentas del usuario en el sistema de destino.









<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
