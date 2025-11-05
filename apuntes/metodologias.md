---
layout: default
title: Apuntes
---


# Metodologías de pruebas de penetración

Las pruebas de penetración pueden tener una amplia variedad de objetivos y metas dentro de su alcance. Por ello, ninguna prueba de penetración es igual a otra, y no existe una solución universal en cuanto a cómo un evaluador de penetración debe abordarla. 

Los pasos que sigue un evaluador de penetración durante una intervención se conocen como metodología. Una metodología práctica es inteligente, pues los pasos seguidos son relevantes para la situación en cuestión.  Por ejemplo, tener una metodología que se usaría para probar la seguridad de una aplicación web no es práctico cuando se trata de probar la seguridad de una red.


Antes de analizar algunas metodologías estándar de la industria, debemos tener en cuenta que todas ellas tienen un tema general de las siguientes etapas:  

|   |   |
|---|---|
|**Escenario** | **Descripción**|
|Recopilación de información|Esta etapa implica recopilar tanta información accesible públicamente sobre un objetivo u organización como sea posible, por ejemplo, OSINT e investigación.<br><br>**Nota:** Esto no implica escanear ningún sistema.|
|Enumeración/Escaneo|Esta etapa implica descubrir las aplicaciones y los servicios que se ejecutan en los sistemas. Por ejemplo, encontrar un servidor web potencialmente vulnerable.|
|Explotación|Esta etapa implica aprovechar las vulnerabilidades descubiertas en un sistema o aplicación. Puede implicar el uso de exploits públicos o la explotación de la lógica de la aplicación.|
|Escalada de privilegios|Una vez que se ha explotado con éxito un sistema o aplicación (lo que se conoce como punto de apoyo), esta etapa consiste en intentar ampliar el acceso al sistema. Se puede escalar horizontal y verticalmente: horizontalmente se accede a otra cuenta del mismo grupo de permisos (es decir, otro usuario), mientras que verticalmente se accede a la de otro grupo de permisos (es decir, un administrador).|
|Post-explotación|Esta etapa consta de algunas subetapas:  <br><br>**1.** ¿A qué otros hosts se puede apuntar (pivotación)?<br><br>**2.** ¿Qué información adicional podemos recopilar del host ahora que somos un usuario privilegiado?<br><br>**3.**  Cubriendo tus huellas<br><br>**4.** Informes|


---

<div style="text-align:center; font-size: 0.9em; margint-top: 40px; color: #fefefeff;">
    © 2025 <strong>Marcela Jimenez</strong>
</div>>