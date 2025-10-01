
Tags: #reconocimiento 

---

- FTP o file transfer protocol.
- Suele correr en el puerto 21.
- Con el siguiente comando podemos ver el archivo de configuración del servidor vsftpd que es un servidor FTP fácil de configurar

```bash
cat /etc/vsftpd.conf | grep -v "#"
```

- En la ruta /etc/ftpusers podremos ver la back list que contiene la lista de usuarios que no tienen permiso para entrar al sftp. 
- El fallo mas importante del FTP es dejar la configuración del usuario anónimo que permite interactuar con el FTP sin autenticarse.
- Algunos comandos utiles, status, debug,ls, ls -R, get,
- Para descargar todo el contenido de un ftp podemos usar el siguiente comando:
```bash
wget -m --no-passive ftp://anonymous:anonymous@<ip-objetivo>
```

- Con el comando put se pueden subir archivos
- Se pude interactuar con el FTP tambien desde nc, telnet y openssl.
```bash
nc -nv 10.129.14.136 21

telnet 10.129.14.136 21

openssl s_client -connect 10.129.14.136:21 -starttls ftp
```