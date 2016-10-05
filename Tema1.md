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

### Ejercicio 3.2
**Crear un programa simple en cualquier lenguaje interpretado para Linux, empaquetarlo con CDE y probarlo en diferentes distribuciones.**

Creo un programa sencillo que imprime el contenido de un archivo llamado fichero.txt. Con el siguiente comando, lo empaqueto con CDE:

```bash
cde python ejemplo.py
```

En el paquete, podemos comprobar como CDE ha creado la ruta en la que se encontraba el script

```bash
cd cde-package/cde-root/home/asus/Descargas/
```

Y ha copiado _fichero.txt_ para su correcta ejecución:

```bash
ls
ejemplo.py  ejemplo.py.cde  fichero.txt  python.cde
```

Por lo que su ejecución es independiente de la distribución de Linux en la que se ejecute.


##Ejercicio 4
**Comprobar si el procesador o procesadores instalados tienen estos flags. ¿Qué modelo de procesador es? ¿Qué aparece como salida de esa orden?**

La salida es:
```
flags       : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch epb intel_pt tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt xsaveopt xsavec xgetbv1 dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp
```

repetido 4 veces, tantas como núcleos tiene el procesador. El modelo es un Intel Core i5-6300HQ.

IMAGEN 3

Tal y como se muestra en la imagen anterior, el procesador soporta la virtualización.

