
tags: #reconocimiento 

---

DNS Domain Name System traduce nombres de dominio a direcciones ip.

![[Pasted image 20251021104748.png]]

![[Pasted image 20251021104803.png]]

Para enumerar el servicio manualmente

![[Pasted image 20260111115251.png]]


Interactuamos con el servidor:
```bash
dig ns <nombre-DNS-objetivo> @<ip-objetivo>
```

Intentamos extraer su versión 
```bash
dig CH TXT version.bind <ip-objetivo>
```

Revisamos la información disponible del registro any
```bash
dig any <nombre-DNS-objetivo> @<ip-objetivo>
```

Se intenta un cambio de zona:
```bash
dig axfr <nombre-DNS-objetivo> @<ip-objetivo>
```

Se intenta un cambio de zona interna:
```bash
dig axfr subdominio.<nombre-DNS-objetivo> @<ip-objetivo>
```
La transferencia de zona básicamente es  una copia de todos los subdominios eliminando la necesidad de realizar fuera bruta, raramente se puede acontecer.

También se puede intentar hacer fuerza bruta con un diccionario con la herramienta dnsenum

```bash
dnsenum --dnsserver <ip-objetivo> --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt <nombre-dominio>
```

Mas herramientas para enumerar DNS

![[Pasted image 20260111115040.png]]

