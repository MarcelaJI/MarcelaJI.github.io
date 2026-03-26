---
layout: default
title: Artículos Técnicos
---

## WannaCry

### El ransomware que paralizó el mundo (análisis técnico completo)

- **Autor:** Marcela Jiménez  
- **Fecha de publicación:** 26 de marzo de 2026
- **Categoría:** Ciberseguridad/Malware

#### Introducción

El 12 de mayo de 2017 marcó un antes y un después en la historia de la ciberseguridad. Ese día apareció *WannaCry*, uno de los ataques de ransomware más devastadores jamás registrados, capaz de propagarse a nivel global en cuestión de horas.

A diferencia de otros ataques, *WannaCry* no solo cifraba archivos:
se comportaba como un gusano (worm), lo que permitía expandirse automáticamente entre sistemas vulnerables sin intervención humana.

---
#### ¿Qué es *WannaCry*?

*WannaCry* en un ransomware, es decir, un tipo de malware diseñado para:
- Cifrar los archivos de la víctima
- Bloquear el acceso al sistema
- Exigir un pago (rescate) para recuperarlos

En este caso, los atacantes pedían 300 dólares en Bitcoin, duplicando la cantidad si no se pagaba a tiempo.

---
#### Impacto global del ataque

El alcance de *WannaCry* fue masivo:
- Más de 230.000 dispositivos infectados
- Presente en más de 150 países 
- Afectó a:
	- Hospitales (como el NHS en Reino Unido)
	- Empresas (Telefónica en España)
	- Infraestructuras críticas
	- Usuarios individuales

Las pérdidas totales se estiman en más de 4.000 millones de dólares, aunque los atacantes solo obtuvieron aproximadamente 130.000 dólares en rescates.

---

#### La clave técnica: *EternalBlue*
El elemento más crítico del ataque fue el uso del exploit *EternalBlue*.

¿Qué es *EternalBlue*?
*EternalBlue* es un exploit que aprovecha una vulnerabilidad en el protocolo:

✅*SMBv1* (Server Message Block) de Microsoft Windows

Esta vulnerabilidad fue registrada como:

✅CVE-2017-0144

Y corregida mediante el parche:

✅ MS17-010

---

#### ¿Cómo funcionaba el ataque?

1. Explotación de SMB

*WannaCry* utilizaba *EternalBlue* para enviar paquetes especialmente diseñados a sistemas vulnerables.

Esto permitía:

- Ejecutar código remoto sin autenticación 
- Tomar control del sistema objetivo

---

2. Ejecución en Windows

Una vez dentro del sistema, el malware:
- Instalaba un backdoor (DoublePulsar)
- Ejecutaba código malicioso en memoria
- Escaneaba la red local en busca de más dispositivos vulnerables

---

3. Propagación automática

Aquí está la diferencia clave:

*WannaCry* no necesitaba la interacción del usuario

Se propagaba automáticamente a través de la red explotando la misma vulnerabilidad  en otros equipos.

---

4. Cifrado de archivos

El malware:
- Cifraba archivos importantes (documentos, imágenes, bases de datos)
- Usaba algoritmos criptográficos fuertes (AES + RSA)
- Cambiaba extensiones de archivos

---

5. Pantalla de rescate

Mostraba un mensaje indicando:

	"Oops, your files have been encrypted"

Incluyendo:
- Temporizador
- Dirección de pago en Bitcoin
- Instrucciones de recuperación

---

#### El papel de la NSA y la filtración

Uno de los aspectos más polémicos del caso es el origen de *EternalBlue*.

Se ha reportado que:

- Fue desarrollado por la NSA (Agencia de Seguridad Nacional EE.UU)
- No se divulgó inmediatamente a Microsoft
- Fue filtrado por el grupo *The Shadow Brokers* en 2017

Esto permitió que ciberdelincuentes accedieran a una herramienta extremadamente potente.

---

#### ¿Se podría haber evitado?
Sí

Microsoft había publicado el parche:

✅ MS17-0144 en marzo de 2017

Sin embargo:

- Muchas organizaciones no actualizaron sus sistemas
- Especialmente en entornos críticos (hospitales, empresas)

Esto facilitó la propagación masiva.

---

#### El "Kill Switch": cómo se detuvo WannaCry

Un investigador de seguridad británico, Marcus Hutchins (MalwareTech), analizó el malware y descubrió algo clave;

✅ *WannaCry* intentaba conectarse a un dominio web no registrado

Hutchins:

- Compró el dominio por ~10 dólares
- Activó sin saberlo un Kill Switch

Eso detuvo la propagación del malware a nivel global.

---

#### Evolución del ransomware tras *WannaCry*

*WannaCry* marcó un punto de inflexión:
- Aumento masico de ataques de ransomware
- Aparición de modelos como:
	- Ransomware-as-a-Service (RaaS)
- Ataques más dirigidos y sofisticados
- Uso de:
	- Ingeniería social
	- Zero-days
	- Técnicas de evasión avanzadas

---

#### Lecciones clave de ciberseguridad

*WannaCry* dejó varias enseñanzas fundamentales:

1. Importancia de las actualizaciones
No aplicar parches puede tener consecuencias críticas.

2. Segmentación de red
Evita que un ataque se propague fácilmente.

3. Desactivar SMBv1
Es un protocolo obsoleto e inseguro.

4. Copias de seguridad
Permiten recuperar datos sin pagar rescates.

5. Monitorización y respuesta
Detectar actividad anómala a tiempo es clave.

---

#### Conclusión

*WannaCry* no fue solo un ataque más. Fue una demostración real de cómo una vulnerabilidad no parcheada, combinada con herramientas avanzadas, puede escalar hasta convertirse en una crisis global.

Hoy en día, sigue siendo un caso de estudio esencial en ciberseguridad, recordándonos que:

	 La prevención siempre es más importante que la reacción

---


