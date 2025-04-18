# Contenedores en red y Docker Desktop

> **Documento realizado por Roberto Delgado Sánchez - Alumno de Despliegue de Aplicaciones Web - DAW**

[TOC]

## 1. Enunciado

En este ejercicio vamos a crear dos contenedores, uno a partir de una imagen de **mariaDB** y otro a partir de una imagen de **Adminer** o **phpMyAdmin** (hay que elegir una). El objetivo final es conectar ambos contenedores en red y acceder desde el segundo al primero.

Es obligatorio el empleo de **Docker** **Desktop** para la resolución del ejercicio, así como la instalación de un par de extensiones (**PortNavigator** y **Disk** **Usage**) en dicha aplicación. Se incluirán en esta documentación capturas de pantalla y los datos que se consideren oportunos respecto al proceso seguido.

## 2. Creación de la red bridge

El primer paso es entrar en **Docker** **Desktop** e instalar la extensión **PortNavigator**, que usaremos para crear y gestionar redes:

<img src="./ejercicio1.assets/image-20250417101633606.png" alt="image-20250417101633606" style="zoom:80%;" />

Una vez instalada nos aparecerá su icono:

<img src="./ejercicio1.assets/image-20250417101800716.png" alt="image-20250417101800716" style="zoom: 50%;" />

Y si hacemos clic en el mismo accederemos al menú de configuración de redes, donde podemos ver las redes que **Docker** tiene creadas por defecto:

<img src="./ejercicio1.assets/image-20250417101856297.png" alt="image-20250417101856297" style="zoom:50%;" />

Para crear una red hacemos clic en el botón **Add Network** y rellenamos los parámetros necesarios (sólo se nos indica el nombre de la red, que debe ser `redej1`):

<img src="./ejercicio1.assets/image-20250417102148980.png" alt="image-20250417102148980" style="zoom:50%;border:1px solid black;" />

Los parámetros de la red que hemos creado (nombre, tipo de red, puerta de enlace y dirección de red) son los siguientes:

<img src="./ejercicio1.assets/image-20250417102502793.png" alt="image-20250417102502793" style="zoom:50%;" />

Ya tenemos creada la red.

## 3. Creación de un contenedor con imagen de mariaDB

Para crear un contenedor a partir de una imagen basada en **mariaDB**, lo primero que tenemos que hacer es buscar una imagen oficial de **mariaDB** en **Docker** **Desktop**, usando para ello el buscador y descargándola con el botón **Pull**:

<img src="./ejercicio1.assets/image-20250417103004888.png" alt="image-20250417103004888" style="zoom:80%;" />

Una vez descargada la imagen, la tendremos disponible en el listado de imágenes. Para crear el contenedor sólo tenemos que hacer clic en el icono con forma de triángulo marcado en verde en la imagen siguiente, que es el equivalente al comando `docker run` de la línea de comandos:

<img src="./ejercicio1.assets/image-20250417103307157.png" alt="image-20250417103307157" style="zoom:80%;" />

Cuando pulsamos dicho botón, nos aparece una ventana en la que podemos configurar diversos parámetros de nuestro contenedor. Aquí tenemos que incluir los datos aportados por el enunciado del ejercicio:

- **nombre del contenedor**: no se especifica ninguno, así que uso una combinación del nombre de la imagen, mi nombre de usuario en **educastur** y el número de ejercicio.
- **puerto**: debe ser accesible desde el puerto 3306.
- **variables de entorno**: según la documentación de la imagen de **mariaDB**, cuando creamos un contenedor a partir de la misma podemos definir diversos parámetros mediante este tipo de variables, como por ejemplo la contraseña del usuario root (`MARIADB_ROOT_PASSWORD`), crear un usuario (`MARIADB_USER`), su contraseña (`MARIADB_PASSWORD`) y una base de datos por defecto (`MARIADB_DATABASE`), que en nuestro caso debe llamarse `DAW`. El resto de datos se escogen al azar, siendo el usuario una combinación de mi nombre y apellidos. 

