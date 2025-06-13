---
layout: default
title: Apuntes
---

# ¿Qué es Metasploit?

Metasploit Framework es una plataforma de código abierto que permite a los investigadores de seguridad y hackers éticos probar la seguridad de sistemas informáticos. Incluye una amplia base de datos con exploits, payloads (cargas útiles), scanners y otras herramientas para hacer pruebas avanzadas.

---

## ¿Cómo funciona Metasploit?

Metasploit funciona combinando tres elementos:

- Exploit: Es el código que aprovecha una vulnerabilidad específica en un sistema o aplicación.

- Payload: Es la carga que se ejecuta una vez explotada la vulnerabilidad, por ejemplo, abrir una consola remota.

- Auxiliary: Herramientas para escaneo, sniffing o ataques que no necesariamente involucran exploits.

---

### Instalación básica

En la mayoría de distribuciones de Linux como Kali, Metasploit ya viene instalado. Si quieres instalarlo en otras distribuciones o Windows, puedes hacerlo desde la web oficial o usando:

```bash 
sudo apt install metasploit-framework
```

Para iniciarlo, solo escribe:
```bash
msfconsole
```

Este comando abre la consola interactiva de Metasploit, desde donde harás la mayoría de las tareas.

---

## Comandos básicos para comenzar: 

Aquí te dejo una lista con comandos clave y para qué sirven:

Comando	Descripción
- search [palabra]:	Buscar módulos por nombre o vulnerabilidad.
- use [módulo]: Seleccionar un módulo para usar (exploit, payload, etc.)
- show options:	Mostrar las opciones configurables del módulo actual.
- set [**opción**] [**valor**]: Configurar una opción del módulo (ejemplo: RHOSTS, LHOST).
- show payloads: Listar payloads compatibles con el exploit seleccionado.
- set payload [payload]:	Seleccionar el payload que se va a usar.
- exploit o run: Ejecutar el exploit con la configuración actual.
- sessions:	Mostrar sesiones activas (conexiones abiertas con víctimas).
- sessions -i [id]: Interactuar con una sesión activa.
- exit:	Salir de msfconsole.


---



<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>
