
tags: #reconocimiento 

---

DNS Domain Name System traduce nombres de dominio a direcciones ip.

![[Pasted image 20251021104748.png]]

![[Pasted image 20251021104803.png]]

Para enumerar el servicio manualmente

Interactuamos con el servidor:
```bash
dig ns inlanefreight.htb @10.129.14.128
```

Intentamos extraer su versión 
```bash
dig CH TXT version.bind 10.129.120.85
```

Revisamos la invio