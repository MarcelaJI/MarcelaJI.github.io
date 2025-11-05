---
layout: default
title: Preparación EJPTv2
---

# Nikto 🛠️

Nikto es una herramienta de código abierto para escanear servidores web y detectar vulnerabilidades. Funciona buscando archivos peligrosos, versiones obsoletas del software del servidor web y configuraciones inseguras. 


## Características Clave de Nikto 🔍

| Opción | Descripción |
| ------ | ----------- |
|Target Host | URL o IP del servidor a analizar.|
| Port | Puerto en el que escucha el servidor (por defecto, 80 o 443). |
| SSL/TLS | Habilita el escaneo sobre HTTPS. | 
| User-Agent | Personaliza la cabecera del agente de usuario. |
| Output | Guarda los resultados en un archivo. | 
| Timeout | Define un límite de tiempo para cada solicitud. | 
| Throttling | Controla la velocidad de las peticiones para evitar ser bloqueado. |

---

## 📚 Diccionarios y Firmas Utilizadas

Nikto utiliza una base de datos con miles de pruebas para detectar vulnerabilidades comunes. Algunas de las firmas que emplea incluyen:

- Detectar versiones de software desactualizadas (Apache, Nginx, IIS, etc.).

- Identificar archivos de configuración expuestos (robots.txt, .htaccess, phpinfo.php).

- Analizar cabeceras HTTP en busca de configuraciones inseguras.

---

## Ejemplo de uso

```bash
nikto -h <url> # Escaneo simple con Nikto.
nikto -h <url> -p 443 # Si el servidor usa un puerto diferente al 80 o queremos analizar HTTPS:
nikto -h <url> -useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" # Evitar la Detección Modificando el User-Agent
nikto -h <url> -tuning -<número> # Excluir Ciertos Tipos de Pruebas, (-2=evita pruebas de archivos peligrosos.) (-4=evita pruebas de inyección SQL.) (-6=evita pruebas de XSS.)
nikto -h <url> -delay 2 # Controlar la Velocidad del Escaneo
```

---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>