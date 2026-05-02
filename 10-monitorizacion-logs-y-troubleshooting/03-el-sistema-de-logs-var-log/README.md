# Tema 3: El sistema de logs (`/var/log`) (La caja negra del servidor)

Todo lo que ocurre en un servidor Linux deja un rastro. Cada vez que alguien inicia sesión, cada vez que conectas un dispositivo USB, cada vez que Nginx sirve una página web y cada vez que ocurre un error crítico, el sistema operativo escribe un mensaje de texto.

A estos mensajes se les llama **Logs** (registros), y casi todos viven en una misma carpeta: `/var/log`.

## 📁 1. Explorando el directorio sagrado
Si haces un simple `ls -l /var/log`, verás decenas de archivos y carpetas. Como SysAdmin, debes conocer de memoria los 3 archivos más importantes:

1.  **`syslog` (o `messages` en CentOS/RedHat):** Es el diario general del sistema. Casi todos los servicios y programas base de Linux escriben aquí sus avisos y errores no críticos.
2.  **`auth.log` (o `secure` en CentOS/RedHat):** El diario de seguridad. Registra cada vez que alguien intenta entrar por SSH (con éxito o fallando) y cada vez que alguien usa el comando `sudo`.
3.  **`kern.log` / `dmesg`:** Registra los mensajes del Kernel (el núcleo de Linux). Muy útil para diagnosticar problemas de hardware, discos duros rotos o fallos de red a bajo nivel.

Además, los programas grandes como servidores web o bases de datos crean sus propias subcarpetas aquí (ej. `/var/log/nginx/` o `/var/log/mysql/`).

## 🛠️ 2. Las herramientas del detective
Abrir un archivo de log que pesa 500 MB con el comando `nano` o `cat` bloqueará tu terminal y será imposible de leer. Necesitamos herramientas específicas para leer flujos de texto masivos.

### A. Para leer hacia atrás: `less`
El comando `less` te permite abrir archivos gigantes de forma instantánea porque no carga todo el archivo en la RAM, solo la parte que estás viendo.
```bash
sudo less /var/log/syslog
```
*   Usa las flechas para subir y bajar.
*   Pulsa `G` (mayúscula) para ir directamente a la última línea (lo más reciente).
*   Pulsa `/` seguido de una palabra (ej. `/error`) y dale a Enter para buscar.
*   Pulsa `q` para salir.

### B. Para buscar la aguja en el pajar: `grep`
Si sabes exactamente lo que buscas, `grep` es tu mejor amigo. Filtra el archivo y solo te muestra las líneas que contienen la palabra exacta.

¿Quieres ver quién ha usado permisos de administrador hoy?
```bash
sudo grep "sudo" /var/log/auth.log
```

### C. La herramienta definitiva en tiempo real: `tail -f`
Este es, sin lugar a dudas, **el comando que más vas a usar en toda tu carrera como SysAdmin o DevOps**.

El comando `tail` muestra las últimas 10 líneas de un archivo. Pero si le añades la bandera `-f` (Follow), la terminal se queda "enganchada" al archivo y **te muestra las nuevas líneas en tiempo real según van ocurriendo**.
```bash
sudo tail -f /var/log/syslog
```
*(Para salir de este modo de vigilancia, pulsa `Ctrl+C`).*

## 🕵️‍♀️ 3. Práctica: Cazando intrusos en vivo
Vamos a comprobar cómo funciona el registro de seguridad en tiempo real. Para esto vas a necesitar tener tu terminal conectada al servidor, y abrir una segunda terminal (o usar tu móvil/otro PC) para simular un ataque.

**Paso 1: Pon al vigilante a observar**
En tu terminal principal, ejecuta:
```bash
sudo tail -f /var/log/auth.log
```
*(Verás las últimas conexiones, y el cursor se quedará parpadeando esperando nuevos eventos).*

**Paso 2: Simula un ataque**
Abre una **segunda** ventana de terminal en tu ordenador (o desconéctate de la actual abriendo otra pestaña si usas un cliente SSH) e intenta conectarte a tu servidor usando un usuario falso y una contraseña inventada:
```bash
ssh hacker@TU_IP_DEL_SERVIDOR
```

**Paso 3: Observa la trampa**
Vuelve a mirar tu primera terminal (la que tiene el `tail -f` corriendo). Verás que instantáneamente ha aparecido una nueva línea que dice algo como:
`Invalid user hacker from <TU_IP_REAL> port 54321`
`Connection closed by invalid user hacker`

¡Acabas de ver un evento de seguridad en el mismo milisegundo en el que ocurrió!

## 🚧 4. Rotación de Logs (¿Por qué el disco no se llena?)
Si Linux registra absolutamente todo, ¿por qué el disco duro no se llena de logs infinitos?

Porque Linux usa un programa llamado **`logrotate`**. Todos los días a medianoche, este programa coge el archivo `syslog`, lo comprime en un archivo `.gz` (ej. `syslog.1.gz`), y crea un `syslog` nuevo y vacío. Cuando hay demasiados archivos comprimidos antiguos (por ejemplo, más de 7 días), borra el más viejo.

Si haces un `ls -l /var/log`, verás todos esos archivos `.gz` comprimidos. Si alguna vez necesitas buscar un error que ocurrió hace 3 días, tendrás que usar `zgrep` (un grep especial para archivos comprimidos) en lugar de `grep` normal.

---
[<- Anterior: Gestión de Memoria y Swap](../02-gestion-de-memoria-y-swap/README.md) | [Volver al Módulo 10](../README.md) | [Siguiente: Dominando journalctl ->](../04-dominando-journalctl/README.md)