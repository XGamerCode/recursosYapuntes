tags: #reconocimiento 

---

Internet Message Acces Protocol (IMAP) se utiliza para acceder a los correos electrónicos de un servidor de correo si es posible.
Este protocolo usa comúnmente los puertos 143 y 993 

![[Pasted image 20251106090240.png]]

Post Office Protocol (POP3) permite la sincronización de un cliente de correo electrónico local con un buzón del servidor.
Este protocolo usa comunmente los puertos 110 y 995.
![[Pasted image 20251106090257.png]]

Los puertos 993 y 995 utilizan encriptación TLS/SSL.

- para enumerar estos servicios se puede usar nmap:
```bash
sudo nmap -sCV -p110,143,993,995 <ip-objetivo>
```

- También podemos intentar conectar con curl si tenemos usuario.
```bash
 curl -k 'imaps://10.129.14.128' --user <user>:<passsword> -v
```

- haciendo uso de OpenSSl con TLS para interactuar con pop3
```bash
openssl s_client -connect <ip-objetivo>:pop3s
```

- haciendo uso de OpenSSl con TLS para interactuar con IMAP
```bash
openssl s_client -connect 10.129.14.128:imaps
```