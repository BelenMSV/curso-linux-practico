# Tema 3: Bases de Datos con MariaDB (El cerebro de las operaciones)

Si Nginx es la fachada de nuestro edificio, la Base de Datos es el archivero gigante que vive en el sótano. Cada vez que alguien se registra en tu web, Nginx le pasa esos datos a la base de datos para que los guarde de forma segura y ordenada.



## 🐬 1. ¿MySQL o MariaDB? (Un poco de historia)
Durante años, el rey absoluto de las bases de datos web fue **MySQL**. Sin embargo, la empresa Oracle compró MySQL y cambió algunas de sus licencias. 

El creador original de MySQL no estaba contento con esto, así que copió su propio código (que era de código abierto) y creó **MariaDB**. Hoy en día, MariaDB es la opción preferida en la mayoría de distribuciones Linux por ser 100% libre. 

*¿La buena noticia?* Los comandos son exactamente los mismos. Si sabes usar MariaDB, sabes usar MySQL.

## 📥 2. Instalación del Servidor
Vamos a instalar el motor de la base de datos en nuestro servidor:

```bash
sudo apt update
sudo apt install mariadb-server
```

Una vez instalado, comprobamos que el servicio está corriendo (igual que hicimos con Nginx):
```bash
sudo systemctl status mariadb
```
*(Si ves el texto verde `active (running)`, pulsa `q` para salir).*

## 🔐 3. Asegurando las puertas (`mysql_secure_installation`)
Recién instalado, MariaDB es un poco inseguro. Tiene usuarios anónimos de prueba y bases de datos vacías que no necesitamos en un entorno profesional. 

Para arreglar esto, los desarrolladores incluyeron un "asistente" de seguridad que te hace unas preguntas rápidas. Ejecuta:

```bash
sudo mysql_secure_installation
```

**Cómo responder al asistente:**
1.  *Enter current password for root:* Pulsa **Enter** (porque aún no hay contraseña).
2.  *Switch to unix_socket authentication?* Escribe **n** y pulsa Enter.
3.  *Change the root password?* Escribe **y** y pon una contraseña súper segura (¡y apúntala!).
4.  *Remove anonymous users?* Escribe **y** (Sí, queremos borrar a los usuarios anónimos).
5.  *Disallow root login remotely?* Escribe **y** (Por seguridad, el administrador solo debe poder entrar desde el propio servidor, no desde internet).
6.  *Remove test database and access to it?* Escribe **y** (Borramos la base de datos de prueba).
7.  *Reload privilege tables now?* Escribe **y** (Aplicamos los cambios).

¡Listo! Tu base de datos ahora es un búnker.

## 🗣️ 4. Hablando con la Base de Datos (Comandos SQL)
Para gestionar la base de datos, tenemos que entrar en su propia consola. Dentro de esta consola, los comandos de Linux (`ls`, `cd`, `mkdir`) ya no funcionan. Aquí se habla otro idioma: **SQL**.

Para entrar como superadministrador, ejecuta:
```bash
sudo mysql -u root -p
```
*(Escribe la contraseña que acabas de configurar. Notarás que el prompt de tu terminal cambia a `MariaDB [(none)]>`).*

> ☢️ **LA REGLA DE ORO DE SQL:**
> **TODOS** los comandos dentro de la consola de MariaDB deben terminar con un **punto y coma (`;`)**. Si pulsas Enter sin el punto y coma, la consola pensará que sigues escribiendo en la línea siguiente y no ejecutará nada.

## 🏗️ 5. Los 4 comandos de supervivencia
Como SysAdmin, no necesitas ser un experto programador de bases de datos, pero sí debes saber preparar el terreno para cuando instales una aplicación web. Aquí tienes la receta mágica:

1. **Crear una base de datos nueva:**
   ```sql
   CREATE DATABASE mi_proyecto;
   ```
2. **Crear un usuario y darle permiso total sobre esa base de datos:**
   *(Sustituye 'mi_usuario' y 'mi_contraseña' por los datos que quieras)*
   ```sql
   GRANT ALL ON mi_proyecto.* TO 'mi_usuario'@'localhost' IDENTIFIED BY 'mi_contraseña';
   ```
3. **Recargar los permisos para que surtan efecto:**
   ```sql
   FLUSH PRIVILEGES;
   ```
4. **Salir de la consola SQL y volver a Linux:**
   ```sql
   EXIT;
   ```

---

### 🧪 Mini reto práctico
Vamos a dejar una base de datos lista para el proyecto final que haremos al terminar este módulo (donde instalaremos WordPress).

1.  Entra en tu consola de MariaDB: `sudo mysql -u root -p`
2.  Crea una base de datos llamada `wordpress_db`.
    * *Comando: `CREATE DATABASE wordpress_db;`*
3.  Crea un usuario llamado `wp_user` con la contraseña `secreta123` y dale todos los permisos sobre `wordpress_db`.
    * *Comando: `GRANT ALL ON wordpress_db.* TO 'wp_user'@'localhost' IDENTIFIED BY 'secreta123';`*
4.  Recarga los permisos: `FLUSH PRIVILEGES;`
5.  Comprueba que la base de datos se ha creado escribiendo: `SHOW DATABASES;`
    *(Deberías ver `wordpress_db` en la lista que aparece en pantalla).*
6.  Sal de la consola con `EXIT;`.

Guarda bien el nombre de esa base de datos, el usuario y la contraseña. ¡Los vamos a necesitar muy pronto!

---
[<- Anterior: Instalación y configuración de Nginx](../02-instalacion-y-configuracion-nginx/README.md) | [Volver al Módulo 8](../README.md) | [Siguiente: El Stack LEMP y PHP ->](../04-el-stack-lemp/README.md)