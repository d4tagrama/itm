# Personalizando contenedores

Existe una amplia varidad de imagenes disponibles en diferente repositorios, pero en ocasiones estas imagenes no se comodan a la necesidad de nuestra aplicación. Docker permite personalizar la imagen base y obtener como resultado una nueva imagen a la medida de la aplicación a publicar.



### 1. Usando Dockerfile

Acontinuación crearemos un Dockerfile el cual permita crear una aplicación web basada en *node*: 

	FROM node
    WORKDIR /app
	COPY disc/* /app
	RUN npm install
    EXPOSE 8080
	CMD ["node", "server.js"]

Descripción de parametros:

- `FROM` crea una capa de la imagen node.
- `WORKDIR` establece como directorio de trabajo el directorio /app (similar a ejecutar `cd /app`)
- `COPY` agregar los archivos del directororio actual al directorio /app dentro del contenedor.
- `RUN` ejecuta el comando indicado.
- `EXPOSE` indica que puertos estará en escucha el contenedor.
- `CMD` especifica que comando ejecutará por omisión el contenedor.


### 2. Crendo imagen

Para generar la nueva imagen Docker proporciona el comando `build` para generar una nueva imagen basandode de otra y personalizar la nueva imagen con el Dockerfile indicado.

```
docker build -t <repositorio>/<nombre_contenedor>:<tag> <ubicación del Dockerfile>
```

Para crear la nueva es necesario realizar los siguientes pasos:

1. Ubicarnos en el directorio *dockerfile*.
2. Dentro este directorio ejecutar el siguiente comando `docker build -t roid/itm:v2 .`

Ejemplo de salida:

![docker_build.png](miscellaneous/docker_build.png)


Para verficar la creación de la nueva imagen utilizamos el comando `docker images` para visualizar las imágenes disponibles de manera local.

![docker_images_build.png](miscellaneous/docker_images_build.png)


### 3. Ejecutando contenedor

La ejecución de un contenedor se puede realizar de dos maneras la priema permite ejecutar el contenedor de manera interactiva es decir visualizar el *standard output* del contendor en pantalla. La segunda opcion es ejecutar el contenedor en modo no atendido un *background*.

1. Modo interactivo.

	Para ejecutar un contenedor Docker cuenta con el `run` para poner en marcha el contenedor. Para ejecutar un contenedor basado de la imagen generada con anterioridad ejecutamos el siguiente comando:
    
    ```
	docker run -it roid/itm:v2
    ```
    
    Ejemplo de salida:

    ![docker_run_it.png](miscellaneous/docker_run_it.png)

2. Modo no atendido	

	Para la ejecución en modo *background* utilizaremos el comando `run`, pero con la diferencia de enlugar de pasar los parametros `-it` pasaremos el parametro `-d`.

    ```
	docker run -d roid/itm:v2
    ```
    
**Nota:** Para verificar si el contenedor se esta ejecutando en *background* ejecutamos el comando `docker ps`
    
### 4. Verificando aplicación web

Aún cuando el contenedor se encuentra en ejecución solo es posible acceder al servicio web de manera local. Para acceder al servicio es necesario identificar la dirección IP que adquirio el contenedor. 

Lo anterior se puede lograr utilizando el comando :

```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <id_del_contenedor>
``` 

Para verificar si el contenedor esta ejecutando la aplicación web abrimos nuestro navegador favorito ingresando la dirección IP y el puerto 8080 sobre la cual esta ejecutando nuestra aplicación.


![docker_web_browser.png](miscellaneous/docker_web_browser.png)

**Nota:** El identificado del ID se puede obtener con el comando `docker ps`

### 5. Mapear puertos

En ocasiones es necesario permitir que los usuario visualicen la aplicación web dentro el contenedor de manera externa para su validación. Para permitir que una aplicación web que se encuentra dentro un contenedor este disponible fuera del *host* que hospeda el contenedor es necesario proporcionar el parámentro `-p <host_port>:<container_port>` (parámetro puerto) al comando `run` para exponer los puertos del contenedor hacia el exterior.


Ejemplo:

	docker run -it -p 8080:8080 roid/itm:v2
    
    
Procedemos abrir nuestro navegador ingresando la IP de nuestro dispositivo. A partir de este momento cualquier persona que tenga la dirección IP de *host* y el puerto que se mapio de la aplicación podrá acceder a la aplicación web.

![docker_web_browser_port.png](miscellaneous/docker_web_browser_port.png)