# Docker Compose

> **Documento realizado por Roberto Delgado Sánchez - Alumno de Despliegue de Aplicaciones Web - DAW**

[TOC]

## 1. Enunciado

En este ejercicio vamos a trabajar con **FileBrowser**, aplicación de código abierto que permite administrar y compartir archivos desde un navegador web de forma sencilla y segura, es decir, que sirve para crear una nube particular. Proporciona una interfaz intuitiva que soporta tareas como subir, descargar, mover, copiar, renombrar y borrar ficheros y carpetas.

Asimismo, incluye características avanzadas como al edición de archivos de texto en el navegador, la creación de enlaces compartidos con configuraciones personalizables y la configuración de permisos de acceso para varios usuarios.

Es compatible con múltiples sistemas operativos y puede integrarse en entornos como servidores domésticos, servicios en la nube o contenedores Docker, ofreciendo flexibilidad para distintos usos.

El proyecto está alojado en https://hub.docker.com/r/hurlenko/filebrowser.

<img src="./ejercicio2.assets/image-20250417194801012.png" alt="image-20250417194801012" style="zoom:50%;border:1px solid black;" />

## 2. Despliegue del contenedor

Para poder desplegar esta aplicación debemos crear un archivo `docker-compose.yaml` con el siguiente contenido, creado a partir del modelo básico que se muestra en la web del proyecto:

- `image`: imagen de partida para crear el contenedor que permitirá ejecutar la aplicación.
- `container_name`: nombre que queremos reciba el contenedor.
- `ports`: puerto en el que "escuchará" las peticiones esta aplicación.
- `volumes`: carpetas del host local en las que se guardarán los datos (usamos `bind-mount`).
- `restart`: el contenedor se reinicia al detener su ejecución salvo que lo detenga un administrador.

```yaml
services:
  filebrowser:
    image: hurlenko/filebrowser:latest
    container_name: filebrowser_ej2
    ports:
      - "8080:8080"
    volumes:
      - ./fb-data:/data
      - ./fb-config:/config
    restart: unless-stopped    
```

Copiamos este archivo `docker-compose.yaml` en la carpeta del `ejercicio2` y ejecutamos este comando para crear el contenedor aprovechando la aplicación **Git** **Bash**:

```bash
$ docker compose up -d
```

<img src="./ejercicio2.assets/image-20250417210112577.png" alt="image-20250417210112577" style="zoom:67%;" />

![image-20250417210338212](./ejercicio2.assets/image-20250417210338212.png)

Resulta curioso que, a pesar de que aparece en el archivo `yaml` de ejemplo en la web del proyecto, al crear el contenedor nos diga que el parámetro `version` está obsoleto, por lo que aunque aparezca en la imagen de este archivo en la versión final se elimina.

<img src="./ejercicio2.assets/image-20250417210831008.png" alt="image-20250417210831008" style="zoom:67%;border:1px solid black;" />

Una vez creado y puesto en marcha el contenedor podemos ver que se han creado las dos carpetas que van a almacenar los datos: `fb-data` y `fb-config`.

<img src="./ejercicio2.assets/image-20250417210719788.png" alt="image-20250417210719788" style="zoom:67%;border:1px solid black;" />

Asimismo, por razones desconocidas, en **Docker Desktop** el contenedor aparece con el nombre `ejercicio2`, mientras que si ejecutamos el comando `docker ps` para saber qué contenedores están en ejecución sí que aparece con el nombre definido en el archivo `yaml`, `filebrowser_ej2`:

<img src="./ejercicio2.assets/image-20250417211219351.png" alt="image-20250417211219351" style="zoom:80%;" />

## 3. Probando la aplicación

Para comprobar que ya tenemos **FileBrowser** funcionando correctamente sólo tenemos que abrir una ventana del navegador y conectarnos a http://localhost:8080:

![image-20250417211432754](./ejercicio2.assets/image-20250417211432754.png)

Entramos con los datos proporcionados (**admin/admin**):

![image-20250417211659231](./ejercicio2.assets/image-20250417211659231.png)

Cambiamos el idioma de la aplicación a `español`:

![image-20250417212105320](./ejercicio2.assets/image-20250417212105320.png)

![image-20250417212124454](./ejercicio2.assets/image-20250417212124454.png)

Creamos un archivo de texto (en la carpeta `fb-data` no hay nada todavía):

<img src="./ejercicio2.assets/image-20250417212859228.png" alt="image-20250417212859228" style="zoom:50%;" />

![image-20250417212524378](./ejercicio2.assets/image-20250417212524378.png)

![image-20250417212625238](./ejercicio2.assets/image-20250417212625238.png)

![image-20250417212725152](./ejercicio2.assets/image-20250417212725152.png)

Si ahora vamos a la carpeta `fb-data` vemos que se ha creado ese archivo:

<img src="./ejercicio2.assets/image-20250417212820851.png" alt="image-20250417212820851" style="zoom: 50%;" />

En la carpeta `fb-config` se ha creado automáticamente un archivo de nombre`filebrowser.db` imagino que con parámetros de configuración de la aplicación:

<img src="./ejercicio2.assets/image-20250417213159252.png" alt="image-20250417213159252" style="zoom:50%;" />

Vamos a subir un archivo a **FileBrowser**:

![image-20250417213849006](./ejercicio2.assets/image-20250417213849006.png)

![image-20250417214031997](./ejercicio2.assets/image-20250417214031997.png)

![image-20250417214102412](./ejercicio2.assets/image-20250417214102412.png)

![image-20250417214252405](./ejercicio2.assets/image-20250417214252405.png)

Y con esto finaliza la realización de este segundo ejercicio.