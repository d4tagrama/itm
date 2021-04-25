# Boxes #

*Box* son paquetes utilizados por Vagrant para generar máquinas virtuales basados en plantillas. Vagrant proporciona las utilerías necesarias para descargar y administrar las plantillas(Box) disponibles en los repositorios ubicados en Internet.



### 1. Descargando *box*

*Vagrant* cuenta con un catálogo en internet con la mayoría de los sistemas operativos base y aplicaciones como: LAMP stacks, Ruby, Python, entre otros. Para descargar una plantilla o *Box* del repositorio público Vagrant proporciona el comando:

```bash
vagrant box add USER/BOX
```


Por ejemplo, para descargar el *box* referente a Ubuntu bionic ejecutamos el comando:

```bash
vagrant box add ubuntu/bionic64
```
Es posible consultar la lista de *Box* Disponible en el [sitio](https://app.vagrantup.com/boxes/search) de Vagrant Cloud.

### 2. Visualizando plantillas (Box)

El comando `vagrant box list` permite visualizar las plantillas disponibles en el sistema local. Las plantillas descargadas permiten generar máquinas virtuales sin la necesidad del uso de Internet acelerado el proceso de instalación. 

Ejemplo de salida del comando list: 

![box_list.png](miscellaneous/box_list.png)

### 3. Eliminar Box

Cuando las platillas ya no son requeridas y se requiere recuperar el espacio consumido por las mismas es necesario eliminar las con el comando `remove`.
```bash
vagrant box remove <box name>
```