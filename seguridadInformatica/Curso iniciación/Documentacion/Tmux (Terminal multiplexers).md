tags: #herramienta #comandos 

---

Tmux sirve para abrir varias terminales en una misma ventana y poder saltar entre una y otra.

Se puede instalar con el siguiente comando:

```bash
sudo apt install tmux -y
```

Una vez instalado podemos iniciarlo:

```bash
tmux
```

Para abrir nuevas terminales en Tmux presionamos la tecla para introducir comandos en Tmux CTRL + B y después la tecla C que nos abrirá una nueva terminal
![[Pasted image 20250901134551.png]]

Presionando las teclas de comando de Tmux y un numero del pad numérico podemos cambiar entre una shell y otra que vendrá especificada con un * la que esta activa
``` bash 
CRTL + c y despues 1
```
![[Pasted image 20250901134734.png]]

Tambien se puede partir la pantalla verticalmente y horizontalmente con la tecla comando Tmux y SHIFT + % y SHIFT + "

![[Pasted image 20250901175443.png]]

Para moverse entre las tres terminales del ejemplo anterior pulsamos el comando Tmux y con las flechas del teclado cambiamos entre terminales.

CHEATSHEET  de la terminal de Tmux [[Tmux Cheat Sheet & Quick Reference | Session, window, pane and more](https://tmuxcheatsheet.com/)]

Comandos mas interesantes sobre paneles partidos:

![[Pasted image 20250901180900.png]]
Para copiar texto teniendo la configuración de ratón activa en tmux se puede presionar el tecla shift y seleccionar lo que quieres copiar y así te deje usar contrl+shift+c
