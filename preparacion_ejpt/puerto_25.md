---
layout: default
title: Preparación EJPTv2
---

# 🔍 Puerto 25 - SMTP

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

