# Uso de *bind mounts*

Docker permite que los direcotrios y archivos en el *host* sea accesible dentro el contenedor. Los archivos o directorios hacen referencia a la ruta absoluta en el *host*. 


### 1. Utilizando *bind mount*

Al momento de ejecutar un contenedor es posible espesificar que directorios del *host* estará disponible en el contenedor agregando el parametro `--mount`. 

	--mount type=bind,source=<host_path>,target=<container_destination_path>

* `type` indica que se vinculará un directorio del *host* dentro el contenedor.
* `source` ruta absoluta del directorio o archivo que será accesible dentro el contenedor.
* `destionation` ruta absoluta del directorio o archivo donde se depositará dentro el contenedor.

Ejemplo:

Considere que se desea acceder el directorio `target` que se encuentra en el directorio de trabajo actual sea accesible dentro el contenedor en el directorio `/app`. Una manera de lograr esto es proporcionar en el atributo `source` el valor `$(pwd)/target` (`$(pwd)` indica de manera reducida el directorio de trabajo). En el atributo `target` es necesario

```
docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx:latest
```
**Nota:** El parámetro `--name` permite establecer el nombre del contenedor.

### 2. Trabajando con volumenes

Los volumenes un el mecanismo preferido para almacenar información de manera persistente en los contenedores de Docker. Bind depende de la estrucutra de directorios para trabajar, los volumenes son completamente manejado por Docker.

Existen multiples comandos para administrar los volumenes en Docker, a continuación se muestran los más comunes:

*	`docker volume create <vol_name>`: Crear un nuevo volumen
*	`docker volume ls`: Listar volumenes disponibles
*	`docker volume inspect <vol_name>`: Ver información detallada del volumen
*	`docker volume rm <vol_name>`: Eliminar volumen

### 3. Asignando un volumen al contenedor

Existe multples 

![docker_build.png](miscellaneous/docker_build.png)