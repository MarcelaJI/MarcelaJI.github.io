---
layout: default
title: Apuntes
---

## Alternativas para la enumeración de puertos usando descriptores de archivo

Existen alternativas para realizar la enumeración de puertos de manera efectiva sin utilizar herramientas externas.

Crearemos un script en bash para que se encargue para una IP que le pasemos que puertos están abiertos

Lo llamaremos *portScan.sh*

Le damos primero permisos con chmod tal que así:

```bash
chmod +x portScan.sh
```

Lo haremos tal que así:


```bash
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo...."
	tput cnorm; exit 1
}

# Ctrl+C
trap ctrl_c SIGINT

declare -a ports=( $(seq 1 65535) )

function checkPort(){
	(exec 3<> /dev/tcp/$1/$2) 2>/dev/null
	
	if [ $? -eq 0 ]; then
		echo "[+] Host $1 - Port $2 (OPEN)"
	fi
	exec 3<&-
	exec 3>-
}; 

tput civis # Ocultar el cursor

if [ $1 ]; then
	for port in $(ports[0]); do
		checkPorts $1 $port &
	done
else
	echo -e "\n[!] Uso: $0 <ip-address>\n"
fi

wait

tput cnorm

```
