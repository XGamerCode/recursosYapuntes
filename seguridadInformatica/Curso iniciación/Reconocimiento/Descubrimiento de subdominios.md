- tags: #reconocimiento #web 

---

Existen dos formas de enumerar los subdominios de un dominio web.

- Pasiva: para realizar un descubrimiento de host de manera pasiva podemos recurrir a las web de búsqueda tipo google y analizar sus resultados, tambien podemos lanzar querys a los servidores DNS o a los repositorios de certificados ssl/tls.
- Activa: esta forma implica interactuar con la maquina victima con alguna herramienta que nos permita realizar fuerza bruta para el reconocimiento de subdominios
![[Pasted image 20260111121349.png]]
Ejemplo de fuerza bruta con diccionario haciendo uso de la herramienta dnsenum siendo -f el comando para indicar el diccionario y -r para que realice la fuerza bruta de manera recursiva 
```bash
dnsenum --enum <dominio-objetivo> -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -r
```