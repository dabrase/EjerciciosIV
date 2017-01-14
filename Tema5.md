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

Para probar Chef-solo de una manera rápida voy a realizar la instalación la aplicación que he desarrollado para pruebas en la asignatura en Nodejs. En primer lugar creo el siguiente directorio desde /home:

```bash
sudo mkdir -p chef/cookbooks/comparadorempresas/recipes
```

En el directorio creo _default.rb_ que contendrá la receta de instalación:
```ruby
git "/home/asus/Documentos/empresas" do
  repository "https://github.com/juanjetomas/Nodejs-Sample.git"
  reference "master"
  action :sync
  user "asus"
end

package "nodejs"

execute "npm-install" do
  cwd "home/asus/Documentos/empresas"
  command "npm install"
  user "asus"
  group "sudo"
  action :run
end
```

Clona el respositorio en la carpeta _empresas_, se instala _nodejs_ y se instalan los requisitos incluidos en el _package.json_.

En la carpeta _chef_ creo el documento _node.json_ donde se enumeran las recetas, en este caso una sola:

```json
{
	"run_list": [ "recipe[comparadorempresas]" ]
}
```

A continuación he creado el archivo _solo.rb_ en mi directorio _HOME_ con el siguiente contenido:
```ruby
file_cache_path "/home/chef"
cookbook_path "/home/chef/cookbooks"
json_attribs "/home/chef/node.json"
```

Lanzamos la receta con:
```bash
sudo chef-solo -c solo.rb
```

![imagen49](Capturas/imagen49.png)

Y ya estaría instalado todo lo necesario para ejecutar la aplicación:
```bash
node app.js
```

### Ejercicio 4
**Instalar una máquina virtual Debian usando Vagrant y conectar con ella.**

Primero instalamos Vagrant:
```bash
sudo apt-get install vagrant
```

Y añadimos una imagen de Debian:
```bash
vagrant box add debian http://static.gender-api.com/debian-8-jessie-rc2-x64-slim.box
```

La iniciamos:
```bash
vagrant init debian
```

Y se crea un archivo _Vagrantfile_.

Instalamos Virtualbox:

```bash
sudo apt-get install virtualbox virtualbox-dkms
```

Levantamos la máquina con:
```bash
vagrant up
```

Y podemos conectarnos por ssh (introduciendo _vagrant_ como contraseña):

![imagen50](Capturas/imagen50.png)
