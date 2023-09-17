
----
- tags: #reconocimiento #herramienta #scanner #web #fuzzing 
---
Gobuster es una herramienta de software para directorios de fuerza bruta en servidores web. [Gobuster - Platzi](https://platzi.com/clases/2984-inteligencia-activa/48380-gobuster/)

- Para enumerar directorios de una pagina web podemos usar los siguientes comandos:

```bash
gobuster dir -u <url-objetivo> -w <diccionario-a-usar> -t 50
```
- -b se puede ocultar códigos de estado separados por comas.
- -x se especifican extensiones con las que probar para encontrar archivos de ese tipo.


- Para ejecutar un análisis de subdominios podríamos usar los comandos:

```bash
gobuster vhost -u <URL-objetivo> -w <diccionario-a-usar> -t 20
```

- -u url a la que vamos a analizar con fuerza bruta.
- -w diccionario que usaremos para el descubrimiento de subdominios.
- -t numero de hilos de ejecución que vamos a utilizar para paralelizar el escaneo.
- si encontramos datos que no nos interesan podemos filtrar con grep -v segido de un codigo de estado para no mostrarlas
Podríamos usar por ejemplo el diccionario de subdominios de seclist [diccionario seclists (github.com)](https://github.com/danielmiessler/SecLists)
