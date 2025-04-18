# Actividad evaluable 3 - Docker

> **Documento realizado por Roberto Delgado Sánchez - Alumno de Despliegue de Aplicaciones Web - DAW**

[TOC]

## 1. Consideraciones previas

En esta actividad se pondrán en práctica los conocimientos adquiridos en esta asignatura sobre el sistema de virtualización ligera **Docker**. El primer paso será crear un repositorio público en **GitHub** con nuestro usuario de **educastur** para dejar en él todos los documentos que vayamos generando:

<img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250416233054222.png" alt="image-20250416233054222" style="zoom:50%;" />

El desarrollo de la documentación de cada ejercicio se hará en local y al finalizar se subirá todo al repositorio remoto. La creación del repositorio local no tiene mucha ciencia, pues se siguen los mismos pasos que en la segunda tarea de esta asignatura:

- inicializamos el repositorio y revisamos que los parámetros de configuración de **Git** son los correctos:

  ```bash
  $ git init
  $ git config --list
  ```

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250416235334902.png" alt="image-20250416235334902" style="zoom: 60%; border: 1px solid black;" />

  En los recuadros en rojo se pueden ver mis datos personales (nombre, apellidos y correo de **educastur**).

- cambiamos el nombre de la rama principal de `master` a `main` para no tener problemas al subir los archivos al repositorio remoto:

  ```bash
  $ git branch -M main
  ```

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417000345448.png" alt="image-20250417000345448" style="zoom: 60%;border:1px solid black;" />

- creación de una carpeta para cada ejercicio y, dentro de cada una de ellas, una versión inicial del archivo `md` que contendrá el desarrollo de cada ejercicio. Asimismo, creo este archivo que contendrá, además de los pasos de configuración del repositorio, la URL del mismo en remoto y la del vídeo que hay que crear:

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417001609444.png" alt="image-20250417001609444" style="zoom:67%;border:1px solid black;" />

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417001840788.png" alt="image-20250417001840788" style="zoom: 48%;border:1px solid black;" />

- hacemos nuestro primer `commit` para registrar todo lo creado hasta ahora:

  ```bash
  $ git status
  $ git add .
  $ git commit -m "Creación de carpetas y ficheros de partida para cada ejercicio."
  ```

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417002331797.png" alt="image-20250417002331797" style="zoom:55%;" />

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417002508954.png" alt="image-20250417002508954" style="zoom: 53%;" />

  Tras hacer el commit vemos que el archivo en el que vamos introduciendo detalles generales de la práctica tiene cambios que no han sido añadidos al `commit`, lo cual es natural ya que es un archivo dinámico que se va actualizando con las capturas de pantalla necesarias.

- sincronizamos todo lo anterior con el repositorio remoto:

  ```bash
  $ git remote add origin https://github.com/egl33817/tareaDocker.git
  $ git remote -v
  $ git push -u origin main
  ```

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417002850965.png" alt="image-20250417002850965" style="zoom:67%;" />

  Estos comandos son los que indica GitHub al crear el repositorio remoto:

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417002950129.png" alt="image-20250417002950129" style="zoom: 55%;" />

- ya por último, comprobamos que en el repositorio remoto tenemos la misma estructura de carpetas y ficheros que hemos creado en nuestro repositorio local tras hacer la sincronización entre ambos repos:

  <img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417003226225.png" alt="image-20250417003226225" style="zoom:38%;" />

A partir de aquí ya podemos centrarnos en el desarrollo de cada ejercicio, por lo que crearemos una rama para cada uno de ellos, conectándonos finalmente a la primera para empezar con ese primer ejercicio:

<img src="./Actividad%20evaluable%203%20-%20Docker.assets/image-20250417095740201.png" alt="image-20250417095740201" style="zoom:60%;border:1px solid black;" />

## 2. URL del repositorio remoto

El repositorio remoto que se ha creado en **GitHub** puede ser localizado en la siguiente URL:

https://github.com/egl33817/tareaDocker

## 3. URL del vídeo

El enlace al vídeo en el que se muestra el repositorio creado y se hace una demostración del funcionamiento de la aplicación **FileBrowser** es el siguiente:

[delgadosanchez_roberto_DAW_tareaDocker.mp4](https://educastur-my.sharepoint.com/:v:/g/personal/egl33817_educastur_es/ES1fShHnq3dIhxB2PMQgzb8BIGa52E3y0g07R-Xzvkt6lw?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&email=minesmp@educastur.org&e=2LUMTS)