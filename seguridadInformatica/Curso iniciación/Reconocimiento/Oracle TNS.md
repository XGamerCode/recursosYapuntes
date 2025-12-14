
---
Para enumerar una base de datos Oracle lo primero que haremos es usar nmap con los comandos de siempre, una vez que terminamos deberemos instalar sqlplus para poder conectarnos a la base de datos ejecutando los comandos: 
```bash
wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-basic-linux.x64-21.4.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip
sudo mkdir -p /opt/oracle
sudo unzip instantclient-basic-linux.x64-21.4.0.0.0dbru.zip -d /opt/oracle
sudo unzip instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip -d /opt/oracle
export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_4:$LD_LIBRARY_PATH
export PATH=/opt/oracle/instantclient_21_4:$PATH

```

con eso tendremos instalado el cliente.
Seguidamente instalaremos un programa con el que enumeraremos los llamado odat.py
```bash
git clone https://github.com/quentinhardy/odat.git
cd odat/
pip install python-libnmap
git submodule init
git submodule update
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
```
 y probaremos la instalación haciendo uso de 
```bash
./odat.py -h
```

ahora trataremos de encontrar los sid con odat
```bash
 ./odat.py all -s <ip-objetivo>
```

una vez que el programa odat nos muestra una base de datos y un usuario valido tratamos de conectarnos con sqlplus
```bash
```shell-sessio
sqlplus scott/tiger@10.129.204.235/XE
```
