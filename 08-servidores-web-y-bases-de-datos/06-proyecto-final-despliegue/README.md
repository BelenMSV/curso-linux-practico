# Tema 6: Proyecto Final (Desplegando WordPress desde cero)

¡Has llegado al final del Módulo 8! Tienes un sistema operativo robusto, un servidor Nginx rapidísimo, una base de datos blindada y el motor PHP listo para procesar código. 

Ahora vamos a ponerle la cereza al pastel instalando un Sistema de Gestión de Contenidos (CMS) real. No vamos a usar instaladores mágicos; lo haremos como los verdaderos administradores de sistemas: descargando el código fuente y configurándolo a mano.



## 📥 1. Limpiando el terreno y descargando el código
Primero, vamos a limpiar nuestra "plaza pública" (la carpeta de Nginx) para que no haya conflictos con nuestras pruebas anteriores, y luego descargaremos la última versión oficial de WordPress en español.

1. Ve a tu carpeta personal para trabajar cómodamente:
   ```bash
   cd ~
   ```
2. Descarga el paquete comprimido de WordPress usando `wget`:
   ```bash
   wget [https://es.wordpress.org/latest-es_ES.tar.gz](https://es.wordpress.org/latest-es_ES.tar.gz)
   ```
3. Descomprímelo usando nuestro amigo `tar`:
   ```bash
   tar -xzvf latest-es_ES.tar.gz
   ```
   *(Esto creará una nueva carpeta llamada `wordpress` con cientos de archivos dentro).*

## 🚚 2. Moviendo los archivos a producción
Ahora tenemos que trasladar todo ese código a la carpeta desde donde Nginx sirve la web.

1. Borramos el archivo `index.html` de prueba que hicimos en el Tema 2, para que Nginx lea el `index.php` de WordPress:
   ```bash
   sudo rm /var/www/html/index.html
   ```
2. Movemos todo el contenido de la carpeta `wordpress` a `/var/www/html`:
   ```bash
   sudo cp -R wordpress/* /var/www/html/
   ```

## 🔐 3. El secreto de los permisos (`www-data`)
Este paso es **crítico**. En Linux, los programas se ejecutan bajo un usuario específico por seguridad. Nginx y PHP no se ejecutan como tu usuario personal ni como `root`; se ejecutan bajo un usuario especial llamado **`www-data`**.

Si no le damos permiso a `www-data` para modificar los archivos de WordPress, no podrás subir fotos, instalar plugins ni actualizar el sistema desde la página web.

Usemos lo aprendido en el Módulo 5 (`chown` = Change Owner) para cambiar el dueño de todos los archivos de la web:
```bash
sudo chown -R www-data:www-data /var/www/html/
```
*(La bandera `-R` significa "Recursivo", es decir, cambia el dueño de la carpeta y de todo lo que haya dentro).*

## 🌍 4. La famosa instalación de los "5 minutos"
El trabajo en la terminal ha terminado. Has preparado el terreno perfectamente. Ahora WordPress toma el control.

1. Abre el navegador web en tu ordenador.
2. Escribe tu dirección IP en la barra de direcciones (ej. `http://TU_DIRECCION_IP`).
3. ¡Deberías ver el asistente de instalación de WordPress con su logo!
4. Haz clic en **"¡Vamos a ello!"**.

### 🔗 5. Conectando con MariaDB
En la siguiente pantalla, WordPress te preguntará cómo conectarse a su cerebro. Aquí es donde usamos los datos que creaste en el **Tema 3**:

* **Nombre de la base de datos:** `wordpress_db`
* **Nombre de usuario:** `wp_user`
* **Contraseña:** `secreta123` *(O la que hayas elegido)*
* **Servidor de la base de datos:** `localhost` *(Porque la base de datos está en esta misma máquina)*
* **Prefijo de la tabla:** `wp_` *(Déjalo como está)*

Si hiciste bien los pasos del Tema 3 y del Tema 4, al darle a "Enviar" verás un mensaje triunfal de WordPress diciendo que se ha podido comunicar con la base de datos.

### 🎉 6. Creando tu sitio
En la última pantalla, solo tienes que rellenar los datos de tu nueva web:
* **Título del sitio:** El que tú quieras (ej. "Mi Primer Servidor Linux").
* **Nombre de usuario:** Tu usuario para entrar al panel de WordPress (NO uses 'admin', inventa uno seguro).
* **Contraseña:** Una contraseña segura para tu web.
* **Correo electrónico:** Tu email.

Haz clic en **Instalar WordPress** y... ¡Boom! 

---

### 🏆 ¡Felicidades, SysAdmin!
Acabas de instalar, configurar y desplegar una infraestructura web profesional completa. Lo que hace unas horas era una pantalla negra sin interfaz gráfica, ahora es un servidor web capaz de publicar contenido para millones de personas en todo el mundo.

Siéntete muy orgulloso del camino recorrido. Has dominado el Stack LEMP.

---
[<- Anterior: Seguridad y SSL](../05-seguridad-y-certificados-ssl/README.md) | [Volver al Módulo 8](../README.md)