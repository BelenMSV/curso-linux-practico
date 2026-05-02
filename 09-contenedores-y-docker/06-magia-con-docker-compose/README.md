# Tema 6: Magia con Docker Compose (Orquestando la infraestructura)

Levantar un contenedor Nginx con `docker run` es fácil. Pero, ¿qué pasa si queremos desplegar un WordPress real? 
Necesitaríamos:
1. Crear una red privada en Docker.
2. Crear un volumen persistente para la base de datos.
3. Crear un volumen persistente para los archivos de WordPress.
4. Levantar el contenedor de MariaDB conectado a esa red y a ese volumen.
5. Levantar el contenedor de WordPress conectado a la misma red, enlazado a la base de datos y exponiendo el puerto 80 al exterior.

Hacer todo esto a mano cada vez que encendemos el servidor es inviable. Aquí es donde brilla **Docker Compose**: una herramienta que nos permite definir toda nuestra infraestructura en un simple archivo de texto y levantarla con un solo comando.



## 📝 1. Infraestructura como Código (IaC)
Docker Compose utiliza archivos con formato **YAML** (extensión `.yml`). 
YAML es un lenguaje súper legible para humanos basado en la indentación (los espacios a la izquierda de cada palabra). En este archivo escribiremos "qué queremos tener", y Docker Compose se encargará del "cómo hacerlo".

## 🚀 2. Práctica: WordPress + MariaDB en 1 segundo
Vamos a replicar el proyecto final del Módulo 8 (donde instalamos el Stack LEMP a mano durante horas), pero esta vez usando contenedores. Te sorprenderá la diferencia.

1.  **Crea una carpeta para el proyecto:**
    ```bash
    cd ~
    mkdir mi-wordpress-docker
    cd mi-wordpress-docker
    ```
2.  **Crea el archivo mágico:**
    ```bash
    nano docker-compose.yml
    ```
3.  **Pega la siguiente receta:**
    Presta mucha atención a la estructura. Estamos definiendo dos `services` (contenedores) y dos `volumes` (discos duros persistentes).
    
    
```yaml
    version: '3.8'

    services:
      base_de_datos:
        image: mariadb:latest
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: password_super_seguro
          MYSQL_DATABASE: wordpress_db
          MYSQL_USER: wp_user
          MYSQL_PASSWORD: secreta123
        volumes:
          - db_data:/var/lib/mysql

      sitio_web:
        depends_on:
          - base_de_datos
        image: wordpress:latest
        restart: always
        ports:
          - "8080:80"
        environment:
          WORDPRESS_DB_HOST: base_de_datos
          WORDPRESS_DB_USER: wp_user
          WORDPRESS_DB_PASSWORD: secreta123
          WORDPRESS_DB_NAME: wordpress_db
        volumes:
          - wp_data:/var/www/html

    volumes:
      db_data:
      wp_data:
    ```
    Guarda (Ctrl+O, Enter) y sal (Ctrl+X).

### 🧠 ¿Por qué esto es una obra maestra?
*   **Redes automáticas:** Fíjate que en la variable `WORDPRESS_DB_HOST` le hemos puesto `base_de_datos` (el nombre del otro servicio). Docker Compose crea una red privada automáticamente y hace que los contenedores se encuentren por su nombre. ¡Magia!
*   **`restart: always`:** Si el servidor se reinicia o se va la luz, Docker Compose volverá a encender los contenedores automáticamente al arrancar.
*   **`depends_on`:** Le dice a WordPress: *"No arranques hasta que la base de datos esté lista"*.

## 🪄 3. Las palabras mágicas (`up` y `down`)
Ya tienes la partitura, ahora vamos a dirigir la orquesta.

Asegúrate de estar en la carpeta donde está tu `docker-compose.yml` y ejecuta:
```bash
docker compose up -d
```
*(Recuerda: `-d` es para que se ejecute en segundo plano y te devuelva el control de la terminal).*

**¡Mira tu terminal!** Verás cómo Docker crea las redes, los volúmenes, descarga las imágenes y levanta la base de datos y la web en paralelo.

**¡Pruébalo!** Abre tu navegador y ve a `http://TU_IP:8080`. ¡Ahí tienes el asistente de instalación de WordPress, conectado y listo! Todo en menos de 10 segundos.

## 🛑 4. Destrucción limpia
Si alguna vez quieres apagar esta infraestructura, no tienes que ir matando contenedores uno a uno. Simplemente vuelve a la carpeta de tu proyecto y ejecuta:
```bash
docker compose down
```
Esto apagará y borrará los contenedores y la red virtual. **Pero tus datos están a salvo**, porque los volúmenes (`db_data` y `wp_data`) no se borran con este comando. Si vuelves a hacer `up -d`, tu WordPress volverá a estar exactamente como lo dejaste.

---

### 🏆 ¡Felicidades, DevOps!
Has terminado el Módulo 9. Has dado el salto evolutivo más grande del curso. 

Ahora sabes cómo aislar aplicaciones, evitar conflictos de librerías, proteger tus datos con volúmenes y desplegar ecosistemas enteros con un solo archivo de texto. Esta es la habilidad más demandada hoy en día en el sector del software. Respira hondo y prepárate para los siguientes niveles.

---
[<- Anterior: Creando tus propias imágenes](../05-creando-tus-propias-imagenes-dockerfile/README.md) | [Volver al Roadmap del Bootcamp](../README.md)