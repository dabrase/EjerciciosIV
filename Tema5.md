# Ejercicios del tema 5: Gestión de infraestructuras virtuales
### Ejercicio 1
**Instalar chef en la máquina virtual que vayamos a usar**

Instalamos Chef como indica [la documentación](http://gettingstartedwithchef.com/first-steps-with-chef.html) con:
```bash
curl -L https://www.opscode.com/chef/install.sh | sudo bash
```
Comprobamos que la instalación es correcta:
```bash
$ chef-solo -v
Chef: 12.17.44
```
