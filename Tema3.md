# Ejercicios del tema 3: Creando aplicaciones en la nube: Uso de PaaS
### Ejercicio 1
**Darse de alta en algún servicio PaaS tal como Heroku, Nodejitsu, BlueMix u OpenShift.**

En primer lugar me he registrado en Heroku:
![img23](Capturas/imagen23.png)

A continuación me he registrado en Openshift, ya que se requiere para el ejercicio 2:

![img24](Capturas/imagen24.png)

### Ejercicio 2
**Crear una aplicación en OpenShift y dentro de ella instalar WordPress.**

Accedemos a [esta página](https://openshift.redhat.com/app/console/applications) y clickamos en _create your first application now_:

_Nota: he usado el proceso de recuperación de contraseña de Openshift para poder acceder a este panel, ya que el disponible por defecto al registrarse en la web principal (con GitHub) no me ha funcionado idénticamente al tutorial usado_

![img25](Capturas/imagen25.png)

Tras consultar [este tutorial de Wordpress en Openshift](https://github.com/openshift/wordpress-example), seleccionamos una aplicación PHP 5.4 y Wordpress y rellenamos tal y como se indica:

![img26](Capturas/imagen26.png)

Tras iniciar la creación de la aplicación, obtenemos esto:

![img27](Capturas/imagen27.png)

y podemos acceder a la inicialización del Wordpress visitando: http://wordpress-juanjetomas.rhcloud.com/

![img28](Capturas/imagen28.png)

![img29](Capturas/imagen29.png)

### Ejercicio 3
**Realizar una app en express (o el lenguaje y marco elegido) que incluya variables como en el caso anterior.**

Como primer paso, he añadido funciones REST (GET y PUT) a aplicación desarrollada con node.js + express ejercicios anteriores. Se encuentra en [este repositorio](https://github.com/juanjetomas/Nodejs-Sample).

Tras esto, si visitamos la dirección _/companies_ definida en el GET, obtenemos un JSON con la información almacenada hasta el momento:

![img30](Capturas/imagen30.png)

A continuación, podemos hacer una inserción mediante:
```bash
curl -X PUT localhost:3000/addcomment/Pademobile/Excelente
```
Y obtenemos en terminal la lista actualizada de comentarios:

![img31](Capturas/imagen31.png)

Si se vuelve a visitar la dirección _/companies_ se comprueba que se han reflejado los cambios.
