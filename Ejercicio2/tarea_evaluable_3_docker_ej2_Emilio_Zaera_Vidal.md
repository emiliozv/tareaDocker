<div style="text-align: center;">
    <h1>Actividad Evaluable 3</h1>
    <h2>Docker</h2>
    <h3>Ejercicio 2 - Docker Compose</h3>
    <h3>Despliegue de Aplicaciones Web - DAW Distancia<br>
    CIFP Sect. Industrial y Servicios - La Laboral<br>
    Curso 2024-2025<br>
    01 de abril de 2025<br>
    Emilio Zaera Vidal - 46.911.234-C</h3>
</div>






<div style="page-break-after: always;"></div>
> Autor: **Emilio Zaera Vidal** 
>
> fecha: 01 del 04 de 2025
[TOC]

## 1. Introducción

En el módulo de **Despliegue de Aplicaciones Web**, uno de los objetivos fundamentales es aprender a gestionar entornos de despliegue modernos utilizando tecnologías basadas en contenedores. En este contexto, la herramienta **Docker** se ha convertido en un estándar para la creación, configuración y administración de entornos aislados, facilitando el despliegue y la distribución de aplicaciones web.

La presente tarea evaluable tiene como finalidad reforzar los conocimientos adquiridos sobre Docker mediante la realización de tres ejercicios prácticos. A través de estos ejercicios, se trabajará la creación de contenedores en red, la orquestación de servicios y la construcción de una imagen personalizada. Todo ello permitirá al alumno familiarizarse con el ciclo completo de creación, despliegue y gestión de contenedores, así como con las buenas prácticas de documentación y organización de proyectos en un repositorio.

> La **orquestación de servicios** es el proceso de coordinar y gestionar varios contenedores para que funcionen juntos como una única aplicación. En Docker, se realiza con herramientas como **Docker Compose**, que permiten definir y automatizar la configuración y despliegue de todos los servicios desde un solo archivo.



## 2. Metodología

La metodología propuesta para esta tarea consiste en la resolución práctica de tres ejercicios diferenciados. En cada uno de ellos, se deberá crear un entorno utilizando distintas herramientas de Docker: redes y contenedores mediante Docker Desktop, despliegue con Docker Compose y creación de una imagen personalizada con Dockerfile. Todo el trabajo se documentará y organizará en un repositorio público de GitHub, utilizando ramas para cada ejercicio. Además, como parte de la evaluación, se solicita un videoclip donde el estudiante muestre y explique parte del trabajo realizado.

---

---



## 3. Preparativos

### Creación de un nuevo repositorio `tareaDocker`

Creo un nuevo repositorio público en [mi GitHub](https://github.com/emiliozv/tareaDocker) para la tarea:

<img src="./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401103607546.png" alt="image-20250401103607546" style="zoom:50%;" />



### Clonado y vinculación en local

Trabajaré en local para, al finalizar, subir todo al repositorio remoto en GitHub. Para ello, creo un repositorio local mediante la línea de comandos de git, genero las carpetas y los ficheros `.md`, y lo vinculo con el remoto:

![image-20250401110718554](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401110718554.png)

![image-20250401110750707](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401110750707.png)

![image-20250401110818708](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401110818708.png)

![image-20250401110840523](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401110840523.png)



### Creación de las ramas

Creo las 3 ramas y cambio a ellas cuando lo necesite. Ejemplo con rama `ejercicio1`:

```bash
git branch ejercicio1
git switch ejercicio1
```

 

## 4. Ejercicio 2 - Docker Compose

#### Breve explicación de la aplicación

**FileBrowser** es una aplicación muy ligera que permite gestionar y visualizar archivos y directorios desde un navegador web, como si fuera un explorador de archivos, pudiendo subir, descargar, renombrar y eliminar archivos, entre otras funciones. 

---



#### `compose.yaml`

> Voy a utilizar un volumen y un bind-mount para ver ambas opciones. La configuración estará en un volumen y los datos en un bind-mount.

```yaml
version: "3"

services:
  filebrowser:
    image: hurlenko/filebrowser:latest
    container_name: filebrowser
    ports:
      - "8080:8080"
    volumes:
      - file_config:/config          # Volumen gestionado por Docker
      - ./data:/data                 # Bind mount (carpeta local)
    restart: unless-stopped

volumes:
  file_config:

```

![image-20250401194629474](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401194629474.png)

![image-20250401194718704](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401194718704.png)

> `restart: unless-stopped` hace que el contenedor se reinicie automáticamente si se apaga por error o al reiniciar el equipo, **pero no se reinicia si el administrador lo detiene manualmente**.





---

#### Despliegue de FileBrowser

```bash
docker compose up -d
```

![image-20250401195712085](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401195712085.png)

![image-20250401195906579](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401195906579.png)

> Aunque en Docker Desktop aparezca el `ejercicio2` en el nombre del contenedor, realmente es `filebrowser`, tal como indicamos el el `yaml`.  Lo que se ve en **Docker Desktop** (el nombre de la carpeta o el proyecto) es solo un **nombre de grupo** que pone la interfaz para organizar los servicios, pero el contenedor real sí tiene el nombre que yo configuré.

A continuación, desde el navegador entramos en la interfaz gráfica de la aplicación:

```url
http://localhost:8080
```

<img src="./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401200108059.png" alt="image-20250401200108059" style="zoom:50%;" />

<img src="./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401200137666.png" alt="image-20250401200137666" style="zoom:50%;" />

Creo una carpeta `ejercicio2` y un fichero `ejercicio2.txt` con contenido:

<img src="./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401200309650.png" alt="image-20250401200309650" style="zoom:50%;" />

---



#### Carpeta y volumen creados

```bash
docker inspect filebrowser
```

![image-20250401201249078](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401201249078.png)

Como podemos ver en la captura anterior, en la sección "Mounts" vemos el bind-mount para los datos y el volumen para la configuración.

Directorio del bind-mount para los datos:

![image-20250401201526396](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401201526396.png)

Como estoy en windows, usando Docker Desktop, el volumen vive dentro de la máquina virtual de Docker, que no es visible desde el explorador de windows. Sin embargo, en Docker Destkop - Volumes, vemos lo siguiente:

![image-20250401202410623](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401202410623.png)

![image-20250401202425356](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401202425356.png)

---



#### Subida de un fichero y cambio de idioma en FileBrowser

![image-20250401202723261](./tarea_evaluable_3_docker_ej2_Emilio_Zaera_Vidal.assets/image-20250401202723261.png)

Como podemos obervar en la captura de pantalla, se ha subido el fichero `pdf` del enunciado de la tarea y ya se ve la interfaz en español.
