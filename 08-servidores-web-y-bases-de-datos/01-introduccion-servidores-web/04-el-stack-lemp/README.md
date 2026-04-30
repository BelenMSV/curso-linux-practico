# Tema 4: El Stack LEMP y PHP (El pegamento de la web)

Nginx es el servidor más rápido del mundo entregando archivos HTML estáticos o imágenes. Pero si entras a una tienda online, la página principal cambia dependiendo del stock, de si has iniciado sesión o de las ofertas del día. Para generar ese código HTML "al vuelo", Nginx necesita la ayuda de un lenguaje de programación. 

Aquí entra en juego **PHP**, el lenguaje con el que está construido casi el 80% de la web (incluyendo WordPress).



## ⚙️ 1. La peculiaridad de Nginx (PHP-FPM)
Si usáramos el servidor Apache, este incluye un módulo interno para procesar PHP. Nginx, obsesionado con la velocidad y la ligereza, se niega a hacer esto. 

Nginx dice: *"Yo solo sirvo archivos. Si me piden un archivo de código PHP, se lo paso a otro programa especializado para que lo procese, y que él me devuelva el resultado"*. Ese programa especializado se llama **PHP-FPM** (FastCGI Process Manager).

## 📥 2. Instalación de PHP y sus extensiones
Vamos a instalar el procesador PHP y, muy importante, el "traductor" que permite que PHP hable con nuestra base de datos MariaDB (`php-mysql`).

```bash
sudo apt update
sudo apt install php-fpm php-mysql
```
*(Nota: Al instalarlo, Linux descargará la versión más reciente disponible en sus repositorios, por ejemplo, PHP 8.1 o PHP 8.3).*

## 🔌 3. Conectando Nginx con PHP (El momento delicado)
Ahora tenemos que enseñarle a Nginx cómo pasarle los archivos a PHP-FPM. Esta es la parte donde la mayoría de los principiantes se atascan, así que vamos paso a paso.

Tenemos que editar el archivo de configuración del sitio por defecto de Nginx:

```bash
sudo nano /etc/nginx/sites-available/default
```

**Paso A: Añadir `index.php`**
Busca la línea que empieza por `index` (suele estar dentro del bloque `server {`). Añade `index.php` justo después de la palabra `index`:
```nginx
index index.php index.html index.htm index.nginx-debian.html;
```

**Paso B: Activar el procesador PHP**
Baja un poco más en el archivo hasta que veas un bloque que dice `location ~ \.php$ {`. Estará comentado con almohadillas (`#`). Tienes que borrar las almohadillas para dejarlo exactamente así:

```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
}
```
> ☢️ **¡ATENCIÓN A LA VERSIÓN!**
> En la línea `fastcgi_pass`, asegúrate de que el número de la versión de PHP coincida con el que se te ha instalado. Si tu sistema instaló PHP 8.3, esa línea debe decir `php8.3-fpm.sock`. (Puedes comprobar qué versión tienes ejecutando `php -v` en otra pestaña de tu terminal).

Guarda el archivo (Ctrl+O, Enter) y cierra nano (Ctrl+X).

**Paso C: Comprobar y recargar**
Antes de reiniciar Nginx, siempre debemos comprobar si nos hemos equivocado al escribir (un punto y coma que falte puede romper el servidor):
```bash
sudo nginx -t
```
Si te dice `syntax is ok` y `test is successful`, ¡perfecto! Recargamos Nginx para aplicar los cambios:
```bash
sudo systemctl reload nginx
```

## 🚨 4. La prueba de fuego (`info.php`)
Vamos a comprobar si todo funciona. Crearemos un archivo PHP en nuestra carpeta pública que le pedirá al servidor que nos muestre toda su información interna.

1. Crea el archivo:
   ```bash
   sudo nano /var/www/html/info.php
   ```
2. Escribe este código (es código PHP real):
   ```php
   <?php
   phpinfo();
   ?>
   ```
3. Guarda y cierra.
4. Abre tu navegador web y visita: `http://TU_DIRECCION_IP/info.php`

¡Deberías ver una página inmensa de color morado con el logo de PHP mostrando toda la configuración técnica de tu servidor! 

> ⚠️ **REGLA DE SEGURIDAD CRÍTICA:**
> Una vez que hayas visto que funciona, **BORRA ESTE ARCHIVO INMEDIATAMENTE** ejecutando `sudo rm /var/www/html/info.php`. Esta página da demasiada información a posibles atacantes sobre cómo está construido tu servidor.

---

### 🧪 Mini reto práctico: El ciclo completo (LEMP)
Vamos a crear una prueba definitiva. Vamos a escribir un pequeño script que haga que PHP se conecte a la base de datos `wordpress_db` que creamos en el Tema 3 y nos diga si la conexión fue exitosa.

1. Crea un archivo nuevo:
   ```bash
   sudo nano /var/www/html/test_db.php
   ```
2. Copia y pega este código (cambiando `secreta123` si usaste otra contraseña):
   ```php
   <?php
   $conexion = new mysqli("localhost", "wp_user", "secreta123", "wordpress_db");

   if ($conexion->connect_error) {
       echo "<h1>Error ❌</h1>";
       echo "<p>Fallo al conectar a MariaDB: " . $conexion->connect_error . "</p>";
   } else {
       echo "<h1>¡Éxito! ✅</h1>";
       echo "<p>El Stack LEMP está funcionando. PHP ha logrado conectarse a la Base de Datos MariaDB perfectamente.</p>";
   }
   ?>
   ```
3. Guarda y cierra.
4. Ve a tu navegador y entra en `http://TU_DIRECCION_IP/test_db.php`.

Si ves el mensaje verde de éxito, ¡enhorabuena! Has dominado la instalación de un entorno de producción profesional.

---
[<- Anterior: Bases de Datos (MariaDB)](../03-bases-de-datos-mariadb/README.md) | [Volver al Módulo 8](../README.md) | [Siguiente: Seguridad y SSL ->](../05-seguridad-y-certificados-ssl/README.md)