tags: #reconocimiento 

---
SMB Server Message Block

Conexión a un smb:
```bash
smbclient -N -L //<ip-objetivo>
```

Para descargar un recurso del SMB se utiliza el comando GET

Con smbstatus se puede ver mucha info interesante sobre las conexiones realizadas.

Para enumerar un SMB podemos usar el cliente rpc con el comando:
```bash
rpcclient -U "" <ip-objetivo>
```
y podemos usar los siguientes comandos
![[Pasted image 20251002173342.png]]
```bash
querygroup 0x201
```


Ajustes sensibles de smb que se pueden aprovechar por el atacante
![[Pasted image 20251002172323.png]]

a parte de rpcclient tambien se puede usar smbmap y CrackMapExec
![[Pasted image 20251002173922.png]]

enum4linux-ng 
para instalar este recurso: 
```bash 
git clone https://github.com/cddmp/enum4linux-ng.git
cd enum4linux-ng
pip3 install -r requirements.txt
```
se ejecuta con:

```bash
./enum4linux-ng.py <ip-objetivo> -A
```

