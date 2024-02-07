tags: #comandos #informacion 

---

Utilidad de redpara interactuar con puertos TCP/UDP. Se puede usar para muchas cosas durante una prueba de penetración.
Su uso principal es para conectares a shells.
Además de eso, se puede usar para conectarse a cualquier puerto de escucha e interactuar con el servicio que se ejecuta en ese puerto. Por ejemplo, enviar todos los datos a un puerto concreto.

```bash
netcat <ip> <puerto>
```

Si ejecutamos ese comando a un puerto valido este nos enviara su banner indicándonos que esta corriendo por ahí.
![[netcatBanner.png]]

a esto se le denomina Banner Grabbin.

Otra Herramienta similar seria Socat.(tambien usada para upgradear una shell a una full TTY)
[[Upgrading Simple Shells to Fully Interactive TTYs - ropnop blog](https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/#method-2-using-socat)]
