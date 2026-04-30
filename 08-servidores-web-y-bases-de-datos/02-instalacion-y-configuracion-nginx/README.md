# Tema 2: Instalación y configuración de Nginx (Tu primera web al mundo)

La teoría está muy bien, pero Linux se aprende escribiendo en la terminal. Vamos a instalar Nginx, a abrir las puertas de nuestro cortafuegos y a entender dónde guarda Linux los archivos que la gente verá en internet.

## 🛠️ 1. Instalación de Nginx
Como Nginx es un estándar de la industria, está perfectamente integrado en los repositorios oficiales de Ubuntu y Mint. Su instalación requiere los clásicos comandos del Módulo 4:

```bash
sudo apt update
sudo apt install nginx
```
*(Pulsa 'Y' o 'S' si te pide confirmación para descargar los paquetes).*

## 🛡️ 2. Abriendo las puertas (UFW)
En el Módulo 7 aprendimos a usar el cortafuegos `ufw`. Si lo tienes activado, en este momento nadie puede ver tu web porque el puerto 80 (HTTP) está cerrado por seguridad.

Afortunadamente, al instalar Nginx, este registra automáticamente unos perfiles en UFW para facilitarnos la vida. Podemos verlos con:
```bash
sudo ufw app list
```

Verás que aparecen opciones como `Nginx HTTP`, `Nginx HTTPS` y `Nginx Full`. Vamos a permitir el tráfico completo (HTTP normal y el seguro HTTPS) y a recargar el cortafuegos:

```bash
sudo ufw allow 'Nginx Full'
sudo ufw reload
```

## 🟢 3. Comprobando el motor (`systemctl`)
Nginx es un "demonio" (un servicio en segundo plano). Vamos a usar lo que aprendimos sobre `systemd` para comprobar que está encendido y funcionando correctamente:

```bash
sudo systemctl status nginx
```
Si ves un texto en verde que dice **`active (running)`**, ¡enhorabuena! Tienes un servidor web funcionando en tu máquina. Pulsa `q` para salir de esa pantalla.

## 🌍 4. La gran prueba: ¡Míralo en tu navegador!
Es hora de ver el resultado. 
1. Si no recuerdas tu IP, averíguala escribiendo `ip a` en tu terminal (busca la línea `inet`, por ejemplo `192.168.1.50`).
2. Abre tu navegador web favorito (Chrome, Firefox, etc.) en tu ordenador.
3. Escribe esa dirección IP en la barra de direcciones y pulsa Enter.

¡Deberías ver una pantalla que dice **"Welcome to nginx!"**! Tu servidor web está sirviendo su primera página al mundo.



## 📁 5. ¿Dónde vive tu web? (La anatomía de Nginx)
Para poder modificar esa página de bienvenida y subir la tuya propia, necesitas saber cómo organiza Nginx sus archivos en el disco duro. Hay dos rutas que un SysAdmin debe tatuarse en la memoria:

* **`/var/www/html/` (La plaza pública):** Aquí es donde se guardan los archivos reales de tu página web (los `.html`, las fotos, los `.css`). Todo lo que pongas en esta carpeta, el mundo podrá verlo.
* **`/etc/nginx/` (La sala de máquinas):** Aquí NO van las fotos ni el código de tu web. Aquí van los archivos de configuración del propio Nginx. Por ejemplo, en `/etc/nginx/sites-available/` configuraremos más adelante si queremos alojar múltiples páginas web (como `miweb.com` y `mi-otra-web.com`) en este mismo servidor.

---

### 🧪 Mini reto práctico
Vamos a "hackear" nuestra propia página de bienvenida. Queremos quitar el aburrido mensaje de Nginx y poner algo nuestro.

1. Ve a la carpeta pública del servidor:
   ```bash
   cd /var/www/html
   ```
2. Si haces un `ls`, verás que hay un archivo llamado `index.nginx-debian.html` (o simplemente `index.html`). Ese es el archivo que estás viendo en tu navegador.
3. Vamos a borrar ese archivo (requiere `sudo` porque la carpeta pertenece a `root` de momento):
   ```bash
   sudo rm index*.html
   ```
4. Ahora, vamos a crear nuestro propio archivo con una sola línea de código usando `nano`:
   ```bash
   sudo nano index.html
   ```
5. Escribe dentro algo divertido, por ejemplo:
   ```html
   <h1>¡Hola Mundo! Este es mi propio servidor Linux.</h1>
   <p>El Módulo 8 está en marcha.</p>
   ```
6. Guarda (Ctrl+O, Enter) y sal (Ctrl+X).
7. Ve a tu navegador web, recarga la página (F5)... ¡y admira tu creación!

---
[<- Anterior: Introducción a Servidores Web](../01-introduccion-servidores-web/README.md) | [Volver al Módulo 8](../README.md) | [Siguiente: Bases de datos (MariaDB) ->](../03-bases-de-datos-mariadb/README.md)