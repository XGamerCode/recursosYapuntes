
---

`Simple Network Management Protocol` ([SNMP](https://datatracker.ietf.org/doc/html/rfc1157))

Para enumerar este servicio tenemos que escanear por UDP
```bash
sudo apt install onesixtyone
onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt <ip-objetivo>
```

con esto encontraremos el nombre para escanear con  snmpwalk

```bash
snmpwalk -v2c -c <nombre-encontrado> <ip-objetivo>
```

adicionalmente podremos usar braa para forzar encontrar los OIDs (nodos) y enumerar la informacion que contienen

```bash
sudo apt install braa
braa <nombre-encontrado>@<ip-objetivo>:.1.3.6.*
```