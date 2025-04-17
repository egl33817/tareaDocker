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



## 4. Creación de un contenedor con Adminer o phpMyAdmin

## 5. Instalación y uso de la extensión Disk Usage
