---
layout: default
title: Preparación EJPTv2
---

# 🐍 Servidor Web Local en Python

Un servidor web local en Python es una herramienta que te permite ejecutar un servidor web en tu propio ordenador para probar y desarrollar aplicaciones o sitios web sin necesidad de conectarte a Internet. Python proporciona módulos integrados, como el paquete http.server, que te permiten iniciar rápidamente un servidor para servir archivos estáticos (HTML, CSS, imágenes) directamente desde un directorio, facilitando el desarrollo y la depuración. 

Esto nos será muy util para la transferencia de archivo entre nuestra máquina atacante y nuestra máquina victima, como reverse shells, etc...

```bash
python3 -m http.server 80 # Inicia un servidor HTTP básico
```

