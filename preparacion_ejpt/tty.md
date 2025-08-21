---
layout: default
title: Preparación EJPTv2
---

# ⚙️ TTY - Spawning

¿Qué es un TTY?

En los sistemas Unix y Linux, TTY (Teletypewriter) es el nombre que se le da a las interfaces de terminal que permiten la interacción entre el usuario y el sistema. Originalmente hacía referencia a los antiguos teletipos físicos conectados a grandes computadoras, pero hoy en día el término se mantiene para designar las consolas virtuales y sesiones interactivas de shell.

Cuando un usuario inicia sesión en una máquina, el sistema “spawnea” (crea) un proceso asociado a un TTY para poder recibir comandos y mostrar respuestas. Esto ocurre tanto en consolas físicas como en terminales remotas (SSH, por ejemplo).

---

Para crearnos una pseudo-consola donde podamos hacer control c y no tengamos problemas con el teclado ejecutamos lo siguiente:

```bash
script /dev/null -c bash # Una vez tengamos acceso a la máquina escribimos esto.
control z # Lo dejamos en segundo plano.
stty raw -echo; fg 
xterm
export TERM=xterm
export SHELL=bash
```

## 🚀 Tratamiento de TTY – Explicación de los comandos

- script /dev/null -c bash

El comando script se usa normalmente para registrar una sesión de terminal.

Al redirigir la salida a /dev/null y ejecutar bash, en realidad forzamos la creación de una pseudo-terminal completamente interactiva.

Esto ayuda a escapar de shells limitadas.

- Ctrl + Z

Suspende el proceso actual (la shell que hemos generado) y lo manda al segundo plano.

Esto nos permite recuperar el control de nuestra terminal local para aplicar ajustes antes de reanudar la sesión.

- stty raw -echo; fg

stty raw -echo: modifica la configuración de la terminal local:

raw: habilita el modo “raw” (captura de teclas directamente, sin procesar).

-echo: evita que se duplique la entrada al escribir.

fg: trae de vuelta al primer plano el proceso que habíamos enviado con Ctrl+Z.

Resultado: la shell remota se comporta de manera mucho más natural y usable.

xterm

Le decimos a la shell que utilice xterm como tipo de terminal.

Esto habilita características como colores, atajos de teclado, mejor compatibilidad de pantalla y uso de editores interactivos.

- export TERM=xterm

Define la variable de entorno TERM, indicando que nuestra sesión trabaja como si fuera un emulador de terminal xterm.

Necesario para que programas interactivos (ej. nano, vim, top) funcionen correctamente.

- export SHELL=bash

Configura la variable SHELL para que el sistema use bash como shell predeterminada.

Asegura que todos los comandos posteriores funcionen con las características de bash en lugar de una shell limitada (como sh).



---

## A continuación vamos a ver varios métodos para lanzarnos una TTY

```bash
python -c 'import pty;pty.spawn("/bin/bash")' # Python TTY Shell.
python3 -c 'import pty;pty.spawn("/bin/bash")' # Python TTY Shell.
/bin/sh -i # Spawn Interactive sh shell.
perl -e 'exec "/bin/sh";' # **Spawn Perl TTY Shell.
ruby -e 'exec "/bin/sh"' # Spawn Ruby TTY Shell.
```


---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
