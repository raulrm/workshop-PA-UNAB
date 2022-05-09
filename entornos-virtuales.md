# Entornos virtuales

## El problema (O los problemas)
Python es un lenguaje al que contribuyen muchas personas y empresas. Eso lo hace un "objetivo móvil" porque continuamente se lo esta revisando, corrigiéndosele errores y, sobre todo, incorporándosele nuevas posibilidades.  
Y lo mismo ocurre con todas las librerías externas que podríamos estar usando.
Esto hace que que tenga varias revisiones anuales. Evidenciadas por el numero de version del lenguaje. 
Entonces cuando tenemos proyectos grandes o medianos que llevan años de desarrollo pueden surgir incompatibilidades o bugs si no conservamos un control de la version de Python o de las librerías externas que empleamos en el proyecto.  
Ademas puede ocurrir que un programador esté trabajando en distintos proyectos a la vez, en la misma computadora. Y que estos proyectos requieran diferentes versiones del lenguaje y/o librerías.   
Un problema adicional con el que nos encontramos es que la ubicuidad de Python hace que sea empleado para desarrollar aplicaciones del propio sistema operativo. Asi nos encontraríamos que luego de actualizar la version de Python nos deje de funcionar la aplicación que nos permite conectarnos a las redes wifi.

## La solución
En estas condiciones, lo ideal seria tener una computadora distinta configurada para cada proyecto. Pero eso sigue sin resolver el problema del uso de Python en el sistema operativo.  
Lo mismo ocurriría si empleáramos maquinas virtuales.  
El uso de contenedores (Docker o ContainerD) seria una solución mucho mas eficaz. Y ademas tendríamos otras ventajas, es por eso que prácticamente se esta convirtiendo en el estándar del desarrollo de software. Aunque requiere de ciertos conocimientos previos para su correcta implementación.
Pero existe una solución mas sencilla que esta al alcance de todos, el empleo de *Entornos Virtuales*  
Con ligeras diferencias, la idea detras de ese concepto es la de tener una consola de comandos especial en la que cada vez que llamamos a un programa PRIMERO se ejecute NUESTRA version elegida de ese programa.  
Asi si nuestra version de Python instalada en el sistema operativo es la 2.7, cuando activemos el entorno virtual y en el hayamos instalado la version 3.9 la que ejecutaremos al escribir el comando "python" sera a la ultima.  
Cualquier otro programa que no hayamos instalado en el entorno virtual sera ejecutado en la version que ya tenga el sistema.  

## Paqueteria
Como ya habremos notado tenemos que tener un sistema para instalar Python o sus librerías en la version que deseemos. Tanto dentro de un entorno virtual como fuera de él.   
Si bien esto puede hacerse manualmente descargando el código fuente y realizando las modificaciones correspondientes para cada sistema operativo que estemos usando (Windows, Linux o MacOS -en sus distintas versiones- ) el ecosistema Python tiene su herramienta preferida.
Esta es pip.  
Pip nos permite instalar, actualizar y remover cualquier librería o incluso el mismo Python.  
Estas librerías generalmente vienen de a varias y en varios archivos, por eso se las denomima **paquetes**. Existen varios repositorios de esos paquetes en la red, pero pip por defecto las descarga del repositorio principal.    
Estas librerías se pueden instalar usando las herramientas incorporadas a nuestro IDE de desarrollo pero es una practica común (y muy conveniente) realizar todas estas operaciones usando la **linea de comandos**. Tanto la propia de nuestro sistema operativo como la que nos provea el IDE.  
Por ejemplo, si quisiéramos instalar la librería de computación numérica "numpy" (que no viene instalada por defecto) deberíamos escribir:   

`pip install numpy`  

Si nos interesara remover esa librería el comando seria:  

`pip remove numpy`   

Si quisiéramos instalar una version especifica de numpy deberemos escribir:  

`pip install numpy==1.22.1`   


