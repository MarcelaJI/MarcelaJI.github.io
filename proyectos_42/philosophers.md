---
layout: default
title: So_Long
---

# 🍝 Philosophers

Este proyecto es una simulación del famoso problema de los filósofos comensales. Cada filósofo piensa, come y duerme, y compite por recursos limitados (tenedores) sin generar condiciones de carrera ni interbloqueos.

## 📦 Contenido del Proyecto

├── includes/ # Archivos .h con estructuras y prototipos

├── src/ # Archivos fuente .c

├── Makefile # Script de compilación


---

## 🚀 Instalación y Uso

Este es el repositorio del proyecto para descargarlo:

[Philosophers](https://github.com/MarcelaJI/philosophers)

### 🔧 Compilar

Usa el `Makefile`:

```bash
make
```
Esto generará un ejecutable llamado **philo**.

🧪 Ejecución
El programa acepta los siguientes argumentos:

```bash
./philo number_of_philosophers time_to_die time_to_eat time_to_sleep[number_of_times_each_philosopher_must_eat]
```

Ejemplo:
```bash 
./philo 5 800 200 200
```
Opcionalmente:

```bash
./philo 5 800 200 200 7
```

Esto ejecuta la simulación con 5 filósofos, cada uno con 800ms antes de morir si no come, 200ms para comer, 200ms para dormir, y finaliza cuando todos han comido 7 veces.

🧠 Descripción General
Cada filósofo:

🥢 Toma los tenedores

🍽️ Come durante un tiempo definido

😴 Duerme

🤔 Piensa

🔁 Repite mientras esté vivo

Además:

Si un filósofo no come en time_to_die, muere ☠️

Cuando todos comen number_of_times_each_philosopher_must_eat, el programa termina correctamente ✅

🧵 Programación Concurrente

Este proyecto hace uso de:

- pthread_mutex_t para gestionar acceso a los tenedores

- Un hilo por filósofo

- Un hilo monitor que detecta muertes o finalización

- Colores e iconos se usan en la salida para hacer más visual la simulación.

💻 Cómo Clonarlo

```bash
git clone https://github.com/MarcelaJI/philosophers.git
cd philosophers
cd philo
make
```
---

✨ Extra

Este proyecto incluye:

🧠 Lógica modular

🎨 Salida coloreada y emojis para mayor claridad

🧼 Limpieza automática de recursos

---


👩💻Autora 
login 42:
[ingjimen]

📧 ingjimen@student.42madrid.com

📜 Licencia

Este proyecto es parte del currículo académico de 42 Madrid y se rige por sus normas de propiedad intelectual.

---