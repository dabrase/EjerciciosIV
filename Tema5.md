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

### Ejercicio 2
**Crear una receta para instalar la aplicación que se viene creando en la asignatura en alguna máquina virtual o servidor en la nube.**

Para probar Chef-solo de una manera rápida voy a realizar la instalación de _nano_ y _emacs_. En primer lugar creo los siguientes directorios desde /home:

```bash
sudo mkdir -p chef/cookbooks/nano/recipes
sudo mkdir -p chef/cookbooks/emacs/recipes
```

En cada uno de estos directorios vamos a crear un archivo _default.rb_ que contendrá cada una de las recetas, que consistirán en instalar el paquete y crear un directorio.

default.rb para nano:

```json
package 'nano'
directory "/home/asus/Documentos/nano"
file "/home/asus/Documentos/nano/readme" do
    owner "asus"
    group "asus"
    mode 00544
    action :create
    content "Directorio para nano"
end
```

default.rb para emacs:
