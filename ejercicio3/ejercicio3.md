# Imagen con Dockerfile y aplicación web

> **Documento realizado por Roberto Delgado Sánchez - Alumno de Despliegue de Aplicaciones Web - DAW**

[TOC]

## 1. Enunciado

En este ejercicio vamos a abordar la creación de una imagen con **Dockerfile**, sistema de **Docker** que nos permite partir de una imagen ya creada y modificarla a nuestro gusto para que pueda ser redistribuida posteriormente. 

En nuestro caso partiremos de la imagen `php:7.4-apache` a la que le añadiremos un sitio web y un script **PHP** para posteriormente crear otra imagen que subiremos a nuestra cuenta de **Docker** **Hub**.

## 2. Creación de la web

Se nos pide que creemos un sitio web sencillo en el que figure nuestro nombre y que debe constar al menos de un archivo `index.html` y de una hoja de estilos. Ambos ficheros los crearemos dentro de una carpeta que se llamará `miweb`:

## 3. Creación del fichero Dockerfile