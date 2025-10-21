
tags: #reconocimiento 

---

SMTP Simple Mail Transfer Protocol es el protocolo para enviar emails en una red de ips.
Por defecto este servicio por el puerto 25, 465 o el 587.

podemos interactuar con el servicio haciendo usaro de telnet
```bash
telnet <ip-objetivo> <puerto-smtp>
```

Se puede verificar el nombre de dominio con el comando HELO/EHLO que respondera con 250 si el nombre existe.
```bash 
telnet <ip-objetivo> <puerto-smtp>
HELO <mail1.dominio>
```

En algunas ocasiones podemos enumerar usuarios validos con el comando vrfy que responderá con el estado 252 si el usuario existe, sino existe no responderá nada.

```bahs 
telnet <ip-objetivo> <puerto-smtp>
VRFY <usuario a verificar>
```

comandos útiles:
![[Pasted image 20251021111149.png]]

Para enumerar el servicio lo podemos hacer con la herramienta mnap

```bash
sudo nmap <ip-objetivo> -sCV -p25
```

Adicionalmente podemos ver si tiene open relay con el script smtp-open-relay 

```bash 
sudo nmap <ip-objetivo> -p25 --script smtp-open-relay 
```
