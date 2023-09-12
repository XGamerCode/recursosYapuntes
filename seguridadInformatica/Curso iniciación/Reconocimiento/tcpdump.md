
---

- tags: #reconocimiento #herramienta #sniffer

---
**tcpdump** sirve para capturar el trafico y guardarlo en un archivo. Este archivo podrá ser analizado con alguna herramienta tipo wireShark o similares.

Uso: 
- requisito necesitas saber tu interfaz de red, esto se puede averiguar ejecutando el siguiente comando que nos mostrará las interfaces de red disponibles en nuestra maquina.
```bash
ifconfig
```

- comando para comenzar la captura de paquetes.
```bash
tcpdump -i <interfaz-red> -w <archivo-destino> -v
```