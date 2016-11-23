# Ejercicios del tema 4: Virtualización ligera usando contenedores
### Ejercicio 1
**Instala LXC en tu versión de Linux favorita. Normalmente la versión en desarrollo, disponible tanto en GitHub como en el sitio web está bastante más avanzada; para evitar problemas sobre todo con las herramientas que vamos a ver más adelante, conviene que te instales la última versión y si es posible una igual o mayor a la 1.0.**

Se instala mediante:
```bash
$ sudo apt-get install lxc
```
Y comprobamos que la versión es mayor a la 1.0:
```bash
$ lxc-start --version
2.0.5
```
También se comprueba la configuración:
```bash
asus@asus-GL552VW:~/Documentos/IG/Practica 3$ lxc-checkconfig
Kernel configuration not found at /proc/config.gz; searching...
Kernel configuration found at /boot/config-4.4.0-47-generic
--- Namespaces ---
Namespaces: enabled
Utsname namespace: enabled
Ipc namespace: enabled
Pid namespace: enabled
User namespace: enabled
Network namespace: enabled
Multiple /dev/pts instances: enabled

--- Control groups ---
Cgroup: enabled
Cgroup clone_children flag: enabled
Cgroup device: enabled
Cgroup sched: enabled
Cgroup cpu account: enabled
Cgroup memory controller: enabled
Cgroup cpuset: enabled

--- Misc ---
Veth pair device: enabled
Macvlan: enabled
Vlan: enabled
Bridges: enabled
Advanced netfilter: enabled
CONFIG_NF_NAT_IPV4: enabled
CONFIG_NF_NAT_IPV6: enabled
CONFIG_IP_NF_TARGET_MASQUERADE: enabled
CONFIG_IP6_NF_TARGET_MASQUERADE: enabled
CONFIG_NETFILTER_XT_TARGET_CHECKSUM: enabled
FUSE (for use with lxcfs): enabled

--- Checkpoint/Restore ---
checkpoint restore: enabled
CONFIG_FHANDLE: enabled
CONFIG_EVENTFD: enabled
CONFIG_EPOLL: enabled
CONFIG_UNIX_DIAG: enabled
CONFIG_INET_DIAG: enabled
CONFIG_PACKET_DIAG: enabled
CONFIG_NETLINK_DIAG: enabled
File capabilities: enabled

Note : Before booting a new kernel, you can check its configuration
usage : CONFIG=/path/to/config /usr/bin/lxc-checkconfig
```

### Ejercicio 2
**Comprobar qué interfaces puente se han creado y explicarlos.**

En primer lugar se crea la caja de ubuntu:

![img43](Capturas/imagen43.png)

A continuación, se arranca:
```bash
sudo lxc-start -n una-caja
```

Una vez terminado el proceso, accedemos a ella:

![img44](Capturas/imagen44.png)

Aunque es mejor acceder a la consola mediante este comando, facilitándose así la salida de la misma:
```bash
sudo lxc-console -n una-caja
```

Podemos observar las interfaces puente de la caja:
```bash
root@una-caja:/# ifconfig
eth0      Link encap:Ethernet  direcciónHW 00:16:3e:e8:44:c5  
          Direc. inet:10.0.3.184  Difus.:10.0.3.255  Másc:255.255.255.0
          Dirección inet6: fe80::216:3eff:fee8:44c5/64 Alcance:Enlace
          ACTIVO DIFUSIÓN FUNCIONANDO MULTICAST  MTU:1500  Métrica:1
          Paquetes RX:65 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:11 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1000
          Bytes RX:9567 (9.5 KB)  TX bytes:1374 (1.3 KB)

lo        Link encap:Bucle local  
          Direc. inet:127.0.0.1  Másc:255.0.0.0
          Dirección inet6: ::1/128 Alcance:Anfitrión
          ACTIVO BUCLE FUNCIONANDO  MTU:65536  Métrica:1
          Paquetes RX:0 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:0 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1
          Bytes RX:0 (0.0 B)  TX bytes:0 (0.0 B)
```
En el sistema anfitrión, comprobamos que se ha creado una interfaz para la comunicación con la caja:
```bash
asus@asus-GL552VW:~$ ifconfig
lo        Link encap:Bucle local  
          Direc. inet:127.0.0.1  Másc:255.0.0.0
          Dirección inet6: ::1/128 Alcance:Anfitrión
          ACTIVO BUCLE FUNCIONANDO  MTU:65536  Métrica:1
          Paquetes RX:6450 errores:0 perdidos:0 overruns:0 frame:0
          Paquetes TX:6450 errores:0 perdidos:0 overruns:0 carrier:0
          colisiones:0 long.colaTX:1
          Bytes RX:1295029 (1.2 MB)  TX bytes:1295029 (1.2 MB)
```

Tras esto, detenemos a la caja:
```bash
sudo lxc-stop -n una-caja
```

### Ejercicio 3
**Crear y ejecutar un contenedor basado en Debian.**

Mi distribución es Ubuntu y el contenedor que he instaldo en el ejercicio anterior es Ubuntu, por lo que he instaldo un contenedor basado en mi misma distribución (Debian)

**Crear y ejecutar un contenedor basado en otra distribución, tal como Fedora. Nota En general, crear un contenedor basado en tu distribución y otro basado en otra que no sea la tuya. Fedora, al parecer, tiene problemas si estás en Ubuntu 13.04 o superior, así que en tal caso usa cualquier otra distro.**

Mi intentción inicial fue instalar Centos, pero como he tenido problemas de dependencias, finalmente he instalado Cirros, que viene como template por defecto:

![img45](Capturas/imagen45.png)
