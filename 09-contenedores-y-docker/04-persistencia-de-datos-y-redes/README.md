# Tema 4: Persistencia de datos (El antídoto contra la amnesia)

Hasta ahora hemos visto que los contenedores son maravillosos porque son de "usar y tirar". Pero piénsalo un segundo: si instalamos una base de datos MariaDB en un contenedor, guardamos todos los usuarios de nuestra web, y mañana borramos el contenedor para actualizarlo a una versión más nueva... **¡Habremos borrado toda la base de datos!**

Los contenedores nacen con *amnesia*. Por defecto, todo lo que se crea dentro de un contenedor, muere con el contenedor. 

Para solucionar esto, Docker inventó los **Volúmenes** y los **Bind Mounts**.



## 🧠 1. Volúmenes vs Bind Mounts
Ambas tecnologías sirven para lo mismo: hacer un "agujero de gusano" entre una carpeta de tu servidor Linux real y una carpeta dentro del contenedor. Si el contenedor se destruye, los datos siguen a salvo en tu servidor.

*   **Bind Mount (Montaje de enlace):** Tú eliges una ruta exacta de tu servidor (ej. `/home/usuario/mi-web`) y la conectas al contenedor. Es perfecto para cuando estás programando y quieres ver los cambios en vivo.
*   **Volumen (Volume):** Tú le dices a Docker: *"Crea un espacio seguro para guardar cosas"*. No te importa exactamente en qué rincón del disco duro lo guarda Docker, solo quieres que esté a salvo. Es lo que se usa en producción para bases de datos.

## 📁 2. Práctica: Tu web persistente (Bind Mount)
Vamos a levantar un servidor Nginx, pero esta vez no le dejaremos mostrar su página por defecto. Le obligaremos a mostrar una página web que nosotros tenemos guardada a salvo en nuestro disco duro real.

1.  **Crea una carpeta en tu servidor real:**
    ```bash
    cd ~
    mkdir mi-web
    cd mi-web
    ```
2.  **Crea un archivo HTML personalizado:**
    ```bash
    nano index.html
    ```
    Escribe algo sencillo:
    ```html
    <h1>¡Hola desde mi servidor real!</h1>
    <p>Este archivo sobrevive aunque el contenedor explote 💥</p>
    ```
    Guarda y cierra (Ctrl+O, Enter, Ctrl+X).

3.  **Lanza el contenedor con el "agujero de gusano" (`-v`):**
    Presta mucha atención a la bandera `-v` (Volume). Vamos a mapear la ruta absoluta de tu carpeta (`$PWD` significa *Print Working Directory*, es decir, la carpeta actual) con la carpeta donde Nginx lee los archivos dentro del contenedor (`/usr/share/nginx/html`).
    ```bash
    docker run -d -p 8080:80 -v $PWD:/usr/share/nginx/html --name mi_nginx nginx
    ```

**¡Pruébalo!** Ve a tu navegador y entra en `http://TU_IP:8080`. ¡Verás tu mensaje personalizado!

## 💣 3. La prueba de la explosión
Vamos a demostrar que nuestros datos son inmortales.

1.  Borra el contenedor sin piedad (fíjate que usamos su nombre en lugar del ID, ¡es más fácil!):
    ```bash
    docker rm -f mi_nginx
    ```
2.  Haz un `ls` en tu terminal. Verás que tu archivo `index.html` sigue ahí, sano y salvo en tu servidor.
3.  Puedes volver a ejecutar el comando `docker run` del paso anterior y la web volverá a estar online exactamente como la dejaste, sin perder ni un solo byte de información.

## 💾 4. Los Volúmenes de Docker (Para Bases de Datos)
Cuando queremos guardar datos sensibles como una base de datos MySQL o MariaDB, es mejor dejar que Docker administre el almacenamiento.

1.  **Crea un volumen de Docker:**
    ```bash
    docker volume create mi_base_de_datos
    ```
    *(Puedes ver todos tus volúmenes ejecutando `docker volume ls`).*

2.  **Úsalo en un contenedor:**
    En lugar de poner una ruta de tu disco duro (`/home/user/...`), simplemente pones el nombre del volumen:
    ```bash
    docker run -d -v mi_base_de_datos:/var/lib/mysql --name server_db mariadb
    
```
    Ahora, aunque borres el contenedor `server_db`, todo el contenido de la base de datos quedará guardado de forma segura en el volumen `mi_base_de_datos`.

---

### 🌐 Mini-Nota sobre Redes (Docker Networks)
Si tienes un contenedor con Nginx y otro contenedor con MariaDB, ¿cómo se hablan entre ellos? 

Por defecto, los contenedores están aislados. Si quieres que se comuniquen, debes crear una red virtual:
```bash
docker network create mi_red_privada
```
Al lanzar los contenedores, les añades `--network mi_red_privada`. Una vez en la misma red, los contenedores pueden hablarse usando **sus nombres** como si fueran direcciones IP (Nginx puede hacer ping a `server_db`). ¡Pero no te preocupes por memorizar esto ahora! En el Tema 6 veremos una herramienta que automatiza todo esto por nosotros.

---
[<- Anterior: Tu primer contenedor](../03-tu-primer-contenedor/README.md) | [Volver al Módulo 9](../README.md) | [Siguiente: Creando tus propias imágenes (Dockerfile) ->](../05-creando-tus-propias-imagenes-dockerfile/README.md)