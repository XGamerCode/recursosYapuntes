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


Ajustes sensibles de smb que se pueden aprovechar por el atacante
![[Pasted image 20251002172323.png]]
