---
layout: default
title: Proyectos 42 Madrid
---

# Recopilación de información

La recopilación de información es el primer paso de cualquier prueba de penetración e implica reunir y recolectar información sobre un individuo, empresa, sitio web o sistema al que se dirige.

Cuanto más información tengamos sobre nuestro objetivo, más éxito tendremos durante las últimas etapas de una prueba de penetración.

La recopilación de información normalmente se divide en dos tipos:

- Recopilación pasiva de información: Implica recopilar tanta información como sea posible, sin interactuar activamente con el objetivo.
- Recopilación activa de información: Implica recopilar la mayor cantidad de información posible interactuando activamente con el sistema objetivo. (Se requiere autorización para realizar la recopilación activa de información).

¿Qué información estamos buscando?

- Recopilación pasiva de información:
	Identificación de direcciones IP e información DNS.
	1. Identificar nombres de dominio e información de propiedad del dominio.
	2.  Identificar direcciones de correo electrónico y perfiles de redes sociales.
	3. Identificar tecnologías web que se utilizan en los sitios de destino.
	4. Identificación de subdominios.
	
- Recopilación activa de información
   Descubrimiento de puertos abiertos en sistema de destino.
   
     1. Aprender sobre la infraestructura interna de la red/organización objetivo.
     2. Enumerar información de los sistemas de destino.

## Reconocimiento y huella del sitio web

Algunas herramientas para la **recopilación de información (footprinting)** pasivas:

- La enumeración con **whois**, es una técnica muy usada en la fase de **recopilación de información (footprinting)**. Permite obtener información pública registrada sobre un dominio, como:

	-  Nombre del propietario (empresa o persona)
	-  Servidores DNS
	-  Fechas de creación y expiración del dominio
	-  Correo del registrante
	-  Servidor web o proveedor de hosting
	-  Dirección IP asignada

Ejemplo de uso:

```bash
whois ejemplo.com
```

---

