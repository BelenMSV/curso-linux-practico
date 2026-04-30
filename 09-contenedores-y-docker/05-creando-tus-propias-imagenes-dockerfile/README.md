# Tema 5: Creando tus propias imágenes (El arte del Dockerfile)

Hasta el momento, hemos utilizado imágenes prefabricadas por la comunidad (como `nginx`, `mariadb` o `ubuntu`). Pero en el mundo real, tu trabajo será empaquetar el código que han escrito los programadores de tu empresa para que pueda ejecutarse en cualquier lugar.

Para lograr esto, Docker utiliza una "receta de cocina" llamada **Dockerfile**.

## 📝 1. ¿Qué es un Dockerfile?
Un Dockerfile es simplemente un archivo de texto sin extensión que contiene una serie de instrucciones secuenciales. Docker lee este archivo de arriba a abajo y va construyendo tu imagen personalizada "capa por capa".

### Las 5 instrucciones de oro:
1.  **`FROM`:** Es la base de tu imagen. Todo Dockerfile **debe** empezar con esta instrucción. (Ej: *Empecemos con un Ubuntu limpio*).
2.  **`RUN`:** Ejecuta comandos de Linux **durante la construcción** de la imagen. Se usa para instalar programas (Ej: `RUN apt update && apt install python3`).
3.  **`COPY`:** Copia archivos de tu servidor real (host) hacia dentro de la imagen.
4.  **`EXPOSE`:** Sirve como documentación para indicar en qué puerto va a escuchar la aplicación (Ej: `EXPOSE 80`).
5.  **`CMD`:** Es el comando que se ejecutará **cuando arranque el contenedor**. Solo puede haber un `CMD` por Dockerfile.

## 🛠️ 2. Práctica: Tu primera imagen personalizada
En el tema anterior, usamos un *Bind Mount* para inyectar una web en un contenedor Nginx vacío. Ahora vamos a hacer lo correcto para producción: vamos a **hornear** la página web directamente dentro de la imagen para que sea 100% portátil.

1.  **Crea una carpeta de trabajo limpia:**
    ```bash
    cd ~
    mkdir mi-app-docker
    cd mi-app-docker
    ```
2.  **Crea el archivo de tu web:**
    ```bash
    echo "<h1>Bienvenidos a mi Imagen Docker Personalizada 🐳</h1>" > index.html
    ```
3.  **Crea el archivo Dockerfile:**
    Abre el editor Nano:
    ```bash
    nano Dockerfile
    
```
    *(Nota: La 'D' mayúscula es importante y no tiene extensión).*
4.  **Escribe la receta:**
    Copia este código dentro del editor:
    ```dockerfile
    # 1. Usamos el servidor web ligero de Nginx basado en Alpine Linux
    FROM nginx:alpine

    # 2. Copiamos nuestra web a la ruta oficial de Nginx
    COPY index.html /usr/share/nginx/html/

    # 3. Indicamos que usaremos el puerto 80
    EXPOSE 80
    ```
    Guarda (Ctrl+O, Enter) y sal (Ctrl+X).

## 🏗️ 3. Construyendo la imagen (`docker build`)
Tenemos los ingredientes (`index.html`) y la receta (`Dockerfile`). Ahora le decimos al motor de Docker que cocine la imagen.

Ejecuta este comando prestando mucha atención al punto (`.`) del final:
```bash
docker build -t mi-servidor-web:v1 .
```

### 🧠 Anatomía del comando:
*   `docker build`: "Construye una imagen".
*   `-t mi-servidor-web:v1`: (Tag) Le damos un nombre a nuestra creación (`mi-servidor-web`) y una versión o etiqueta (`v1`).
*   `.` (Punto): Importantísimo. Le dice a Docker: *"El Dockerfile y los archivos que necesitas están en esta carpeta actual"*.

Verás cómo Docker descarga la imagen base, ejecuta la copia y termina con un mensaje de éxito. Si ejecutas `docker images`, verás tu creación en la lista. ¡Felicidades, eres un creador!

## 🚀 4. Ejecutando tu obra de arte
Tu imagen ya está guardada en el disco duro de tu servidor. Vamos a darle vida:
```bash
docker run -d -p 8080:80 --name mi_app_corriendo mi-servidor-web:v1
```

Abre tu navegador, ve a `http://TU_IP:8080` y admira tu obra. 

**¿La gran diferencia con el tema anterior?**
Si ahora te llevas esa imagen (`mi-servidor-web:v1`) a un servidor en Japón o se la pasas a un compañero de trabajo, la web funcionará **exactamente igual** sin necesidad de configurar carpetas ni mapear volúmenes. Todo va dentro de la caja.

---
[<- Anterior: Persistencia de datos](../04-persistencia-de-datos-y-redes/README.md) | [Volver al Módulo 9](../README.md) | [Siguiente: Magia con Docker Compose ->](../06-magia-con-docker-compose/README.md)