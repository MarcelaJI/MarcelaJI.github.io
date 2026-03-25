---
layout: default
title: So_Long
---

# 🛠️ pipex

> Proyecto realizado como parte del cursus de **42 Madrid**  
> ✅ Puntuación obtenida: **100/100**

---

## 📜 Descripción

**pipex** es un proyecto cuyo objetivo principal es reproducir el comportamiento de los *pipes* (`|`) de bash, redireccionando correctamente la entrada y salida estándar entre múltiples comandos.

Este proyecto fue diseñado para afianzar conocimientos sobre:

- Procesos y *forks*
- Redirección de archivos
- *Pipes* y comunicación entre procesos
- Manejo de errores
- Parsing de argumentos
- Acceso y búsqueda en el `PATH`

---

## 📂 Estructura del proyecto

- `pipex.c`: Lógica principal del programa, manejo de procesos e hilos.
- `processes.c`: Implementación de los hijos que ejecutan los comandos.
- `path.c` & `path_utils.c`: Localización del binario de un comando en el PATH.
- `parsing.c` & `parsing_utils.c`: Parsing de los comandos pasados por argumentos.
- `utils.c`: Funciones auxiliares, gestión de errores y liberación de memoria.
- `Makefile`: Compilación automatizada.
- `Libft`: Biblioteca auxiliar obligatoria del cursus 42.

---

## 🧪 Ejemplo de uso

Este es el repositorio del proyecto para descargarlo:

[Pipex](https://github.com/MarcelaJI/pipex)

```bash
./pipex infile "cmd1" "cmd2" outfile
```

🔁 Equivalente en bash:
```bash
< infile cmd1 | cmd2 > outfile
```

### 📌 Ejemplo práctico

```bash
./pipex archivo_entrada.txt "grep hola" "wc -l" resultado.txt
```

Lo que hará será tomar el contenido de `archivo_entrada.txt`, filtrarlo con `grep hola`, contar las líneas con `wc -l` y guardar el resultado en `resultado.txt`.

---

## ⚙️ Compilación

Para compilar el proyecto, simplemente ejecuta:

```bash
make
```

Esto generará el ejecutable `pipex`.

Para limpiar los archivos `.o`:

```bash
make clean
```

Para eliminar los archivos `.o` y el ejecutable:

```bash
make fclean
```

Para recompilar desde cero:

```bash
make re
```

---

## ✅ Reglas

El programa solo acepta exactamente **4 argumentos** además del nombre del ejecutable:

```bash
./pipex infile "cmd1" "cmd2" outfile
```

De lo contrario, mostrará un mensaje de error de formato.

---

## 🧠 Aprendizajes clave

- Cómo usar `pipe()`, `fork()`, `dup2()`, `execve()`
- Gestión de errores y señales
- Parsing manual sin bibliotecas externas
- Creación de una estructura robusta y escalable

---

## 📚 Requisitos del proyecto

Este proyecto fue desarrollado y evaluado bajo las siguientes restricciones:

- ✅ No uso de funciones prohibidas del sistema
- ✅ Solo uso de bibliotecas estándar de C
- ✅ Integración de **Libft**
- ✅ Limpieza de memoria garantizada (sin leaks)
- ✅ Gestión de errores sólida

---


## 🧑‍💻 Autora

**Nombre:** [Marcela Jimenez]  
**Login:** [ingjimen]  
**Contacto:** [ingjimen@student.42madrid.com]

---