Pip tiene muchas opciones mas. Aquí tenemos un [Machete de PIP](https://opensource.com/sites/default/files/gated-content/cheat_sheet_pip.pdf) (en ingles)  
Una característica de pip increíblemente util es la de permitirnos la exportación de la paquetería usada en un proyecto mediante la generación de un archivo donde estan listados todos los paquetes usados en el proyecto con sus versiones especificas.  
Este archivo se suele llamar **requeriments.txt** (aunque puede tener cualquier nombre) y se genera mediante el comando:  

`pip freeze > requeriments.txt`  

Vamos a ver que es muy frecuente encontrar ese archivo en los repositorios de código del tipo git.  
Para reconstruir localmente una paquetería a partir de ese archivo debemos hacer:  

`pip install -r requeriments.txt`  

Vamos a usar mucho pip para administrar la paquetería, asi que debemos acostumbrarnos a sus uso. Y también es la herramienta que emplearemos para instalar los entornos virtuales.  
No podemos dejar de mencionar que en todo proyecto de software que se apoya en el uso de librerias que a su vez requieren de otras librerías pueden y van a surgir incompatibilidades entre ellas. A esto se lo llama **"pesadilla de dependencias"**  
Y es algo que debemos tener en cuenta incluso en proyectos pequeños.

## Las opciones  
Los EV son la forma mas practica de aislar el desarrollo de aplicaciones, necesitemo o no tener versiones separadas de lenguaje y librerías. Es por ello que surgieron muchas diferentes soluciones similares. Entonces elegir la mejor se basa en el gusto, la costumbre o el soporte que tenga cada uno de ellos.  
Recordemos que mayormente los entornos virtuales se trabajan en modo consola. Los entornos graficos se apoyan en la infraestructura creada por los EV pero sigue siendo una operacion que se realiza en el shell del sistema operativo.  
Es por eso que casi todos suelen modificar de alguna forma el **prompt** de la linea de comando insicandonos que estamos dentro d eun EV. Lo mas comun es que nos agreguen el nombre del entorno entre corchetes antes de el cursor.  
Cuando no estamos dentro de un entorno creado por nosotros, se suele indicar que se halla en el entorno BASE (base) en donde se ejecutan los programas y la version de Python que viene por defecto con el sistema operativo.    
Entre los mas conocidos EV podemos nombrar:   
+ virtualenv
+ pipenv
+ conda 
+ venv (Entorno "oficial" de Python)
+ Poetry  

Y existen cientos mas. Pero por cantidad de usuarios se destacan virtualenv y Conda. Poetry es una solución mas moderna que incorpora también el manejo de paquetes y la creación automática de entornos y su uso esta creciendo fuerte.  
En este articulo hablaremos en detalle de los siguientes EV:  

## Opcion 1

[Virtualenv](https://virtualenv.pypa.io/en/stable/) es una herramienta que se utiliza para crear entornos Python aislados. Crea una carpeta que contiene todos los ejecutables necesarios para usar los paquetes que necesitaría un proyecto de Python.

### Crear entorno

Para crear un entorno usando virtualenv ejecutamos el comando:  

 `pip install virtualenv`

 La instalación se verifica con el siguiente comando:

  `virtualenv --version`


### Administrar paquetes

Se utiliza el sistema standard de pip

### Administrar entornos

Para crear un entorno virtual utilizamos:

 `virtualenv --no-site-packages my-env`

Esto crea una carpeta en el directorio actual con el nombre del entorno (my-env/). 
Esta carpeta contiene los directorios para instalar módulos y ejecutables de Python.

También podemos especificar la versión de Python con la que quieres trabajar. Simplemente usamos el argumento:
--python=/ruta/a/la/version/de/python. 

Por ejemplo para python2.7:

 `virtualenv --python=/usr/bin/python2.7 my-env`

Podemos enumerar los entornos disponibles con:

 `lsvirtualenv`
 

Antes de utilizar el entorno, tenemos que activarlo:

 `source my-env/bin/activate`

 Esto asegura que solo se usen los paquetes bajo `my-env/.`

Vamos a ver que el nombre del entorno se muestra a la izquierda de la línea de comandos. De esta forma podemos ver cuál es el entorno activo.


## Opcion 2
[Pipenv](https://pipenv-es.readthedocs.io/es/latest/) es un manejador de entornos virtuales que pretende unificar las acciones de instalacion de paquetes y de creacion de entornos mediante una sola herramienta.  
Tiene sus propios archivos de listado de paquetes y de control de versiones, asi que deja de ser compatible con el uso del archivo **requeriments.txt**
Por otro lado su desarrollo se ha estancado desde que se hizo oficial el uso de venv en Python.  

Para instalarlos ejecutamos:  
`pip install pipenv`  

### Crear entorno  
Para crear un entorno con pipenv debemos ejecutar:  
`pipenv shell`  

Esto nos disparara un EV donde funcionan los programas por defecto del sistema operativo, a menos que exista en el directorio actual un archivo Pipfile.lock.  
De ser asi se creara el entorno con las versiones de los programas allí listados.

### Administrar paquetes
Una vez que tengamos en ejecucion el shell podemos instalar paquetes y sus versiones con:  
`pipenv install paquete==version`  

Una vez que tengmos todos los paquetes instalados podemos congelar la paqueteria haciendo que el archivo de configuracion se actualice mediante el comando: 
`pipenv lock`  

### Administrar entornos  
Pipenv mantiene una lista de entornos creados, para ver donde se alla esa lista ejecutamos:  
`pipenv --venv`  
De esa forma podremos ver donde están todos los archivos --Pipfile-- que son los que representan los entornos.  
Para eliminar un entorno ejecutamos:  
`pipenv --rm`  
Pipenv tiene muchas otras funciones para conocerlas, como siempre, es preferible leer la documentacion oficial.


## Opcion 3
[conda](https://docs.conda.io/projects/conda/en/latest/index.html) es un sistema completo de instalación de paquetes y aplicaciones para muchos lenguajes y librerias que incluyen tambien a Python.  
Es parte importante del proyecto [Anaconda](https://anaconda.org/) orientado a proveer de un entorno de desarrollo completo para Ciencia de Datos.  
La forma mas sencilla de instalarlo es empleando la version [miniconda](https://docs.conda.io/en/latest/miniconda.html)
### Crear entorno  
Para crear un entorno con el nombre **nombre-entorno** debemos ejecutar:  
`conda create --name nombre-entorno `  

Para activarlo:  
`conda activate nombre-entorno`  

Para salir de un entorno:  
`conda deactivate`

### Administrar paquetes
Conda nos permite usar pip dentro de cada entorno pero tambien tiene su propio método de instalación y actualización de paquetes empleando su propio repositorio.  
Para instalar un paquete en una version especifica debemos ejecutar:  
`conda install paquete=version`  

Para remover un paquete:  
`conda remove paquete`  

Para actualizar un paquete:  
`conda update paquete`
### Administrar entornos

Para ver cuales entornos ya tenemos creados:  
`conda env list`

Para ver que paquetes y versiones están instalados en le entorno activo:  
`conda list`  

Para borrar un entorno existente:  
`conda env remove --name nombre-entorno`

Para actualizar la version de conda:  
`conda update conda`

Para ver informacion de conda:  
`conda info`

Podemos revisar este [Machete de Conda](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf) para mas opciones.  

## Conclusion  
Como no podemos estar cambiando continuamente la version de Python que viene con nuestro sistema operativo para adaptarla a la version que necesitamos para llevar adelante nuestro desarrollo y tampoco podemos llevar constancia de que version de cada libreria estamos usando el empleo de entornos virtuales es prácticamente obligatorio para la programación en Python.  
Asi que cuanto antes incorporemos como habito el de disparar el entorno virtual de nuestra preferencia **antes** de ponernos a editar código, mejores seremos como programadores.  
Siempre teniendo en cuenta que no hay forma sencilla de corregir la **pesadilla del versionado**. Solo se puede mitigar siendo muy consientes de que librerías estamos usando.
