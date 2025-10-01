tags: #informacion #metodos #reconocimiento 

---

- Ver certificado SSL del dominio principal si lo tiene. (De a qui podemos sacar mucha info extra entre ella posibles subdominios)
- Ver [crt.sh] donde podemos encontrar los certificados de la empresa.
- En la misma url con el siguiente comando podemos listar los subdominios que contiene 
```bash
curl -s https://crt.sh/\?q\=<dominio.com>\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```

- Con shodan también podemos encontrar ips asociadas a dominios además de darnos puertos abiertos y mucha información de manera pasiva
```
dig any <dominio.com>
```
- Con Domain.Glass podemos extraer la ip de por ejemplo un dominio AWS o Azure