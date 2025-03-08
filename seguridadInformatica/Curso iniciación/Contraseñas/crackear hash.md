
---

Para identificar el tipo de hash podemos utilizar la herramienta **hash-identifier** a la cual le podemos pasar el hash y nos retornara las posibilidades de algoritmos correspondientes al hash

Posteriormente podemos usar la herramienta **hashcat** a la cual le pasamos -m para indicar el algoritmo de hashing, un archivo con el hash entre comillas simples y el diccionario con el cual probaremos a ver si encontramos la contraseña

para encontrar contraseñas en una maquina podriamos probar a buscar si tenemos acceso al /etc/passwd
y tambien necesitamos el /etc/shadow el cual tiene el hash de la contraseña de los usuarios.

- para crackear la pass de un archivo .zip se puede usar el modulo zip2john para pasar el hash a un archivo que reconoce john the ripper y asi poder hacer un ataque de fuerza bruta al hash
```bash 
zip2john <nombre-archivo>.zip > hash
```

```bash
john --wordlist=<ruta-diccionario> hash
```