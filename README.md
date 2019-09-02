# Jupyter notebook para análisis de datos asociados a la ejecución de tareas en el cluster computacional de Univalle

El cluster computacional de Univalle lleva en operación casi 10 años.
Actualmente se tiene registro de las ejecuciones hechas desde el 2015 a la fecha (Agosto 2019).
En este repositorio encontrará un *notebook* de Jupyter que permite visualizar algunos valores relativos al uso del cluster de Univalle.

Para correr el *notebook* se usará una imagen de Docker.
Se debe tener entonces instalado Docker en su máquina.

## Como correr el *notebook*

Para ejecutar el notebook se debe ejecutar lo siguiente desde una terminal y ubicado en el directorio donde se clonó este repositorio.

```
docker run -p 8888:8888 --rm -v $(pwd):/home/jovyan josanabr/jupyter-notebook
```

Al momento de levantar la ejecución del contenedor se observan unos mensajes en pantalla y se debe tener especial cuidado con un mensaje como este:

```
    To access the notebook, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/nbserver-6-open.html
    Or copy and paste one of these URLs:
        http://fca7a883370b:8888/?token=4c2fba58f3d123812196149736c40f13b8226389f275c52e
     or http://127.0.0.1:8888/?token=4c2fba58f3d123812196149736c40f13b8226389f275c52e
```

Como indica el mensaje, corte y pegue en su navegador uno de esos enlaces y ya tendrá acceso al *notebook* para ver e interactuar con los datos obtenidos a partir de monitorear la ejecución de tareas en el cluster de Univalle.

Una vez se abra la interfaz de Jupyter, se debe seleccionar el *notebook* `Analizando Datos del Cluster Univalle.ipynb`.

Además de este *notebook* se hace necesario tener el archivo `history.csv.gzip`.
En este archivo se tienen los datos históricos del cluster.

Estos datos se generan con otra herramienta que se puede encontrar [aquí](aquí).

## Información relativa a la imagen `josanabr/jupyter-notebook`

La imagen `josanabr/jupyter-notebook` es derivada de la imagen `jupyter/minimal-notebook`.
La diferencia entre ambas es que a la primera se la han instalado los siguientes paquetes:

   * numpy
   * pandas
   * matplotlib

### Como se creo la nueva imagen?

La imagen `josanabr/jupyter-notebook` se creo a partir de un contenedor en ejecución derivado de la imagen `jupyter/minimal-notebook`.
Una vez se identifica el `id` del contenedor se ejecutan las siguientes instrucciones (asuma que el `id` es `7a`):

```
docker exec 7a  pip install numpy pandas matplotlib
```

Una vez se tiene el software instalado en el contenedor se genera una imagen de Docker a partir del mismo como sigue:

```
docker commit 7a josanabr/jupyter-notebook
```

