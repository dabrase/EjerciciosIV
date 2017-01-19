# Ejercicios del tema 5: Virtualización completa: uso de máquinas virtuales
### Ejercicio 1
**Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.**

Siguiendo [estas instrucciones](https://help.ubuntu.com/community/KVM/Installation) comprobamos que KVM está instalado y se puede usar la virtualización:

```bash
$ kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used
```
A continuación, siguiendo la [wiki de KMV](https://wiki.debian.org/KVM#Installation) instalo el paquete _qemu-kvm_ y otros necesarios:

```bash
sudo apt-get install kvm qemu-kvm libvirt-bin virtinst
```

**Atención**: un kernel antiguo puede provocar el bloqueo del sistema e imposibilitar el arranque tras instalar alguno de estos paquetes, por lo que se recomiendo actualizarlo siguiendo [estos pasos](http://askubuntu.com/questions/777627/what-is-the-lastest-stable-kernel-and-how-to-install-it).

A continuación, añadimos nuestro usuario a los grupos necesarios:
```bash
sudo adduser asus libvirtd
sudo adduser asus kvm
```

Y comprobamos que todo está correctamente instalado al no recibir un error tras ejecutar:
```bash
virsh list --all
 Id    Nombre                         Estado
----------------------------------------------------
```
### Ejercicio 2
#### Ejercicio 2.1
**Crear varias máquinas virtuales con algún sistema operativo libre tal como Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).**

Primero creamos el disco duro virtual para slitaz:
```bash
$ qemu-img create -f qcow2 mvirtuales/slitaz.qcow 200M
Formatting 'mvirtuales/slitaz.qcow', fmt=qcow2 size=209715200 encryption=off cluster_size=65536 lazy_refcounts=off refcount_bits=16
```
Y tras descargar Slitaz ejecutamos la máquina virtual con:
```bash
$ qemu-system-x86_64 -machine accel=kvm -hda mvirtuales/slitaz.qcow -cdrom ../Descargas/slitaz-5.0-rc3.iso -m 1G -boot once=d
```
Donde se indica la virtualización, la locaclización del disco duro virtual, la localización del archivo iso, la RAM asignada y el orden de arranque.

![imagen51](Capturas/imagen51.png)

De la misma forma, creamos otro disco duro virtual para Damn Small Linux:
```bash
$ qemu-img create -f qcow2 mvirtuales/small.qcow 200M
Formatting 'mvirtuales/small.qcow', fmt=qcow2 size=209715200 encryption=off cluster_size=65536 lazy_refcounts=off refcount_bits=16
```
Y ejecutamos:
![imagen52](Capturas/imagen52.png)

#### Ejercicio 2.2
**Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.**

Desde Virtualbox, hacemos click en _nueva_ y rellenamos los datos tal y como se muestra:

![imagen53](Capturas/imagen53.png)

Se asigna la ram:

![imagen54](Capturas/imagen54.png)

Si el sistema muestra que el driver de virtualbox no está funcionando correctamente, hay un sinfín de posiblidades, pero en mi caso me funcionó lo siguiente:
* Desisntalar dkms
* Desinstalar Virtualbox
* Instalar ambos siguiendo [esta guía](https://www.virtualbox.org/wiki/Linux_Downloads)

Se selecciona el archivo .iso:

![imagen55](Capturas/imagen55.png)

E inicia la máquina virtual:

![imagen56](Capturas/imagen56.png)

Siguiendo los mismos pasos arrancamos Slitaz:

![imagen57](Capturas/imagen57.png)

### Ejercicio 3
**Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img**

Instalo Slitaz y lo abro de la manera habitual:
```bash
qemu-system-x86_64 -machine accel=kvm -hda Documentos/mvirtuales/slitaz.qcow -m 1G
```
Y ejecuto un pequeño progama que he creado que escribe en disco (donde se quiere comprobar la mejora), arrojando este tiempo de ejecución:

![imagen58](Capturas/imagen58.png)

Cuando ejecuto la paravirtualización lamentablemente obtengo un _Kernel Panic_ y por más que he intentado arrancar la máquina no me ha sido posible:

![imagen60](Capturas/imagen60.png)

Pese a ello, he investigado un poco y por lo que parece, los beneficios de la paravirtualización dependen del programa a testear, y en aquellos en los que se realizan cálculos matemáticos, por ejemplo, puede no observarse mejora.

Intentaré hacerlo en otra distribución: Debian. Ejecuto sin paravirtualización:
```bash
qemu-system-x86_64 -boot order=c -drive file=debianlxde.img
```
Obteniendo estos resultados:

![imagen61](Capturas/imagen61.png)


Y la ejecución con paravirtualización:
```bash
qemu-system-x86_64 -boot order=c -drive file=debianlxde.img,if=virtio
```
Ofrece estos resultados:

![imagen62](Capturas/imagen62.png)

Por lo que experimentamos una leve mejora, alrededor de un 4%.

### Ejercicio 4
**Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.**

En primer lugar descargo [Debian netinstall](http://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-8.7.1-amd64-netinst.iso) y creo un disco duro virtual:
```bash
qemu-img create -f qcow2 debianlxde.img 9G
```
Y lanzamos la máquina por primera vez para realizar la instalación:
```bash
qemu-system-x86_64 -hda debianlxde.img -cdrom /home/asus/Descargas/debian-8.7.1-amd64-netinst.iso
```
Activamos la opción vnc:
```bash
qemu-system-x86_64 -vnc 0.0.0.0:1 -hda debianlxde.img
```
Y nos conectamos con vinagre:
```bash
vinagre 0.0.0.0:1
```

![imagen63](Capturas/imagen63.png)

Para el SSH lanzamos la máquina virtual como sigue:
```bash
qemu-system-x86_64 -hda debianlxde.img -m 512M -name jjdebian -redir tcp:2222::22
```
Y conectamos así:
```bash
ssh -p 2222 localhost
```
Así accedemos finalmente:

![imagen64](Capturas/imagen64.png)
