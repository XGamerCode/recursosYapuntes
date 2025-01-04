- Tags: #reconocimiento #herramienta #scanner 
---

Herramienta con la que podemos escanear una red completa para el descubrimiento de host.

necesita permisos sudo

```bash
sudo netdiscover

```

para escanear un rango de ips

```bash

sudo netdiscover -r 192.168.56.0/24

```

también se puede usar de manera pasiva con el comando -p