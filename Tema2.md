Do  # Ejercicios del tema 2: Desarrollo basado en pruebas
### Ejercicio 1
**Instalar alguno de los entornos virtuales de node.js (o de cualquier otro lenguaje con el que se esté familiarizado) y, con ellos, instalar la última versión existente, la versión minor más actual de la 4.x y lo mismo para la 0.11 o alguna impar (de desarrollo).**

Instalamos nvm mediante:
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
```
Tras reiniciar el terminal, comprobamos que nvm se ha instalado correctametne mediante:
```bash
command -v nvm
```
Instalamos la última versión:
```bash
nvm install node
######################################################################## 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v6.8.1 (npm v3.10.8)
Creating default alias: default -> node (-> v6.8.1)
```
De igual forma se instala la versión de desarrollo:
```bash
nvm install v0.11
######################################################################## 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v0.11.16 (npm v2.3.0)
```
Para hacer el cambio entre versiones se usa el comando _nvm use version-a-usar_ como por ejemplo:
```bash
nvm use v6.8.1
```

![img4](Capturas/imagen4.png)

### Ejercicio 2
**Como ejercicio, algo ligeramente diferente: una web para calificar las empresas en las que hacen prácticas los alumnos.
Crear un repositorio en GitHub para la librería y crear un pequeño programa que use algunas de sus funcionalidades.
Si se quiere hacer con cualquier otra aplicación, también es válido. Se trata de hacer una aplicación simple que se pueda hacer rápidamente con un generador de aplicaciones como los que incluyen diferentes marcos MVC. Si cuesta mucho trabajo, simplemente prepara una aplicación que puedas usar más adelante en el resto de los ejercicios.**

Voy a seguir un tutorial de node.js, express y jquery del [blog Koalite](http://blog.koalite.com/2011/11/tutorial-node-js-express-jquery-i-creando-la-aplicacion/).

Los pasos que he tenido que seguir que no aparecen en el tutorial son los siguientes:
* Tras la instalación de express, para obtener el generador usar:
```bash
npm install express-generator
```
* Una vez creado el proyecto express, ejecutar el siguiente comando para instalar las dependencias necesarias antes de lanzar la aplicación:
```bash
cd . && npm install
```
* La primera línea del archivo _index.jade_ debe ser _doctype html_ en lugar de _doctype 5_.

A punto de terminal el tutorial, las incongruencias entre el código autogenerado por express 4 y el de ejemplo del tutorial (que se basa en la versión 3) han hecho casi imposible finalizarlo, por lo que he hecho un fork y rehecho los pasos anteriores. [Enlace al repositorio](https://github.com/juanjetomas/Nodejs-Sample)

Ejecutamos la aplicación:

![img5](Capturas/imagen5.png)

Y en http://localhost:3000/ encontramos:

![img6](Capturas/imagen6.png)

### Ejercicio 3
**Ejecutar el programa en diferentes versiones del lenguaje. ¿Funciona en todas ellas?**

![img7](Capturas/imagen7.png)

![img8](Capturas/imagen8.png)

Tal y como se ve en las 2 imágenes anteriores el programa funciona tanto en la versión v.6.8.1 como en la v0.11.16.

### Ejercicio 4
**Crear una descripción del módulo usando package.json.**

He generado el package.json mediante el comando:
```bash
npm init
```
Obteniendo como resultado:
```javascript
{
  "name": "calificador-empresas-node",
  "version": "1.0.0",
  "description": "Permite la calificacion de empresas de practicas icaro",
  "main": "app.js",
  "dependencies": {
    "express": "^3.0.0rc3",
    "jade": "^0.27.2",
    "underscore": "^1.3.3"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/juanjetomas/Nodejs-Sample.git"
  },
  "author": "Juan Jesus Tomas Rojas",
  "license": "GPL-3.0",
  "bugs": {
    "url": "https://github.com/juanjetomas/Nodejs-Sample/issues"
  },
  "homepage": "https://github.com/juanjetomas/Nodejs-Sample#readme"
}
```

### Ejercicio 5
**Automatizar con grunt y docco (o algún otro sistema) la generación de documentación de la librería que se cree. Previamente, por supuesto, habrá que documentar tal librería.**

Para poder instalar grunt globalmente (y usando sudo) en primer lugar ejecutamos:
```bash
sudo apt-get install npm
```
Y a continuación instalamos grunt de manera global:

![img10](Capturas/imagen10.png)

Pese al paso anterior recibía un aviso al instalar docco de que grunt no estaba instalado, quedando resuelto al usar:
```bash
npm install -g grunt-cli
```
A continuación he instalado docco:

![img11](Capturas/imagen11.png)

Y esto queda reflejado en el _package.json_:

![img12](Capturas/imagen12.png)

A continuación creamos el archivo _Gruntfile.js_ con la siguient estructura:
```json
'use strict';