Estas opciones quedan tal y como se puede ver en la siguiente imagen:

<img src="./ejercicio1.assets/image-20250417103805901.png" alt="image-20250417103805901" style="zoom: 50%;" />

Al hacer clic en el botón **Run** se crea el contenedor (en la siguiente imagen se puede ver parte del log donde se recoge el proceso de instalación y se pueden ver cosas como el nombre del contenedor o la creación del usuario y de la base de datos por defecto):

<img src="./ejercicio1.assets/image-20250417105122710.png" alt="image-20250417105122710" style="zoom:80%;border:1px solid black;" />

Ahí tenemos nuestro contenedor creado y en funcionamiento:

![image-20250417105347880](./ejercicio1.assets/image-20250417105347880.png)

Sólo quedaría pendiente conectar el contenedor que acabamos de crear a la red `redej1`. Para ello, tenemos en primer lugar que desconectar el contenedor de la red bridge que **Docker** crea por defecto, y después conectarlo a nuestra red `redej1`. Los pasos se pueden ver a continuación:

<img src="./ejercicio1.assets/image-20250417105730710.png" alt="image-20250417105730710" style="zoom: 50%;" />

Al desconectarlo, queda asignado automáticamente a una red sin nombre, desde la cual lo podemos conectar a la red que hemos creado `redej1`:

![image-20250417114001083](./ejercicio1.assets/image-20250417114001083.png)

<img src="./ejercicio1.assets/image-20250417110030569.png" alt="image-20250417110030569" style="zoom:50%;border:1px solid black;" />

![image-20250417110615612](./ejercicio1.assets/image-20250417110615612.png)

![image-20250417110707295](./ejercicio1.assets/image-20250417110707295.png)

Ya tenemos creado el contenedor basado en la imagen de **mariaDB**. Ahora hay que generar un script **SQL** que cree una tabla de nombre módulos con algunos registros, como los nombres de las asignaturas en las que estoy matriculado:

```sql
CREATE TABLE modulos
(
	id INT AUTO_INCREMENT PRIMARY KEY,
	nombreAsignatura VARCHAR(60) NOT NULL
);

INSERT INTO modulos (nombreAsignatura) VALUES
('bases de datos'),
('programación'),
('interfaces'),
('despliegue'),
('cliente'),
('servidor');
```

De momento lo dejamos así, ya que este script se usará más adelante.

## 4. Creación de un contenedor con Adminer o phpMyAdmin

De las dos opciones que se nos dan escogemos **Adminer** para crear otro contenedor. Los pasos son similares a los que seguimos para crear el contenedor basado en **mariaDB**, por lo que mostraremos las capturas de pantalla del proceso haciendo sólo hincapié en aquello que sea diferente:

<img src="./ejercicio1.assets/image-20250417113142736.png" alt="image-20250417113142736" style="zoom:80%;" />

<img src="./ejercicio1.assets/image-20250417113310811.png" alt="image-20250417113310811" style="zoom:80%;" />

<img src="./ejercicio1.assets/image-20250417154146705.png" alt="image-20250417154146705" style="zoom:50%;" />

<img src="./ejercicio1.assets/image-20250417154258000.png" alt="image-20250417154258000" style="zoom:67%;" />

Nuestros dos contenedores ya están en marcha:

![image-20250417154352054](./ejercicio1.assets/image-20250417154352054.png)

Metemos al contenedor creado con la imagen de **Adminer** en la red `redej1`:

<img src="./ejercicio1.assets/image-20250417113904794.png" alt="image-20250417113904794" style="zoom:67%;" />

Al desconectarlo, queda asignado automáticamente a una red sin nombre, desde la cual lo podemos conectar a la red que hemos creado `redej1`:

![image-20250417114001083](./ejercicio1.assets/image-20250417114001083.png)

<img src="./ejercicio1.assets/image-20250417114216684.png" alt="image-20250417114216684" style="zoom:50%;border:1px solid black;" />

Ya tenemos a ambos contenedores conectados a nuestra red `redej1`:

