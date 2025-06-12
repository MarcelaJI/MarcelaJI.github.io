---
layout: default
title: Apuntes
---

# Local File Inclusion (LFI)

Local File Inclusion (LFI) es una vulnerabilidad de seguridad que ocurre cuando una aplicación web permite que el usuario incluya archivos del servidor local en la ejecución de la aplicación sin validación adecuada. Esto puede permitir a un atacante leer archivos sensibles, como contraseñas, configuraciones, o incluso ejecutar código malicioso si hay condiciones favorables.

## ¿Cómo ocurre?

Sucede cuando una aplicación usa datos proporcionados por el usuario para construir rutas de archivos sin sanitización. Por ejemplo, en PHP:

```php
<?php
  include($_GET["page"]);
?>
```

Si se accede a:
http://victima.com/index.php?page=about.php
Se cargará el archivo about.php.

Pero un atacante podría modificar la URL a:
http://victima.com/index.php?page=../../../../etc/passwd
Y acceder a archivos como /etc/passwd (en sistemas Unix).

- Ejemplo práctico:

Supongamos que tenemos esta URL vulnerable:

```bash
http://victima.com/index.php?page=home
```

Un atacante podría intentar:

```bash
http://victima.com/index.php?page=../../../../etc/passwd
```

Y obtener una salida como:

```bash
root:x:0:0:root:/root:/bin/bash
...
```
Esto revela que el atacante ha logrado leer archivos del sistema.


---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>

































































