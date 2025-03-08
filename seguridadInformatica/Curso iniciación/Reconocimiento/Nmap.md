--------------------------------------

- Tags: #reconocimiento #herramienta #scanner 

----
# Definición

**Nmap** es una herramienta de **escaneo de red** gratuita y de código abierto que se utiliza en pruebas de penetración (pentesting) para explorar y auditar redes y sistemas informáticos.

---

# Uso de Nmap

El uso básico de **Nmap** :
```bash
nmap -p- <ip-objetivo>
```

Escaneo de red para la obtención de host:
```bash

nmap -sn 192.168.56.0/24

```

Ejemplo de escaner
```bash
sudo nmap -p- --open -n -Pn -sS --min-rate 4000 <ip-objetivo> -vvv

```

Parámetros comunes de **Nmap** (ojo case sensitive).
- **-p** especifica el/los puertos que van a ser escaneados. Se puede especificar como **-p-** para todos los puertos, **p22** para escanear un puerto concreto como por ejemplo el 22 o por rango de puerto **p1-128** que escanearía desde el puerto 1 al 128. (TCP 65535 puertos)(UDP 65535 puertos).
- **--open** especifica que solo quieres que te retorne los puertos que se encuentren abiertos.
- **-v** especifica que queremos que la salida sea "verbose", a medida que vaya encontrando cosas nos las ira mostrando por pantalla. Variante **-vvv** triple "verbose".
- **-n** especifica que **NO** quieres que te aplique resolución **DNS**. Esto se hace para agilizar un poco el escaneo.
- **-T** especifica la plantilla de temporizado, ajusta la velocidad del escaneo (a mas velocidad mas ruido y menos precisión). Rango de velocidad 0-5. -T0 modo seguro , -T5 modo loco.
- **-sT** **TCP connect scan** especifica que queremos hacer un escaneo por el protocolo **TCP**.
- **-sU** especifica que queremos hacer un scaneo por el protocolo **UDP**
- **-Pn** con este parámetro le especificamos a **Nmap** que de por hecho que el host esta activo. Esto es interesante para que no aplique descubrimiento de host por el protocolo **ARP**. 
- **-sn** ping swip escanea un rango de ips buscando host activos. ejemplo ``nmap -sn <ip>\24``
- **-O** comando para intentar detectar el sistema operativo de un host. (No recomendado, demasiado agresivo).
- **-sV** con este comando Nmap intenta averiguar las versiones de los servicios que corren por un puerto.
- **-sC** comando que especifica que queremos usar un conjunto básico de scripts de reconocimiento (recomendacion usar en un segundo escaneo cuando ya sepamos los puertos)(se puede colapsar con el comando anterior en un solo comando **-sCV**)  
- **-sn** Especificándole una ip o rango de ips (192.168.0.0/24) realiza un descubrimiento de host lanzando trazas icmp denominado **barrido de ping** 
- -sX similar al sS pero en este caso se retorna un paquete reset si el puerto esta cerrado, sino podemos entender que se encuentra abierto.

---
Parámetros para la evasión de firewalls.
- **-f** con este parámetro podemos fragmentar los paquetes enviados por nmap.(se puede jugar con rangos y tamaños).
- **--mtu** este parámetro especifica el tamaño máximo de paquete. (Especificando un tamaño menor que el de la regla del firewall se podría conseguir ver el puerto)(deben de ser múltiplos de 8).
- **-D** falsificación de ip. Este parámetro permite lanzar el escaneo simulando que se realiza desde una ip especifica y distinta a la real. (se puede especificar varias ips con lo que iría variando la ip origen y ocultaríamos mas o menos nuestra ip real ).
- **--source-port** comando donde podemos especificar un puerto concreto, con lo que el escaneo se realizara desde ese puerto y no abriendo uno aleatorio en nuestra maquina.
- **--data-length** manipulación del tamaño de paquete, se le suma al tamaño original (58) el tamaño que le especifiquemos.
- **--spoof-mac** comando con el que podemos falsificar nuestra dirección mac especificando una nueva.
- **-sS** hace que el escaneo sea sigiloso y un poco mas rápido cortando la respuesta ack y no completando la conexión.
- **--min-rate** cantidad de paquetes que son enviados como mínimo, sirve para agilizar el escaneo y para garantizar el resultado.

---
Scripts nmap:
- **default**: Esta es la categoría predeterminada en Nmap, que incluye una gran cantidad de scripts de reconocimiento básicos y útiles para la mayoría de los escaneos.
- **discovery**: Esta categoría se enfoca en descubrir información sobre la red, como la detección de hosts y dispositivos activos, y la resolución de nombres de dominio.
- **safe**: Esta categoría incluye scripts que son considerados seguros y que no realizan actividades invasivas que puedan desencadenar una alerta de seguridad en la red.
- **intrusive**: Esta categoría incluye scripts más invasivos que pueden ser detectados fácilmente por un sistema de detección de intrusos o un Firewall, pero que pueden proporcionar información valiosa sobre vulnerabilidades y debilidades en la red.
- **vuln**: Esta categoría se enfoca específicamente en la detección de vulnerabilidades y debilidades en los sistemas y servicios que se están ejecutando en la red.
Comandos:
- **--script** seguido de las categorias entre comillas y separadas por and ejemplo --script "intrusive and vuln"
- **--script http-enum** script que aplica fuzzing sobre un puerto para averiguar direcciones de un dominio.