---
layout: default
title: So_Long
---

# 🧠 push_swap

`push_swap` es un proyecto del currículo de 42 que consiste en ordenar una lista de números enteros utilizando un conjunto restringido de operaciones y la menor cantidad posible de movimientos. El algoritmo implementado debe ser lo más eficiente posible, especialmente para conjuntos de datos grandes.

---

## 📌 Objetivo del Proyecto

El objetivo es implementar un algoritmo de ordenación utilizando **dos pilas (stack A y stack B)**, una lista doblemente enlazada, y un conjunto de instrucciones específicas:

- `sa`, `sb`, `ss` — intercambiar el primer y segundo elemento de una pila.
- `pa`, `pb` — mover el elemento superior de una pila a otra.
- `ra`, `rb`, `rr` — rotar la pila hacia arriba.
- `rra`, `rrb`, `rrr` — rotar la pila hacia abajo.

---

## 🔧 Compilación

Este es el repositorio del proyecto para descargarlo:

[push_swap](https://github.com/MarcelaJI/push_swap)

Clona este repositorio y compílalo con `make`:

```bash
git clone https://github.com/MarcelaJI/push_swap.git
cd push_swap
make
```

Esto generará el ejecutable:

```bash
./push_swap
```


▶️ Ejecución


Puedes ejecutar el programa pasando una lista de números como argumentos:

```bash
./push_swap 3 2 1
```

Esto imprimirá la secuencia de operaciones necesarias para ordenar esa lista.

✔️ Comprobación con checker


Puedes usar el checker oficial (checker_linux o checker_Mac) para verificar que tu salida es correcta:

```bash
ARG="4 2 3 1"; ./push_swap $ARG | ./checker_linux $ARG
```

Resultado esperado: OK

🔍 Ejemplos de prueba

```bash
ARG=$(seq 1 100 | sort -R | tr '\n' ' ')
./push_swap $ARG | ./checker_linux $ARG
```


🧹 Limpieza

Para eliminar los archivos compilados, ejecuta:

```bash
make fclean
```


🧪 Tests de memory leaks (Valgrind)


```bash
valgrind --leak-check=full --show-leak-kinds=all ./push_swap 3 2 1
```


🧮 Estructura general del algoritmo

El programa convierte los argumentos en una pila A (doblemente enlazada).

Si la pila ya está ordenada, termina.

Si no, se aplica un algoritmo de ordenación personalizado:

Si hay 3 o menos elementos: ordenación específica.

Si hay más: se empujan los elementos menos relevantes a la pila B, y se reintegran en orden.

Se buscan nodos objetivo y se calculan costes de operaciones.

Finalmente, se rota la pila A para dejar el menor valor en el top.

---

👩💻 Autora:
Marcela Jimenez

Login 42: ingjimen

GitHub: @MarcelaJI 

¡Gracias por visitar mi proyecto! ⭐

---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>