![image-20250417154653775](./ejercicio1.assets/image-20250417154653775.png)

## 5. Comprobación de la conexión entre ambos contenedores

Una vez que sabemos la dirección IP de cada contenedor, podemos comprobar si se puede hacer un `ping` de `adminer` a`mariadb`:

<img src="./ejercicio1.assets/image-20250417154742745.png" alt="image-20250417154742745" style="zoom:50%;" />

El resultado es correcto, así que vamos a conectarnos ahora sí a la interfaz gráfica de `adminer_egl33817_ej1` a través del navegador:

<img src="./ejercicio1.assets/image-20250417154923366.png" alt="image-20250417154923366" style="zoom: 50%;" />

Ponemos los datos de conexión que definimos al crear el contenedor `mariadb_egl33817_ej1`:

<img src="./ejercicio1.assets/image-20250417155120107.png" alt="image-20250417155120107" style="zoom:50%;" />

Una vez dentro se nos muestra la pantalla principal:

<img src="./ejercicio1.assets/image-20250417155247736.png" alt="image-20250417155247736" style="zoom: 50%;border:1px solid black;" />

Vamos a ejecutar ahora el script **SQL** que generamos anteriormente. Para ello vamos a la opción **Comando SQL** del menú:

<img src="./ejercicio1.assets/image-20250417160630637.png" alt="image-20250417160630637" style="zoom:80%;border:1px solid black;" />

Las sentencias SQL se han ejecutado correctamente:

<img src="./ejercicio1.assets/image-20250417160826953.png" alt="image-20250417160826953" style="zoom:80%;border:1px solid black;" />

Comprobamos que, efectivamente, ahora tenemos una tabla `modulos` en la base de datos `DAW` que contiene los datos aportados anteriormente:

<img src="./ejercicio1.assets/image-20250417161012970.png" alt="image-20250417161012970" style="zoom:67%;border:1px solid black;" />

Y así completamos la realización de este apartado del ejercicio.

## 6. Instalación de Disk Usage

Vamos a instalar la extensión **Disk Usage**, que es equivalente al comando `docker system df`, es decir, da información sobre el espacio ocupado, etc. La buscamos desde el gestor de extensiones y la instalamos:

<img src="./ejercicio1.assets/image-20250417161759643.png" alt="image-20250417161759643" style="zoom:80%;" />

Una vez instalada, podemos ver cuánto espacio ocupan las imágenes, contenedores, etc.:

![image-20250417162424201](./ejercicio1.assets/image-20250417162424201.png)

## 7. Borrado de los contenedores y red creados

Como nos piden borrar los contenedores y la red creados (no hemos creado ningún volumen), los eliminaremos de uno en uno para ir viendo el efecto de ese borrado en el espacio utilizado (el borrado se gestiona con los botones con forma de papelera que aparecen en el apartado **acciones** de cada contenedor):

![image-20250417162731648](./ejercicio1.assets/image-20250417162731648.png)

<img src="./ejercicio1.assets/image-20250417162839558.png" alt="image-20250417162839558" style="zoom:50%;" />

Tras confirmar el borrado, podemos ver que el espacio usado es menor:

<img src="./ejercicio1.assets/image-20250417162915468.png" alt="image-20250417162915468" style="zoom:50%;" />

<img src="./ejercicio1.assets/image-20250417162954491.png" alt="image-20250417162954491" style="zoom:50%;" />

<img src="./ejercicio1.assets/image-20250417163047720.png" alt="image-20250417163047720" style="zoom:80%;" />

Ya no hay ningún contenedor:

![image-20250417163233720](./ejercicio1.assets/image-20250417163233720.png)

La red se borra haciendo clic en el botón resaltado en la siguiente imagen:

![image-20250417163312949](./ejercicio1.assets/image-20250417163312949.png)

![image-20250417163347926](./ejercicio1.assets/image-20250417163347926.png)

Y con esto finaliza la realización de este primer ejercicio con **Docker Desktop**.
