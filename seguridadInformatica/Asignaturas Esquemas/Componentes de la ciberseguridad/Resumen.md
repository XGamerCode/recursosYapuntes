tags: #temario #master 

---

Problemas con cifrados
 - Cesar vulnerable a ataque de fuerza bruta debido a que el conjunto de claves es muy pequeño
 - One time pad vulnerable si no se cambia la password en cada cifrado por que el adversario podría empezar a reconocer patrones en el mensaje cifrado.
 - Choosen plaintext atack, el adversario podría ver patrones al ser el mismo el que envía los mensajes pudiendo distinguir un texto cifrado de otro.

---
**Pseudo-random Generator**

Como input tienen n y como output tienen un polinomio de n y siempre es mas grande que el tamaño de input.
El resultado de un **PRG** debe parecer totalmente generado al azar.

El trabajo que hacen estos **PRG** es muy similar a como trabaja el **one time pad** con la peculiaridad de que la clave elegida al azar es mucho mas pequeña, pasa por un algoritmo de ensanchado G y el resultado se le aplica un **XOR** con el mensaje. Para descifrar el mensaje se realizan los mismos pasos, se genera un clave ensanchada al pasar S por el algoritmos G y se le aplica XOR con el texto cifrado para obtener el mensaje.

Para la realización del xor con el mensaje se tiene que generar una cadena de bits igual de grande que el mensaje, esto seria tedioso si tenemos que generar una nueva clave S con cada texto a cifrar, ahí surgen los PRG de tipo stream que generar una clave haciendo uso de G mucho mas grande y van usando trozos de esa clave con cada mensaje.
Existen de dos tipos sincronizados y no sincronizados, siendo los no sincronizados los mas populares.

Para que los PRG de tipo stream no sincronizados funcionen de manera correcta debemos introducir un parámetro **Inicialization vector (IV)** y este va incluido en el texto cifrado.
**El stream cipher mas famoso fue RC4** (RSA) se uso en **WEP, WPA y TLS**  40 a 2048 bits que son entre 5 y 256 bytes para la key 2064 bits de estado.
Cuando este RC4 se uso en WEP se usaban 40 bits para las claves y 24 para el IV posteriormente se ampliaron a 104 bits para la clave y 24 para el IV.

---
Block ciphers y Pseudorandom functions    
AES es una pseudo random permutacion (K = 128 bits)

CBC dependiente de los bloques anteriores
CRT no depende de bloques y es autonomo por bloque

DES clave 56 bits y bloque de 64
IDEA clave de 128 bits y bloque de 64
AES bloques de 128,192,256 con cloque de 128

Modo CBC
![[Pasted image 20250219171017.png]]

![[Pasted image 20250219171036.png]]
![[Pasted image 20250219171100.png]]
![[Pasted image 20250219171228.png]]


---
Hash tienen que ser:
- resistentes a colisiones. ---> 2 mensajes que dan lugar a una colision
- pre-image resistence, que no se puedan invertir y volver a sacar el mensaje.
- second-preimage resistance, yo te doy un mensaje y tu tienes que encontrar otro que haga colision

if is collision resisntance entoces es secon-preimage resistance y además es preimage resistance

parametros para un hash merkle-damgard seguro son mensaje, IV ,longitud del mensaje. El hasheo se realiza de la siguiente manera, se parte el mensaje en blockes y se rellena el final con 00 si hiciera falta, cogemos el primer bloque y le realizamos el hash junto con el inicialización vector(IV), se va hasheando con el bloque anterior hasta llegar al ultimo que se hashea con la longitud del mensaje.

**Merkleproof** nodos hermanos que necesitamos hasta llegar a la raiz 
![[Pasted image 20250219172135.png]]
En la imagen se puede observar como nos piden F5 y el servidor le entrega los recuadros grises que necesita para ir hasheando hasta llegar a la raiz, en este caso el merkleproof es f,l,m

MD5 output 128 bits
SHA1 output 160 bits

---
Un mac seguro tiene los parametros del mensaje, la posicion de cada sub mensaje, la longitud total del mensaje y un IV random para cada mensaje