- [**Netcraft**](https://www.netcraft.com/) es una herramienta web que proporciona **información técnica detallada** sobre sitios web. Te permite saber cosas como:

	-  **Sistema operativo** del servidor web
	-  Proveedor de hosting
	-  Certificados SSL
	-  **Tecnología de backend** (Apache, Nginx, etc.)
	-  Subdominios
	-  Sitios alojados en la misma IP
	-  **Historial de tecnologías** usadas

🧭 ¿Para qué sirve hacer "huella" con Netcraft?

La **huella de un sitio web** es recopilar toda la información **visible y técnica** posible **antes de atacar**, para entender mejor su infraestructura.

Ejemplo:  
Si sabes que un servidor usa **Apache 2.4.29 en Ubuntu 18.04**, ya puedes buscar **vulnerabilidades conocidas (CVEs)** para esa versión.

---

- **whatweb**, detecta tecnologías web

Ejemplo de uso:

```bash
whatweb ejemplo.com
```

---

- Curl -I, para ver cabeceras HTTP(servidor, cookies, etc.)

Ejemplo de uso: 

``` 
Curl -I http://ejemplo.com
```

---

## Reconocimiento DNS

Es el proceso de **investigar el sistema de nombres de dominio** de un objetivo para obtener:

-  Direcciones IP asociadas
-  Subdominios
-  Registros de correo (MX)
-  Servidores de nombres (NS)
-  Posibles rutas ocultas
-  Enumeración de servicios

---

Algunas de las herramientas para el reconocimiento DNS son:

-  Detección de WAF con **waf00f**

### 📌 ¿Qué es un WAF?

- **WAF (Web Application Firewall)** = Cortafuegos web que **protege aplicaciones** de ataques como:

-  SQL Injection
-  Cross-Site Scripting (XSS)
-  Path Traversal
-  LFI/RFI
-  User-Agent falsos

🛡️ Filtra, bloquea o responde con errores cuando detecta peticiones sospechosas.

Qué hace `wafw00f`?

Es una herramienta que detecta **si un sitio web tiene un WAF**, y **cuál es** (Cloudflare, AWS WAF, F5, ModSecurity...).

Ejemplo de uso:

```bash
wafw00f http://ejemplo.com
```

Cabe mencionar que esta herramienta es activa, hace varias peticiones HTTP maliciosas simuladas para ver si son bloqueadas, redirigidas o manipuladas, lo cual puede ser detectado por el objetivo.

----

### Enumeración de subdominios con **sublist3r**

## ¿Qué es **Sublist3r**?

**Sublist3r** es una herramienta de **enumeración de subdominios** que recopila subdominios **públicamente visibles** de un dominio objetivo usando múltiples fuentes OSINT (como motores de búsqueda). Sublist3r es mayoritariamente pasivo, cabe mencionar que si la pasamos el parámetro **-p** para hacer brute force, entonces se vuelve activo.

## ¿Qué hace exactamente Sublist3r?

- Consulta fuentes públicas como:  
    `Google, Bing, Yahoo, Netcraft, VirusTotal, ThreatCrowd, DNSdumpster, crt.sh, etc.`


Ejemplo de uso:

```bash
sublist3r -d ejemplo.com
```

- El parámetro **-d** es para especificar el dominio que vamos a atacar.

---

## 🔍 Google Dorks

¿Qué son los **Google Dorks**?

Son **búsquedas avanzadas** en Google que permiten **encontrar información sensible o expuesta públicamente** mediante el uso de operadores especiales.

🧠 Esta técnica también se conoce como **Google Hacking**.

## 📌 ¿Para qué se usan los Google Dorks?

- Encontrar archivos sensibles (PDFs, DOCs, logs)
- Detectar paneles de administración
- Ver cámaras, logs, backups o contraseñas expuestas
- Localizar subdominios
- Descubrir versiones vulnerables de CMS (WordPress, Joomla…)

Ejemplos prácticos de Google Dorks

| Dork                             | ¿Qué hace?                                       |
| -------------------------------- | ------------------------------------------------ |
| `site:tinder.com`                | Muestra solo resultados del dominio `tinder.com` |
| `site:tinder.com inurl:admin`    | Busca URLs que contengan `admin`                 |
| `site:tinder.com intitle:login`  | Busca páginas con “login” en el título           |
| `site:tinder.com filetype:pdf`   | Muestra PDFs públicos                            |
| `intitle:index.of`               | Indexaciones públicas de carpetas del servidor   |
| `filetype:log password`          | Busca archivos .log con contraseñas              |
| `inurl:/phpinfo.php`             | Busca archivos `phpinfo.php`                     |
| `"Powered by WordPress"` version | Busca sitios WordPress con info de versión       |
| `site:*.tinder.com`              | Encuentra subdominios indexados por Google       |


Herramienta para **Google Hacking Database (GHDB)**:

- Página oficial: https://www.exploit-db.com/google-hacking-database

- Ahí veremos **cientos de dorks** ya listos para:
    - Archivos sensibles
    - Logs
    - Configuraciones
    - Bases de datos expuestas
    - Backdoors
    

---

### Recolección de correo electrónico con theHarvester

**theHarvester** es una herramienta utilizada en pruebas de penetración (pentesting) para **recopilar información pública** sobre un objetivo, y uno de los datos que puede recolectar son los correos electrónicos relacionados con un dominio o empresa.

En concreto, la recolección de correos electrónicos con theHarvester sirve para:

- **Obtener direcciones de correo electrónico relacionadas con el objetivo** (por ejemplo, empleados de una empresa).
    
- **Facilitar el reconocimiento o footprinting**, que es la fase inicial en un pentest, donde se busca toda la información posible sobre el objetivo.
    
- **Encontrar posibles puntos de entrada** para ataques como phishing, spear phishing o ingeniería social.
    
- Ayuda a crear un **mapa de personas y posibles cuentas** para futuros ataques o pruebas.


Ejemplo de uso:

```bah
theHarvester -d ejemplo.com -b bing,crtsh,duckduckgo
```

- `-d ejemplo.com` indica el dominio objetivo.
    
- -b bing,crtsh,duckduckgo especifica la fuente (Google, Bing, LinkedIn, etc.) para la búsqueda.

---

## Bases de datos de contraseñas filtradas

Cuando haces **footprinting** o reconocimiento de un objetivo, es importante buscar **información pública** o filtrada que pueda ayudarte a conocer vulnerabilidades o datos comprometidos, y una fuente valiosa son las **bases de datos de contraseñas filtradas**.

### ¿Qué son las bases de datos de contraseñas filtradas?

- Son conjuntos de datos donde usuarios y sus contraseñas (o hashes) han sido expuestos en brechas de seguridad o hackeos.
    
- Pueden contener combinaciones de usuarios, emails y contraseñas que fueron filtradas y publicadas en internet.
    
- Ejemplos famosos incluyen brechas como **LinkedIn, Adobe, Yahoo**, entre otras.
    

---

### ¿Por qué es útil para un pentester?

- Permite verificar si las cuentas del objetivo ya están comprometidas.
    
- Se puede identificar si el objetivo usa contraseñas débiles o repetidas.
    
- Facilita ataques de **credential stuffing** o fuerza bruta con contraseñas reales.
    
- Da contexto para planificar vectores de ataque.
    

---

### Fuentes y herramientas para buscar bases de datos de contraseñas filtradas

#### 1. **Have I Been Pwned (HIBP)**

- Sitio web y API que te permite consultar si un correo o dominio ha sido comprometido.
    
- Web: [https://haveibeenpwned.com/](https://haveibeenpwned.com/)
    
- También tiene una base con millones de contraseñas filtradas para buscar por hash o texto.
    

#### 2. **Dehashed**

- Motor de búsqueda de datos filtrados, incluyendo emails, contraseñas, IPs.
    
- Se puede usar como fuente en theHarvester (`-b dehashed`).
    

#### 3. **LeakCheck**

- Otro servicio para verificar si tus credenciales han sido filtradas.
    

#### 4. **Bases de datos públicas y dumps**

- Algunos dumps están disponibles en sitios como RaidForums, GitHub (con cuidado legal), etc.
    

---

### Cómo usar algunas herramientas para footprinting de contraseñas filtradas

#### Usando theHarvester con `dehashed`:

```bash
theHarvester -d ejemplo.com -b dehashed
```

---

## Cómo hacer descubrimiento de hosts con nmap

Comando básico para descubrir hosts activos:

```bash
nmap -sn -PR 192.168.1.0/24
````

- -sn (antes -sP) significa ping scan, solo detecta si el host está vivo, no hace escaneo de puertos.

- -PR usa ARP requests (ideal para redes locales).


---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
