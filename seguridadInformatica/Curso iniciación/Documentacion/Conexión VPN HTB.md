tags: #informacion #comandos

---

- Para conectar mediante vpn a la plataforma hack the box se utiliza un archivo que hay que descargar desde la pagina web terminado en .ovpn y con el comando que se muestra a continuación:

```bash
sudo openvpn <archivovpn>.ovpn
```

	Como se puede ver este comando se ejecuta con privilegios sudo.

- comandos útiles para ver la de nuestras ips.
```bash
ifconfig
```

- con ifconfig vemos nuestra configuración de ip .

```bash
netstat -rn
```

- netstat -rn sirve para ver las redes accesibles desde la nuestra.