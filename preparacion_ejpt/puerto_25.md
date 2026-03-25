---
layout: default
title: Preparación EJPTv2
---

## 🔍 Puerto 25 - SMTP

El puerto 25 es el puerto predeterminado utilizado por el protocolo SMTP (Simple Mail Tranfer Protocol) para el envío de correo electrónico entre servidores. Es decir, se utiliza para la comunicación de correo electrónico entre diferentes servidores de correo.

---

## Reconocimiento del puerto 25 con Nmap 🔍

Para analizar el puerto 25 y sus servidores asociados con Nmap, podemos listar todos los scripts disponibles para SMTP con el siguiente comando:

```bash
ls -la /usr/share/nmap/scripts | grep -e "smtp" # Ver scripts de Nmap para el servicio SMTP
```

Comandos útiles para Nmap para SMTP:

```bash
nmap -p25 -sVC <ip_victima> # Escaneo con detección de versiones y scripts comunes
nmap -p25 --script smtp-* <ip_victima> # Ejecutar todos los scripts SMTP
nmap -p25 <ip_victima> --script smtp-commands # Enumera comandos SMTP disponibles
nmap -p25 <ip_victima> --script smtp-enum-users # Intenta enumerar usuarios válidos
nmap -p25 <ip_victima> --script smtp-vuln-* # Busca vulnerabilidades conocidas
nmap -p25 <ip_victima> --script smtp-open-relay # Prueba si el servidor es un relay abierto
```

---

##  Principales flags de smtp-user-enum


| **Flag** | **Descripción** 
| --------  | ------------- |
| -M        |  Modo (VRFY, EXPN, RCPT)
| -U         | Lista de usuarios a probar
| -u         | Usuario único
| -t         | Host objetivo
| -T         | Lista de hosts objetivo
| -p         | Puerto (por defecto 25)
| -d         | Modo debug

---

## 📌 Ejemplo de uso con diccionario de usuarios:

```bash
smtp-user-enum -M VRFY -U <diccionario.txt> -t <ip_victima>
```

## 📌 Enumeración Manual

Conexión básica al servidor SMTP:

```bash
telnet <ip_victima> 25 # Conexión manual al servidor SMTP
nc -vn <ip_victima> 25 # Uso de Netcat para verificar conexión
```

## 📌 Usos:

- Verificar si el puerto 25 está abierto.
- Probar comandos SMTP manualmente (EHLO, MAIL FROM, RCPT TO...).
- Identificar la versión del servidor SMTP.

---

## 🛠️ Usando Metasploit para SMTP

### 📌 Escaneo de versión SMTP

```bash
msfconsole -q # Iniciar Metasploit en modo silencioso
use auxiliary/scanner/smtp/smtp_version
set RHOSTS <ip_victima>
exploit
```

### 📌 Enumeración de usuarios SMTP

```bash
use auxiliary/scanner/smtp/smtp_enum
set RHOSTS <ip_victima>
set USER_FILE /usr/share/wordlists/metasploit/unix_users.txt # Diccionario recomendado
exploit
```

### 📌 Comandos SMTP útiles para pruebas

```bash
HELO example.com
EHLO example.com
VRFY usuario
EXPN usuario
RCPT TO: <usuario@dominio>
MAIL FROM: <remitente@dominio>
```

### 📌 Verificación de Relay Abierto

Para comprobar si un servidor SMTP permite el reenvío de correos sin autenticación (open relay), se pueden ejecutar los siguientes comandos:

```bash
telnet <ip_victima> 25
HELO test
MAIL FROM: <attacker@example.com>
RCPT TO: <victim@example.com>
DATA
Subject: Test
Test message
.
QUIT
```

Si el servidor acepta y entrega el correo sin restricciones, significa que está configurado como relay abierto, lo cual es una grave vulnerabilidad de seguridad.

---