module.exports = function(grunt) {

  // Configuración del proyecto
  grunt.initConfig({
  pkg: grunt.file.readJSON('package.json'),
  docco: {
	  debug: {
	  src: ['*.js'],
	  options: {
		  output: 'docs/'
	  }
	  }
  }
  });

  // Carga el plugin de grunt para hacer esto
  grunt.loadNpmTasks('grunt-docco');

  // Tarea por omisión: generar la documentación
  grunt.registerTask('default', ['docco']);
};
```

Y finalmente generamos la documentación:

![img13](Capturas/imagen13.png)

Éste es el archivo _Gruntfile.html_ por ejemplo:

![img14](Capturas/imagen14.png)

### Ejercicio 6
**Para la aplicación que se está haciendo, escribir una serie de aserciones y probar que efectivamente no fallan. Añadir tests para una nueva funcionalidad, probar que falla y escribir el código para que no lo haga (vamos, lo que viene siendo TDD).**

He añadido varios asserts en el archivo _index.js_ en los que compruebo la correcta lectura de variables y algunas condiciones.
```json
exports.index = function(req, res) {
  var names = companies.map(function(p) { return p.name; });
  assert(names, "Colección de nombres de empresas");
  res.render('index', { companies: names })
};

exports.company = function(req, res) {
  var comments = _(companies).detect(function (p) {
    return p.name == req.params.name;
  }).comments;
  assert(comments.length!=0, "Si no hay comentarios se debe mostrar un mensaje invitando a añadirlos.")
  res.json(comments);
}

exports.addComment = function(req, res) {
  var company = _(companies).detect(function(p) {
    return p.name == req.body.name;
  });

  var numComments = company.comments.length;
  company.comments.push(req.body.comment);
  assert(numComments+1 === company.comments.length, "El comentario no se ha añadido correctamente");

  console.log('Nuevo comentario para ' + company.name + ': ' + req.body.comment);

  res.json({status: 'ok' });
}
```
Y podemos comprar que hay un test que falla:

![img15](Capturas/imagen15.png)

Ocurre porque no mostramos un mensaje invitando al usuario a añadir su valoración de la empresa que aún no tiene. Tras modificar el código comprobamos que el test ya no falla:

![img16](Capturas/imagen16.png)

### Ejercicio 7
**Convertir los tests unitarios anteriores con assert a programas de test y ejecutarlos desde mocha, usando descripciones del test y del grupo de test de forma correcta.**

Instalamos mocha globalmente con:
```bash
sudo npm install -g mocha
```
Y dentro de la carpeta _tests_ creamos un archivo _tests.js_ con el siguiente contenido:
```json
var assert = require("assert");
empresas = require(__dirname+"/../app.js");

describe('Empresas', function(){
    describe('Carga', function(){
        it('Carga el fichero app.js', function(){
            assert(empresas, "Correcto");
        });
    });
});
```
Que simplemente comprueba que se carga correctamente el fichero _app.js_. Tras esto, ejecutamos los test:

![img17](Capturas/imagen17.png)

Y comprobamos que los test (en este caso, uno) han sido válidos.

### Ejercicio 8
**Darse de alta. Muchos están conectados con GitHub por lo que puedes autentificarte directamente desde ahí. A través de un proceso de autorización, puedes acceder al contenido e incluso informar del resultado de los tests a GitHub.**


**Activar el repositorio en el que se vaya a aplicar la integración continua. Travis permite hacerlo directamente desde tu configuración; en otros se dan de alta desde la web de GitHub.**


**Crear un fichero de configuración para que se ejecute la integración y añadirlo al repositorio.**
