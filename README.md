# Practica-Docker-Alpine

# Práctica de Docker con Alpine

Esta práctica consiste en realizar varias tareas utilizando la imagen de Alpine en Docker. A continuación, se detallan los pasos realizados con los comandos utilizados y una breve descripción de cada uno.

## 1. Descargar la imagen "alpine" SIN ARRANCARLA y comprobar que está en tu equipo

- **Comandos utilizados:**
    ```bash
    docker pull alpine
    docker images
    ```

- **Descripción:**
    - Se descarga la imagen "alpine" desde Docker Hub.
    - Se verifica que la imagen se haya descargado correctamente con el comando `docker images`.

---

## 2. Crear un contenedor sin ponerle nombre. ¿Está arrancado? Obtén el nombre

- **Comandos utilizados:**
    ```bash
    docker run -d alpine sleep 3600
    docker ps
    docker ps -a
    ```

- **Descripción:**
    - Se crea un contenedor en segundo plano que ejecuta el comando `sleep 3600` para mantenerlo activo.
    - Con `docker ps` se comprueba que el contenedor esté en ejecución.
    - Con `docker ps -a` se obtienen todos los contenedores, incluyendo los que no están en ejecución, para ver el nombre asignado automáticamente.

---

## 3. Crear un contenedor con el nombre 'dam_alp1'. ¿Cómo puedes acceder a él?

- **Comandos utilizados:**
    ```bash
    docker run -d --name dam_alp1 alpine sleep 3600
    docker exec -it dam_alp1 /bin/sh
    ```

- **Descripción:**
    - Se crea un contenedor llamado 'dam_alp1' y se ejecuta en segundo plano.
    - Se accede al contenedor 'dam_alp1' utilizando el comando `docker exec -it dam_alp1 /bin/sh` para iniciar una sesión interactiva de shell.

---

## 4. Comprobar qué IP tiene y si puedes hacer un ping a google.com

- **Comandos utilizados:**
    ```bash
    docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' dam_alp1
    docker exec -it dam_alp1 ping -c 4 google.com
    ```

- **Descripción:**
    - Se obtiene la dirección IP del contenedor 'dam_alp1'.
    - Se realiza un ping a google.com desde el contenedor para verificar la conectividad.

---

## 5. Crear un contenedor con el nombre 'dam_alp2'. ¿Puedes hacer ping entre los contenedores?

- **Comandos utilizados:**
    ```bash
    docker run -d --name dam_alp2 alpine sleep 3600
    docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' dam_alp2
    docker exec -it dam_alp1 ping -c 4 <IP_dam_alp2>
    ```

- **Descripción:**
    - Se crea un segundo contenedor llamado 'dam_alp2' que se ejecuta en segundo plano.
    - Se obtiene la IP del contenedor 'dam_alp2'.
    - Se realiza un ping desde 'dam_alp1' a la dirección IP de 'dam_alp2' para comprobar la conectividad entre los contenedores.

---

## 6. Sal del terminal, ¿qué ocurrió con el contenedor?

- **Comandos utilizados:**
    ```bash
    exit
    docker ps
    ```

- **Descripción:**
    - Al ejecutar `exit`, se sale de la sesión del contenedor, pero el contenedor sigue ejecutándose en segundo plano debido a que fue creado en modo detached (`-d`).

---

## 7. ¿Cuánta memoria en el disco duro ocupaste?

- **Comandos utilizados:**
    ```bash
    docker system df
    ```

- **Descripción:**
    - Se utiliza `docker system df` para mostrar el espacio en disco utilizado por imágenes, contenedores y volúmenes de Docker.

---

## 8. ¿Cuánta RAM ocupan los contenedores? ¿Hay algún comando Docker para saber esto?

- **Comandos utilizados:**
    ```bash
    docker stats --no-stream
    ```

- **Descripción:**
    - Se utiliza `docker stats --no-stream` para mostrar el uso de CPU, memoria (RAM), red y disco de cada contenedor en un momento específico.
