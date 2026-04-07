---
layout: default
title: Apuntes
---

## Fuzzing y enumeración de archivos en un servidor web

Esta técnica se utiliza para descubrir rutas y recursos ocultos en un servidor web mediante ataques de fuerza bruta.

Una de las herramientas que utilizaremos es gobuster que se ejecuta tal que así:

```bash
./gobuster dir -u https://miwifi.com/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 50 -x php,html,txt -s 200 -b ''
```

- `dir` → Modo de búsqueda de directorios.
- `-u` → URL objetivo.
- `-w` → Diccionario de rutas/archivos.
- `-t 50` → 50 hilos (más velocidad).
- `-x php,html,txt` → Extensiones a probar.
- `-s 200` → Mostrar solo respuestas HTTP 200.
- `-b ''` → No excluir ningún código (lista vacía de códigos a ignorar).

---

La siguiente herramienta es *wfuzz* y se ejecuta tal que así:

```bash
wfuzz -c --sl=216 --hc=404,403 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ/
```

- `-c` → Salida con colores.
- `--sl=216` → Filtra por **tamaño de respuesta en líneas** (_size lines_).
- `--hc=404,403` → Ocultar respuestas con esos códigos.
- `-t 200` → 200 hilos (más rápido).
- `-w` → Diccionario de palabras.
- `FUZZ` → Punto donde se inyectan las palabras del diccionario.

```bash
wfuzz -c --hc=404,403 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt https://miwifi.com/FUZZ.html
```

- `-c` → Salida en color.
- `--hc=404,403` → Oculta respuestas con códigos 404 y 403.
- `-t 200` → 200 hilos (más rapidez).
- `-w` → Diccionario de palabras.
- `FUZZ.html` → Inserta cada palabra del diccionario **antes de `.html`**.

Ejemplo:  
Si el diccionario tiene `admin` → prueba:  
`https://miwifi.com/admin.html`

Diferencia clave: aquí estamos buscando **archivos `.html` concretos**, no directorios.

```bash
wfuzz -c --hc=404,403 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -z list,html-txt-php https://miwifi.com/FUZZ.FUZ2Z
```

- `-c` → Salida en color.
- `--hc=404,403` → Oculta respuestas 404 y 403.
- `-t 200` → 200 hilos.
- `-w` → Diccionario principal (para `FUZZ`).
- `-z list,html-txt-php` → Segunda lista manual (para `FUZ2Z`) con valores: `html`, `txt`, `php`.
- `FUZZ.FUZ2Z` → Dos posiciones de fuzzing:
    - `FUZZ` → palabras del diccionario
    - `FUZ2Z` → extensiones (`html`, `txt`, `php`)

Ejemplo generado:  
`admin.php`, `login.html`, `test.txt`

 En resumen: prueba **nombres + múltiples extensiones a la vez**.

```bash
wfuzz -c --hw=6515 -t 200 -z range,1-20000 'https://miwifi.com/shop/buy/detail?product_id=FUZZ'
```

- `-c` → Salida en color.
- `--hw=6515` → Filtra por **número de palabras** (_hide words_). -> Oculta respuestas que tienen exactamente **6515 palabras**.

Uso típico: eliminar respuestas repetidas (por ejemplo, páginas de error con el mismo tamaño en palabras).
- `-t 200` → 200 hilos (rápido).
- `-z range,1-20000` → Genera números del 1 al 20000.
- `FUZZ` → Punto donde se insertan esos números.
- `product_id=FUZZ` → Va probando distintos IDs.

Ejemplo:  
`product_id=1`, `product_id=2`, `product_id=3`…

En resumen: prueba muchos IDs para encontrar productos válidos u ocultos.

---

La siguiente herramienta es *FFUF*

Se ejecuta tal que así:

```bash
./ffuf -c -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u https://miwifi.com/FUZZ/ --mc=200
```

- `-c` → Salida en color.
- `-w` → Diccionario de palabras.
- `-u` → URL objetivo con `FUZZ` como punto de inyección.
- `FUZZ/` → Prueba directorios (ej: `/admin/`, `/login/`).
- `--mc=200` → Muestra solo respuestas HTTP 200.

---

Otra herramienta es *Phonebook.cz* para hacer esta enumeración a través de la web.

[Phonebook](https://phonebook.cz/)