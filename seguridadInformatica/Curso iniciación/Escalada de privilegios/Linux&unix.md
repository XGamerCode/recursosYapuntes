
---
- tags: #EscaladaPrivilegios #linux #unix 
---

Para escalar privilegios en este sistema tendremos que observar varias posibilidades a ver si alguna de ellas nos permite obtener nuestro objetivo.
Entre ellas podemos observar:

- Permisos SUID / SGID.
- Cron jobs.
- Configuración errónea de servicios.
- Kernel exploits.
- Herramientas automatizadas.

**METODO SSH** la conexión por ssh es muy común y se establece por dos métodos, el primero es por contraseña que introducirá el usuario al intentar conectar por este protocolo, la segunda es mediante una contraseña por clave publica/privada que se guardara en un archivo que se le pasa al intentar establecer la conexión.

- En el directorio del usuario se guardan las claves establecidas para la conexión ssh.
```bash 
/home/<usuario>/.ssh/
```
- Para la generación de una clave con la que podamos conectar por SSH usaremos
```bash 
ssh-keygen
```

- Para usar la clave generada usaremos el comando -I
```bash 
ssh <user>@<ip-objetivo> -i <archivo-clave-ssh>
```
- **EXPLOTACION** ,para explotar esto deberemos de obtener la clave privada o el directorio con permisos de escritura. Si esto sucede podremos obtener la clave shh o **sobreescribirla** 

**METODO SUDO** por lo general la configuración de sudo se establece en el archivo
```bash 
/etc/sudoers
```
Normalmente se necesitan privilegios root para ver o editar este fichero.
- En el caso de no tener privilegios suficientes como para editar o ver el archivo sudoers, podremos usar un comando para listar los comandos que podemos ejecutar con privilegios especiales desde el usuario actual con el comando:
```bash 
sudo -l
```

**METODO SUID & SGID**
Existen archivos con permisos especiales que al ejecutarlos, los estaremos ejecutando como el usuario que lo creo (**SUID**) o como el grupo que lo creo (**SGID**). Esto quiere decir que aunque nuestro usuario no tenga permiso para realizar una acción, si el archivo la puede realizar, lo podremos ejecutar y obtener el resultado. 
- Para buscar los ficheros con permisos especiales que tiene un usuario podemos usar el comando:
```bash
find / -perm -u=s -type f 2> /dev/null
```
- Si por ejemplo al usar el comando anterior detectamos que tenemos privilegios para ejecutar python con usuario elevado, podríamos intentar esto.
```bash
python -c 'import os,pty; os.setresuid(new_id, new_id, new_id); pty.spawn("/bin/bash")' 
os.setresuid(ruid, euid, suid);
```
en los id solo deberemos poner los id del usuario que queremos usurpar, y podemos ver los nuestros con el comando id

**METODO CRON**
Todos los usuarios tienen asignadas tareas cron que pueden ver con el comando:
```bash
crontab -l
```
y también las pueden editar con el comando:
```bash 
crontab -e
```
También existen crons a nivel de sistema, estos están ubicados en la carpeta:
```bash
/etc/crontab
```
El contenido de ese fichero se ejecutara con privilegio root, la sintaxis de un cron es:
![[Pasted image 20250125171128.png]]\
Con la ayuda de **pspy** podemos ver las tareas sin ser root y monitorear todos los comandos que lanzan.

**METODO EXPLOIT KERNEL** 
Este método se debe de usar solo como ultima opción y si con todo lo anterior no encontramos nada, debido a que explotaremos directamente el núcleo del sistema operativo y podríamos causar su corrupción.
Para realizar esto deberemos de averiguar el sistema operativo que corre en la maquina y su versión de kernel. Para ello podremos usar la herramienta **linux-exploit-suggester.sh** que nos indicara la versión de kernel que corre en la maquina. Tambien podremos usar los comandos de shell:
sistema operativo
```bash 
lsb_release -a 
```
kernel 
```bash
uname -r
```

**METODO AUTOMATICO**
Disponemos de una herramienta que se llama **linenum** con la que podemos automatizar todo lo anterior. para usarla deberemos descargarla desde su repositorio de github
```bash
https://github.com/rebootuse r/LinEnum
```