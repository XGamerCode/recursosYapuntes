
tags: #herramienta #reconocimiento #scanner 

---

para instalar este crewler:
```bash
pip3 install scrapy
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
unzip ReconSpider.zip

```
 este crawler esplorara todo el dominio y nos generara un respnse.json con el resultado, a parte de recorrer la web lee el html buscando comentarios
```bash
python3 ReconSpider.py <dominio-objetivo>
```