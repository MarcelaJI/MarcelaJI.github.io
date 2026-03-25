---
layout: default
title: Apuntes
---

# Permisos SUID

## Qué es SUID?

SUID = Set User ID → Es un permiso especial que se puede poner a un archivo ejecutable.

Cuando un ejecutable tiene el bit SUID activado, se ejecuta con los privilegios del dueño del archivo, no con los del usuario que lo lanza.

Lo más común: si un binario pertenece a root y tiene SUID, entonces aunque lo ejecute un usuario normal, se ejecuta como root.

- Cómo se ve un archivo SUID:

```bash
ls -la /bin/ping
```

```bash
-rwsr-xr-x 1 root root ... /bin/ping
```

la **s** en lugar de la **x** en el primer grupo de permisos: **rws**, esto indica que el archivo tiene el bit SUID activo.

Para listar todos los SUID del sistema ejecutamos:

```bash
find / -user root -perm -4000 -exec ls -la {} \; 2>/dev/null
```

Esto nos muestra todos los binarios que tienen el bit SUID y que pertenecen a **root**.

## ¿Por qué es peligroso?

Muchos binarios tienen SUID por necesidad (por ejemplo passwd, ping, etc.).
Si un admin pone SUID a un binario que no es seguro (por ejemplo, un editor de texto, python, perl, tar, bash, etc.), entonces un usuario normal puede ejecutar ese binario como root → escalada de privilegios.

Ejemplo de explotación de SUID:

Supongamos que encontramos:

```bash
-rwsr-xr-x 1 root root ... /usr/bin/python
```

Esto es muy grave -> porque podemos hacer:

```bash
/usr/bin/python -c 'import os; os.system("/bin/bash")'
```

Y así obtendríamos un bash con permisos de root -> root shell.

---

🔸 ¿Cómo sé si puedo escalar con un SUID?

- ¿El binario permite ejecutar comandos del sistema?
- ¿El binario permite escribir o leer archivos como root?
- ¿El binario permite escapar a una shell interactiva?

- Binarios peligrosos si están SUID.


Si alguno de estos binarios tiene SUID, casi siempre puedes escalar:

/bin/bash → ejecutas bash como root.

/usr/bin/python o python3

/usr/bin/perl

/usr/bin/vim, vi, nano → puedes escribir/leer como root.

/usr/bin/find → puede ejecutar comandos.

/usr/bin/awk

/usr/bin/less, /usr/bin/more

/usr/bin/tar, /usr/bin/zip, /usr/bin/rsync

Estos binarios son "escalables" si los vemos con SUID.

- Recursos útiles:


👉 Hay una web que te dice cómo escalar con cada binario:

[gtfobins](https://gtfobins.github.io)

En GTFObins buscas python, vim, tar, etc., y te dice: si tienes SUID en este binario, haz este comando para obtener root.

---