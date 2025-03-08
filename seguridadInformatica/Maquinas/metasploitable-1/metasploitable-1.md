tags: #maquina #writeups \

---


Comenzamos la maquina realizando un escaneo de la red en busca de la ip de la maquina victima.
![[Pasted image 20250108185712.png]]
la ip de la maquina victima es **192.168.56.107**

realizamos un escaneo de puertos con nmap para obtener la lista de puertos abiertos
![[Pasted image 20250108190223.png]]
Sobre esta lista vamos a lanzar un escaneo con un conjunto basico de reconocimiento y una serie de scripts para sacar las versiones de los servicios que corren detras de los puertos
![[Pasted image 20250108190714.png]]
![[Pasted image 20250108190738.png]]

En esta caso buscando por metasploit excuentro un exploit interesante para probar para el puerto 445 samba
![[Pasted image 20250110171310.png]]
Después de intentar varias veces este exploit conseguimos una sesion remota, me costo entrar por que hay que congifurar bien el lhost y el lport por que los que vienen por defecto no funcionan bien

en este caso puse lhost 192.168.56.105 por que con la direccion de 127.0.0.1 no funciona y como lport estableci 9999

![[Pasted image 20250110171532.png]]
tenemos ROOT