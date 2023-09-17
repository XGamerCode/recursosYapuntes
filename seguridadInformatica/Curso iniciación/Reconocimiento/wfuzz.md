
---
- tags: #reconocimiento #herramienta #scanner #web #fuzzing 
- ---
WFuzz es una **herramienta de fuerza bruta que se utiliza para encontrar vulnerabilidades en aplicaciones web**. Es capaz de buscar directorios y archivos ocultos, así como también puede realizar ataques de inyección de parámetros y de fuerza bruta de contraseñas.

Para usar esta herramienta podemos usar por ejemplo los comandos:
```bash
wfuzz -c -t 20 -w <Diccionario a usar> -H "Host: FUZZ.urlAEscanear.com" http://<url>
```

Los comandos son similares a otras herramientas de escaneo, con la diferencias que esta herramienta sustituirá las palabras del diccionario en la palabra FUZZ que le especificamos.

Esto es muy potente porque podemos usarla no solo para subdominios sino para url completas y para encontrar archivos en la web.

comandos especiales:
- --hc oculta el codigo de estado que le especifiquemos.
- --sc muestra el codigo de estado que le especifiquemos.
-  -z list,html-php este comando especifica una lista separada por guiones. y se sustituye en un segundo payload como FUZ2Z o en un tercero como FUZ3Z. 
- -z range,1-50 para hacer rangos.

Alternativamente podemos usar una herramienta llamada fuff de uso similar a esta pero programada en go.