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



