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
