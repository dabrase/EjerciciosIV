# Ejercicios del tema 1:Introducción a la infraestructura virtual

### Ejercicio 1
**Consultar en el catálogo de alguna tienda de informática el precio de un ordenador tipo servidor y calcular su coste de amortización a cuatro y siete años.**

Para este ejemplo voy a usar el servidor Lenovo ThinkServer TS140, que tiene un precio de venta de 723.04€ en [Amazon](https://www.amazon.es/Lenovo-ThinkServer-TS140-procesadores-E3-1226V3/dp/B00SSR7H30/ref=sr_1_15?ie=UTF8&qid=1475683161&sr=8-15&keywords=servidor). Como tiene el I.V.A. incluído, calculamos la base imponible, que es 597,52€.

Como se puede deducir un 25% de la base imponible anualmente, la amortización sería de 180,76€ al año, durante 4 años.

Si lo repartimos entre 7 años, el coste de amortización anual sería de 103,29€.

Estos cálculos están realizados suponiendo periodos anuales completos. Si se realizara la compra a mitad de año, la amortización sería la mitad del máximo anual, continuando al 25% durante los 2 años siguientes y volviendo a bajar a la mitad en el cuarto año.

### Ejercicio 2
**Usando las tablas de precios de servicios de alojamiento en Internet y de proveedores de servicios en la nube, Comparar el coste durante un año de un ordenador con un procesador estándar (escogerlo de forma que sea el mismo tipo de procesador en los dos vendedores) y con el resto de las características similares (tamaño de disco duro equivalente a transferencia de disco duro) en el caso de que la infraestructura comprada se usa sólo el 1% o el 10% del tiempo.**

Vamos a comparar un servidor dedicado de [Hostgator](http://www.hostgator.com/dedicated-server) con el web services de [Amazon](https://aws.amazon.com/es/ec2/pricing/) con características similares: CPU de 2 núcleos y 4GB de RAM.

IMAGEN1

En el servidor dedicado, el precio es de 79$ al mes, alrededor de 70.55€.

IMAGEN2

En servidor cloud de Amazon, usando la opción *t2.medium* el coste es de 0.06$ por hora, lo que serían 0.053€.

Para un uso del **10%**:
* Servidor dedicado: 70.55€/mes x 12 meses = 846.60€ (precio fijo independiente de su uso)
* Servidor cloud: 10% de las horas de 1 año: 876 x 0.053€/hora = 42.43€

Para un uso del **1%**:
* Servidor dedicado: 70.55€/mes x 12 meses = 846.60€ (precio fijo independiente de su uso)
* Servidor cloud: 1% de las horas de 1 año: 87,6 x 0.053€/hora = 4.64€

Se obtiene como conclusión que para las situaciones propuestas, el servidor cloud realiza el mismo servicio con un coste mucho menor.

###Ejercicio 3.1
**¿Qué tipo de virtualización usarías en cada caso? Comentar en el foro**

[Comentario en el foro](https://github.com/JJ/IV16-17/issues/1#issuecomment-251745834)

