
---

Este protocolo nos permite conectarnos a una maquina windows a su escritorio remoto.

Podemos saber si tiene habilitada esta opcion lanzando un scaneo con nmap y el resultado nos arroja el puerto 3389 abierto

![[Pasted image 20251215142408.png]]

para conectarnos necesitaremos un usuario valido y ejecutar el siguiente comando:
```bash 
xfreerdp /v:<ip-objetivo> /u:<usuario> /p:<contraseña>
```