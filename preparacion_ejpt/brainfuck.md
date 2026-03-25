---
layout: default
title: Preparación EJPTv2
---


## Brainfuck

Brainfuck es un lenguaje de programación esotérico creado en 1993 por Urban Müller.

## Características principales

- Está diseñado para ser muy difícil de leer y escribir, de ahí el nombre (“te rompe el cerebro”).

- Opera sobre una especie de cinta de memoria (como una máquina de Turing):

    1. Una fila de celdas (inicialmente todas a 0).

    2. Un puntero que se mueve a izquierda o derecha.

- Cada instrucción es un solo carácter:

    -   '>' → mueve el puntero a la derecha

    - '<' → mueve el puntero a la izquierda

    - '+' → incrementa el valor en la celda

    - '-' → decrementa el valor en la celda

    - '.' → imprime el carácter de la celda actual

    - ',' → lee un carácter desde la entrada y lo guarda en la celda

    - '[' → si la celda es 0, salta al ] correspondiente

    - ']' → si la celda no es 0, salta de vuelta al [ correspondiente

## Ejemplo: 

````bash
++++++++++[>+++++++>++++++++++>+++>+<<<<-]>
++.>+.+++++++..+++.>++.<<+++++++++++++.>.+++.------.--------.>+.>.
````

👆 Eso imprime Hello World! en pantalla.


## ¿Para qué sirve?

🔹No está hecho para proyectos reales.

🔹Es más como un reto mental / diversión entre programadores.

🔹Se usa en competiciones de code golfing (resolver problemas con el menor número de caracteres).

🔹También lo ves en CTFs o labs como easter egg.

---
