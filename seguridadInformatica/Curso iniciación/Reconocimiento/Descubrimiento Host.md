
---
-  tags: #reconocimiento #metodos #hosts
---
Para descubrir los host que hay activos en una red tenemos varias alternativas.

- Con la herramienta [[Nmap]] podemos usar el operador -sn para realizar un scaneo de una ip con su [CIDR](https://es.wikipedia.org/wiki/Classless_Inter-Domain_Routing) que nos retornaría los hosts que se encuentran activos en la red.
  Este escaneo se realiza mediante trazas ICMP [Protocolo de control de mensajes de Internet - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Protocolo_de_control_de_mensajes_de_Internet)
  
```bash
nmap -sn 192.169.0.0/16
```

- También podemos realizar un descubrimiento de host usando trazas ARP [Protocolo de resolución de direcciones - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Protocolo_de_resoluci%C3%B3n_de_direcciones#:~:text=En%20redes%20de%20c%C3%B3mputo%2C%20el,a%20una%20determinada%20direcci%C3%B3n%20IP.) Haciendo uso de la herramienta ArpScan con el parametro -I para especificar la interfaz de red que vamos a utilizar, -g para ignorar duplicados y --localnet para especificar que queremos la red local.
  Adicionalmente comentar que podemos observar nuestra interfad de red haciendo uso del comando:
  
```bash
ifconfig
``` 
```bash
arp-scan -I <interfaz-de-red> --localnet -g
```
- Una forma de escanear host de forma mas manual seria:
```bash
timeout 1 bash -c "ping -c 1 <ip-objetivo>" &>/dev/null
echo $?
```

Si el resultado de esos comandos es distinto de 0 es que el host no esta activo y si retorna 0 el host esta activo.
Una forma de automatizar esto en bash seria:

```bash
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo.... \n"
	tput cnorm: exit 1
}

tput civis

# Ctrl+c
trap ctrl_c SIGINT

for i in $(seq 1 254); do
	timeout 1 bash -c "ping -c 1 192.169.111.$i" &>/dev/null && echo "[+] Host 192.168.111.$i - ACTIVE" &
done

wait
tput cnorm
```

Si los host no aceptan traza ICMP podríamos intentar atacar directamente a los puertos mandando una cadena vacía para saber si ese puerto responde:

```bash
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo.... \n"
	tput cnorm: exit 1
}

tput civis

# Ctrl+c
trap ctrl_c SIGINT

for i in $(seq 1 254); do
	for port in $(seq 1 65535)
		timeout 1 bash -c "echo '' > /dev/tcp/192.169.111.$i/$port" &>/dev/null && echo "[+] Host 192.168.111.$i - Port $port (OPEN)" &
	done
done

wait
tput cnorm
```

Estos scripts se pueden modificar para aceptar mas rangos de ips y puertos o automatizar del todo con argumentos parametrizables.

- Por ultimo veremos la herramienta masscan:
```bash
masscan -p21,22,139,445 -Pn 192.168.0.0/16 --rate=5000
```
