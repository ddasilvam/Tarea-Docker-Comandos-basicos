## Tarea: Docker - Comandos básicos
La siguiente práctica es una lista de tareas que tenéis que hacer. Por cada tarea tenéis que ir poniendo los comandos utilizados y, brevemente, describir el proceso.

Utilizaremos la imagen de Ubuntu (la última). Usa Visual Studio Code y Docker junto con esta imagen para seguir las siguientes instrucciones:
### 1. Descarga la imagen ubuntu y comprueba que está en tu equipo

En una terminal ejecutamos `docker image pull ubuntu`. Comprobamos que está en el equipo ejecutando `docker image list`.
```console
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu       latest    c6b84b685f35   4 weeks ago    77.8MB
```
### 2. Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre
Creamos un contenedor sin nombre con `docker run -it ubuntu bash`. De esta manera el contenedor se crea y automáticamente se accede al terminal del mismo usando bash. Podemos comprobar que está en ejecución utilizando `docker ps` en otra pestaña.
```console
CONTAINER ID    IMAGE   COMMAND     CREATED     STATUS    PORTS        NAMES
c807a7f5c72d    ubuntu  "bash"  59 seconds ago    Up    59 seconds   focused_bhaskara
```
Podemos ver que el nombre que le ha dado es focused_bhaskara.
### 3. Crea un contenedor con el nombre 'ubu1'. ¿Como puedes acceder a él?
Utilizando `docker run -it --name ubu1 ubuntu bash` creamos un nuevo contenedor con el nombre ubu1 que ejecuta bash.

Si queremos acceder a este contenedor desde una terminal, ejecutaremos `docker exec -it ubu1 bash`.
### 4. Comprueba que ip tiene y si puedes hacer un ping a google.com
Para comprobar si tiene IP, necesitamos la utilidad `ifconfig`. Para ello, primero instalamos el paquete `net-tools` ejecutando `apt update && apt install net-tools`. A continuación ejecutamos `ifconfig` y comprobamos que el contenedor tiene la IP 172.17.0.2.

Para hacer ping a google.com, necesitamos la utilidad `ping`. Para ello, primero instalamos el paquete `inetutils-ping` ejecutando `apt install inetutils-ping`. A continuación ejecutamos `ping google.com` y comprobamos que se ejecuta con éxito.
### 5. Crea un contenedor con el nombre 'ubu2'. ¿Puedes hacer ping entre los contenedores?
Creamos un contenedor llamado ubu2 siguiendo los mismos pasos e instalando las herramientas de los puntos 3, 4 y 5. Comprobamos que el contenedor ubu2 tiene la IP 172.17.0.3. Si en ubu2 ejecutamos `ping 172.17.0.2` vemos que se ejecuta con éxito. Si en ubu1 ejecutamos `ping 172.17.0.3` también se ejecuta con éxito. Por tanto, puede realizarse ping entre ambos contenedores.
### 6. Sal del terminal, ¿que ocurrió con el contenedor?
En ubu2 ejecutamos el comando `exit` y abandonamos su consola. Si hacemos `docker ps` vemos que ubu1 se está ejecutando, pero ubu2 no. Esto no quiere decir que el contenedor no exista, ya que si hacemos `docker ps -a` podemos ver que el contenedor existe, pero está parado.
### 7. ¿Cuanta memoria en el disco duro ocupaste? ¿Hay alguna herramienta de docker para calcularlo?
Ejecutando `docker ps -a --size` se nos mostrarán todos los contenedores creados, así como la memoria ocupada. En el caso de ubu1 y ubu2, cada uno ocupan 45.3MB en disco y 123MB de memoria virtual.
### 8. ¿Cuanta RAM ocupan los contenedores? Crea cuantos contenedores necesites para calcularlo.
Para ver la RAM que ocupan los contenedores, podemos usar la herramienta `docker stats`. Con los contenedores recién arrancados, se muestra un uso de 872KiB y 888KiB de memoria RAM, respectivamente.
```console
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O       BLOCK I/O   PIDS
eec24f65000c   ubu2      0.00%     872KiB / 15.39GiB              0.01%     4.54kB / 0B      0B / 0B         1
2832714c42a0   ubu1      0.00%     888KiB / 15.39GiB             0.01%     4.92kB / 0B      0B / 0B         1
```