---
layout: default
title: Apuntes
---

## Enumeración de subdominios

La enumeración de subdominios es una de las fases cruciales en la seguridad informática para identificar los subdominios asociados a un dominio principal. Los subdominios son parte de un dominio más grande y a menudo están configurados para apuntar a diferentes recursos de la red, como servidores web, servidores de correo electrónico, sistemas de bases de datos, sistemas de gestión de contenido, entre otros. Al identificar subdominios vinculados a un dominio principal, un atacante podría obtener valiosa para cada uno de estos, lo que le podría llevar a encontrar vectores de ataque potenciales.
### Herramientas que nos ayudan a enumerar subdominios:

- **Phonebook** (Herramienta pasiva): [https://phonebook.cz/](https://phonebook.cz/)

- **Intelx** (Herramienta pasiva): [https://intelx.io/](https://intelx.io/)


- **CTFR** (Herramienta pasiva): [https://github.com/UnaPibaGeek/ctfr](https://github.com/UnaPibaGeek/ctfr)

Se ejecuta tal que así :

```bash
python3 ctfr.py -d tinder.com
```

- **Gobuster** (Herramienta activa): 
 [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)

Se ejecuta tal que así:

```bash
gobuster vhost -u https://.tinder.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 20 | grep -v "403"
```



- **Wfuzz** (Herramienta activa): [https://github.com/xmendez/wfuzz](https://github.com/xmendez/wfuzz)

Se ejecuta tal que así:

```bash
wfuzz --hc=403 -c -t 20 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.tinder.com" http://tinder.com
```

- **Sublist3r** (Herramienta pasiva): [https://github.com/huntergregal/Sublist3r](https://github.com/huntergregal/Sublist3r)

Se utiliza tal que así:

```bash
python3 sublist3r.py -d tinder.com
```

