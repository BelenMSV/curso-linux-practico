# Tema 6: Troubleshooting Práctico (El Simulacro)

En el mundo militar, se entrena bajo estrés para que, cuando llegue el combate real, la memoria muscular tome el control. En la administración de sistemas hacemos exactamente lo mismo.

A este proceso de diagnóstico y resolución de problemas se le llama **Troubleshooting**.



Hoy vas a provocar dos caídas críticas en tu servidor. No intentes adivinar qué pasa; sigue las pistas, usa `systemctl`, lee los logs con `journalctl` y aplica la solución. ¡Que empiece el simulacro!

---

## 🔥 Simulacro 1: El error silencioso (Servidor Web Nginx)

Es viernes a las 17:00. Un compañero ha hecho un cambio rápido en la configuración de Nginx y ha reiniciado el servicio. De repente, todas las páginas web de la empresa se han caído.

### 1. Provoca la avería
Vamos a introducir un error tipográfico en la configuración principal de Nginx.
1. Abre el archivo de configuración:
   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```
2. Busca cualquier línea dentro del bloque `http {` (por ejemplo, `sendfile on;`) y **bórrale el punto y coma (`;`) del final**.
3. Guarda (Ctrl+O, Enter) y sal (Ctrl+X).
4. Aplica los cambios reiniciando el servicio:
   ```bash
   sudo systemctl restart nginx
   ```

### 2. Analiza los síntomas
¡Boom! El comando `restart` te devolverá un error inmediato diciendo:
`Job for nginx.service failed because the control process exited with error code.`
Nginx está muerto. Las webs están caídas.

### 3. El diagnóstico del SysAdmin
No entres en pánico. Usa tus herramientas.
1. Pregúntale a systemd qué ha pasado exactamente:
   ```bash
   sudo systemctl status nginx
   ```
   *Te dirá que falló, pero puede que no te dé el detalle exacto de la línea de código.*
2. Ve al diario avanzado para buscar la pista definitiva:
   ```bash
   sudo journalctl -u nginx -n 10
   ```
   *¡Ahí está! Deberías ver un mensaje claro de Nginx diciendo algo como: `nginx: [emerg] unexpected "}" in /etc/nginx/nginx.conf:25` (El número de línea puede variar).*

> 💡 **El truco de Nginx:** Para servidores web, antes de reiniciar a ciegas, siempre debes verificar la sintaxis de la configuración con el comando: `sudo nginx -t`. ¡Pruébalo ahora y verás cómo te señala exactamente el error!

### 4. Aplica la cura
1. Vuelve a abrir `/etc/nginx/nginx.conf`.
2. Ve a la línea que te indicó el log y vuelve a poner el punto y coma (`;`).
3. Guarda y comprueba que todo está bien: `sudo nginx -t`.
4. Reinicia el servicio: `sudo systemctl restart nginx`.
¡Emergencia resuelta!

---

## 🔥 Simulacro 2: El secuestro de datos (MariaDB)

La web de producción carga, pero todos los usuarios están viendo un error de "Error establishing a database connection". Parece que la base de datos MariaDB ha desaparecido.

### 1. Provoca la avería
En un intento de "asegurar" el servidor, un administrador novato ha cambiado los permisos de la carpeta donde MariaDB guarda todos sus datos.
1. Ejecuta este comando para cambiar el dueño de la base de datos al usuario `root`:
   ```bash
   sudo chown -R root:root /var/lib/mysql
   ```
2. Reinicia MariaDB para que el desastre surta efecto:
   ```bash
   sudo systemctl restart mariadb
   ```

### 2. Analiza los síntomas
El comando puede que tarde unos segundos y luego falle, o puede que no diga nada. Pero si compruebas el estado:
```bash
sudo systemctl status mariadb
```
Verás que está en rojo (`failed`). 

### 3. El diagnóstico del SysAdmin
MariaDB es un servicio complejo. Necesitamos leer sus logs de error para entender por qué se niega a arrancar.
1. Abre el diario de systemd específico para MariaDB:
   
```bash
   sudo journalctl -u mariadb -n 20
   ```
   *Busca con atención entre las líneas rojas. Verás mensajes parecidos a `[ERROR] mysqld: File '/var/lib/mysql/aria_log_control' not found (Errcode: 13 "Permission denied")` o `Fatal error: Can't open and lock privilege tables`.*

¡El sistema te lo está gritando! **Permission denied** (Permiso denegado). El proceso de MariaDB (que se ejecuta bajo el usuario `mysql`) está intentando leer sus propios datos, pero alguien se los ha dado al usuario `root`.

### 4. Aplica la cura
Sabiendo que es un problema de permisos en `/var/lib/mysql`, vamos a devolvérselos a su dueño legítimo.
1. Restaura los permisos:
   ```bash
   sudo chown -R mysql:mysql /var/lib/mysql
   ```
2. Vuelve a encender el motor:
   ```bash
   sudo systemctl start mariadb
   ```
3. Comprueba el pulso:
   ```bash
   sudo systemctl status mariadb
   ```
¡Verde y `active (running)`! Has salvado la empresa otra vez.

---

## 🏆 Fin del Módulo 10

¡Enhorabuena! Has completado el módulo más desafiante. 
Ya no eres alguien que simplemente copia y pega comandos de internet; ahora eres alguien que **entiende el sistema**. Sabes cómo medir su rendimiento, sabes cómo leer sus pensamientos en los logs, y sabes cómo resucitarlo cuando cae.

Estas habilidades de Troubleshooting son, sin exagerar, las que diferencian a un Junior de un Senior en cualquier entrevista técnica. ¡Disfruta de la victoria!

---
[<- Anterior: Observabilidad moderna](../05-observabilidad-prometheus-y-grafana/README.md) | [Volver al Roadmap del Bootcamp](../README.md)