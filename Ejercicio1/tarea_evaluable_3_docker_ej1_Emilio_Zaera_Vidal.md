<div style="text-align: center;">
    <h1>Actividad Evaluable 3</h1>
    <h2>Docker</h2>
    <h3>Ejercicio 1 - Contenedores en red y Docker Desktop</h3>
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

---

---



## 2. Metodología

La metodología propuesta para esta tarea consiste en la resolución práctica de tres ejercicios diferenciados. En cada uno de ellos, se deberá crear un entorno utilizando distintas herramientas de Docker: redes y contenedores mediante Docker Desktop, despliegue con Docker Compose y creación de una imagen personalizada con Dockerfile. Todo el trabajo se documentará y organizará en un repositorio público de GitHub, utilizando ramas para cada ejercicio. Además, como parte de la evaluación, se solicita un videoclip donde el estudiante muestre y explique parte del trabajo realizado.

---

---



## 3. Preparativos

### Creación de un nuevo repositorio `tareaDocker`

Creo un nuevo repositorio público en [mi GitHub](https://github.com/emiliozv/tareaDocker) para la tarea:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401103607546.png" alt="image-20250401103607546" style="zoom:50%;" />



### Clonado y vinculación en local

Trabajaré en local para, al finalizar, subir todo al repositorio remoto en GitHub. Para ello, creo un repositorio local mediante la línea de comandos de git, genero las carpetas y los ficheros `.md`, y lo vinculo con el remoto:

![image-20250401110718554](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401110718554.png)

![image-20250401110750707](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401110750707.png)

![image-20250401110818708](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401110818708.png)

![image-20250401110840523](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401110840523.png)



### Creación de las ramas

Creo las 3 ramas y cambio a ellas cuando lo necesite. Ejemplo con rama `ejercicio1`:

```bash
git branch ejercicio1
git switch ejercicio1
```

---

---



## 4. Ejercicio 1 - Contenedores en red y Docker Desktop

### Creación red bridge `redej1`

Este ejercicio se realiza desde Docker Desktop

> En Docker Desktop instalamos previamente la extensión `PortNavigator`

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401131641349.png" alt="image-20250401131641349" style="zoom:50%;" />

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401131451829.png" alt="image-20250401131451829" style="zoom:50%;" />

![image-20250401131810863](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401131810863.png)

---



### Creación contenedor de `mariadb`

Primero busco la imagen oficial de `mariadb` en el buscador de Docker Desktop y la descargo pulsando sobre el botón `Pull`:

![image-20250401132004680](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401132004680.png)

A continuación creo el contenedor pulsando sobre `Run`:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401132220768.png" alt="image-20250401132220768" style="zoom:50%;" />

Podemos ver esta ventana de ajustes opcionales, donde introduciremos la información solicitada en el enunciado:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401132454735.png" alt="image-20250401132454735" style="zoom:50%;" />

Para ello tendremos que encontrar en la documentación de la imagen la información necesaria:

- Definición de contraseña para el usuario root:

  <img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401132859846.png" alt="image-20250401132859846" style="zoom: 50%;" />

  El nombre de la variable de entorno es `MARIADB_ROOT_PASSWORD`, para el valor (la contraseña) estableceré "root".

  

- Definir un usuario con mi nombre de pila y con contraseña:

  https://mariadb.com/kb/en/mariadb-server-docker-official-image-environment-variables/

  <img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401134650111.png" alt="image-20250401134650111" style="zoom:50%;" />

  - Nombre de usuario: El nombre de la variable de entorno es `MARIADB_USER`. Su valor será "Emilio"

  - Contraseña: El nombre de la variable de entorno es `MARIADB_PASSWORD`. Su valor será "1234"

    

- Nombre de la BD por defecto será `DAW`:

  <img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401135034509.png" alt="image-20250401135034509" style="zoom:50%;" />

  - Nombre de la BD: El nombre de la variable de entorno es `MARIADB_DATABASE`. Su valor será "DAW"



Con la información anterior, queda de la siguiente manera:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401150546214.png" alt="image-20250401150546214" style="zoom:50%;" />

![image-20250401135609531](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401135609531.png)



#### Script creación de tabla `modulos`

```sql
CREATE TABLE modulos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50) NOT NULL
);

INSERT INTO modulos (nombre) VALUES
('cliente'),
('servidor'),
('interfaces'),
('despliegue'),
('empresa'),
('proyecto'),
('prácticas');
```

---



### Creación de contenedor con `Adminer`

Introduzco "adminer" en el buscador de Docker Desktop y hago un `Pull` de la imagen, para luego crear el contenedor meidante `Run`:

![image-20250401140520333](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401140520333.png)

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401145039200.png" alt="image-20250401145039200" style="zoom:50%;" />

![image-20250401141428398](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401141428398.png)

---



### Conexión de los contenedores a la red `redej1`

Primero desconecto de la red bridge por defecto (muestro `mariadb_ej1`):

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401141728227.png" alt="image-20250401141728227" style="zoom:50%;" />

A continuación, conecto ambos contenedores a la red `redej1` (muestro `adminer_ej1`):

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401141546622.png" alt="image-20250401141546622" style="zoom:50%;" />

Resultado de la configuración de red:

![image-20250401141938578](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401141938578.png)

Compruebo mediante ping la conexión de adminer con mariadb:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401143850294.png" alt="image-20250401143850294" style="zoom:50%;" />



---



### Conexión a la BD con Adminer

```url
http://localhost:8088
```

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401150829703.png" alt="image-20250401150829703" style="zoom:50%;" />

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401150841464.png" alt="image-20250401150841464" style="zoom:50%;" />

---



### Ejecución del script SQL desde la GUI de Adminer

Creación de la tabla `modulos` mediante el script (SQL command):

![image-20250401151023177](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151023177.png)

Muestra de los datos contenidos en la tabla (SELECT modulos):

![image-20250401151128947](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151128947.png)

---



### Instalación de Disk Usage

Lo busco en el buscador de Docker Desktop y filtro por extensiones:

![image-20250401151416617](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151416617.png)

Muestro el espacio ocupado:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151507643.png" alt="image-20250401151507643" style="zoom:50%;" />

Borro el contenedor `mariadb_ej1` y compruebo la diferencia:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151706865.png" alt="image-20250401151706865" style="zoom:50%;" />

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151729529.png" alt="image-20250401151729529" style="zoom:50%;" />

---



### Borro los contenedores y la red

![image-20250401151902487](./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401151902487.png)

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401152000512.png" alt="image-20250401152000512" style="zoom:50%;" />

Resultado, ningún contenedor:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401152018055.png" alt="image-20250401152018055" style="zoom:50%;" />

Borrado de la red `redej1`:

<img src="./tarea_evaluable_3_docker_ej1_Emilio_Zaera_Vidal.assets/image-20250401152137093.png" alt="image-20250401152137093" style="zoom:50%;" />

