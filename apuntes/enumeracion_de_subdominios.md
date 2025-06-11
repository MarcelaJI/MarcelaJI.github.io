---
layout: default
title: Apuntes
---

# Enumeración de subdominios

La enumeración de subdominios es una de las fases cruciales en la seguridad informática para identificar los subdominios asociados a un dominio principal.

Los subdominios son parte de un dominio más grande y a menudo están configurados para apuntar a diferentes recursos de la red, como servidores web, servidores de correo electrónico, sistemas de bases de datos, sistemas de gestión de contenido, entre otros.

Al identificar los subdominios vinculados a un dominio principal, un atacante podría obtener información valiosa para cada uno de estos, lo que le podría llevar a encontrar vectores de ataque potenciales. Por ejemplo, si se identifica un subdominio que apunta a un servidor web vulnerable, el atacante podría utilizar esta información para intentar explotar la vulnerabilidad y acceder al servidor en cuestión.

Existen diferentes herramientas y técnicas para la enumeración de subdominios, tanto pasivas como activas. Las herramientas pasivas permiten obtener información sobre los subdominios sin enviar ninguna solicitud a los servidores identificados, mientras que las herramientas activas envían solicitudes a los servidores identificados para encontrar subdominios bajo el dominio principal.

Algunas de las herramientas pasivas más utilizadas para la enumeración de subdominios incluyen la búsqueda en motores de búsqueda como Google, Bing o Yahoo, y la búsqueda en registros DNS públicos como PassiveTotal o Censys. Estas herramientas permiten identificar subdominios asociados con un dominio, aunque no siempre son exhaustivas. Además, existen herramientas como CTFR que utilizan registros de certificados SSL/TLS para encontrar subdominios asociados a un dominio.

También se pueden utilizar páginas online como Phonebook.cz e Intelx.io, o herramientas como sublist3r, para buscar información relacionada con los dominios, incluyendo subdominios.

Por otro lado, las herramientas activas para la enumeración de subdominios incluyen herramientas de fuzzing como wfuzz o gobuster. Estas herramientas envían solicitudes a los servidores mediante ataques de fuerza bruta, con el objetivo de encontrar subdominios válidos bajo el dominio principal.

Las herramientas más comunes son:

- Phonebook (Herramienta pasiva): https://phonebook.cz/

- Intelx (Herramienta pasiva): https://intelx.io/
CTFR (Herramienta pasiva): https://github.com/UnaPibaGeek/ctfr

- Gobuster (Herramienta activa): https://github.com/OJ/gobuster

- Wfuzz (Herramienta activa): https://github.com/xmendez/wfuzz

- Sublist3r (Herramienta pasiva): https://github.com/huntergregal/Sublist3r

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #33ff33;">
    💻 Hecho con 💚 por <strong>Marcela</strong> - 2025
</div>