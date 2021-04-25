# Creando contenedor

A continuación, se muestra como generar un contenedor basado de la imagen de Ubuntu.

### 1. Creando un contenedor

Un contenedor se basa de una imagen para su creación, gracias a esta característica es posible crear múltiples contenedores en cuestión de segundos a diferencia de una máquina virtual la cual puede llevar de varios minutos en estar lista para su funcionamiento.

Para crear un contenedor ejecutamos el siguiente comando:


```bash
 docker run -it --rm ubuntu bash
 ```

Descripción:

- `docker run`: Indica que se desea iniciar un contenedor.
- `-it` : Estos parámetros permiten trabajar de manera interactiva (`i`) y se que se tendrá acceso a la TTY del contenedor (`t`).
- `--rm`: Cuando se detenga el contenedor este será eliminado de manera automática.
- `ubuntu`: La imagen que se utilizará para crear el contenedor.
- `bash`:  El último parámetro proporciona el comando que se desea ejecutar dentro el contenedor.

Ejemplo de salida:

**Nota**: para salir del contenedor es necesario ejecutar el comando `exit`.

![run_ubuntu.png](miscellaneous/docker_run_ubuntu.png)

El *prompt* (`root@7020d39d6f60:/#`) indica que nos encontramos dentro el contenedor el cual se basa de la imagen de Ubuntu. Dentro este contenedor se encuentra disponible la gran mayoría de los comandos disponibles en GNU/Linux.


### 2. Verificando contenedores en ejecución

Uno de los beneficios de utilizar contenedores es la capacidad de generar múltiples contenedores basada de la misma o diferente imagen de manera rápida y ágil.
Para visualizar que contenedores están en ejecución es posible utilizar el comando `docker ps`:


![docker_ps.png](miscellaneous/docker_ps.png)

Parámetros de salida

- `CONTAINER ID`: Identificador único del contenedor
- `IMAGE` : Imagen base utilizada para la creación del contenedor.
- `COMMAND`: Comando proporcionado a ejecutar en el contenedor.
- `CREATED`: Tiempo transcurrido desde la creación del contenedor.
- `STATUS`: Puerto(s) mapeados al contenedor.
- `NAME`: Nombre aleatorio generado de manera automática por Docker.


