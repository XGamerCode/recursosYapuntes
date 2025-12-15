
#reconocimiento 

---

NFS o Network File System es un sistema de archivos de red desarrollado por Sun Microsystems y tiene el mismo proposito que el SMB.

- La carpeta donde se configura es en /etc/exports
- Se puede agregar una carpeta haciendo uso de los comandos

```bash
echo '/mnt/nfs  <conjunto-ip-a-compartir>/24(<opciones>)' >> /etc/exports
systemctl restart nfs-kernel-server 
exportfs
```

Las opciones se establecen separadas por comas y pueden ser:
![[Pasted image 20251010115124.png]]

con esto ya tendríamos una carpeta compartida en la subred

- las opciones con las que hay que tener cuidado son:
![[Pasted image 20251010115226.png]]

---
ENUMERACION

Para realizar un reconocimiento de este servicio se puede hacer uso de nmap con -sCV 

Una vez terminado podemos hacer uso de los scripts de nfs que tiene nmap

```bash
sudo nmap --script nfs* <ip-objetivo> -sV -p111,2049
```

Una vez que tenemos enumerado el servicio podemos proceder a montar las carpetas compartidas en nuestro sistema.

- showmount nos mostrara las carpetas disponibles para montar
```bash
showmount -e <ip-objetivo>
```

- Montamos la carpeta en una carpeta local:

```bash
mkdir target-NFS
sudo mount -t nfs <ipobjetivo>:/<nombre-carpeta-remota> ./target-NFS/ -o nolock
cd target-NFS
```

a partir de aquí podemos usar comandos comunes de linux para ver los archivos o los grupos etc como puede ser ls -la o -n

- Por ultimo desmontamos la carpeta:
```bash
sudo umount ./target-NFS
```

Puede que al intentar acceder a las carpetas compartidas no nos deje por permisos, por eso puede ser importante ejecutar los comandos con SUDO