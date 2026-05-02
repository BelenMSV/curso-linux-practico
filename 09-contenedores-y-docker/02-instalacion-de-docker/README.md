# Tema 2: Instalación de Docker (Preparando el motor)

En el módulo de gestión de paquetes aprendimos que `apt` es nuestro mejor amigo. Sin embargo, si instalamos Docker directamente con `sudo apt install docker`, Linux nos instalará una versión antigua mantenida por la comunidad. 

Como buenos administradores de sistemas, vamos a conectar nuestro servidor directamente a los **repositorios oficiales de Docker** para tener la versión de grado empresarial (Docker Community Edition o Docker CE).

## 🧹 1. Limpieza previa
Por si acaso el sistema trae alguna versión residual o conflictiva instalada por defecto, lo primero es limpiar la casa. Ejecuta este comando para desinstalar paquetes antiguos:
```bash
sudo apt remove docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc
```
*(Si te dice que no encontró ninguno de esos paquetes, ¡perfecto! Tu sistema ya estaba limpio).*

## 🔑 2. Añadiendo las llaves de seguridad
Para que nuestro Linux confíe en los servidores de Docker y descargue su código, necesitamos descargar su llave criptográfica (GPG key) oficial.

1. Actualizamos el sistema e instalamos unas herramientas previas necesarias para descargar datos de internet de forma segura:
   ```bash
   sudo apt update
   sudo apt install ca-certificates curl gnupg
   ```
2. Creamos una carpeta segura para guardar la llave de Docker:
   ```bash
   sudo install -m 0755 -d /etc/apt/keyrings
   ```
3. Descargamos la llave oficial:
   ```bash
   curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
   ```
4. Le damos permisos de lectura a la llave:
   ```bash
   sudo chmod a+r /etc/apt/keyrings/docker.gpg
   ```

## 📦 3. Añadiendo el Repositorio Oficial
Ahora le decimos a `apt` dónde encontrar el software de Docker. Este comando detecta automáticamente tu versión de Linux y añade la dirección correcta:
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## ⚙️ 4. Instalación de Docker Engine
Con el repositorio configurado, actualizamos la lista de paquetes y, por fin, instalamos el motor principal, su interfaz de comandos y los plugins necesarios:

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

> 🟢 **Comprobación del servicio:**
> Docker funciona en segundo plano como un demonio (`daemon`). Asegúrate de que está activo usando nuestro viejo amigo `systemctl`:
> ```bash
> sudo systemctl status docker
> ```
> *(Si dice `active (running)`, pulsa la letra `q` para salir).*

## 🔐 5. El truco del SysAdmin: El grupo `docker`
Si intentas ejecutar un comando de Docker ahora mismo (por ejemplo, `docker ps`), el sistema te dará un error de **"Permission denied"** (Permiso denegado). 

Esto ocurre porque el demonio de Docker tiene tanto poder sobre el sistema operativo que, por seguridad, **solo el usuario `root` (o usando `sudo`) puede darle órdenes.**

Escribir `sudo` antes de cada comando de Docker es agotador. Para evitarlo, vamos a añadir a tu usuario actual al grupo de usuarios privilegiados llamado `docker`:
```bash
sudo usermod -aG docker $USER
```

> ⚠️ **¡Pausa crítica!**
> Para que Linux reconozca que ahora perteneces a ese grupo, **tienes que cerrar tu sesión y volver a entrar**. 
> * Escribe `exit` para cerrar tu terminal (o tu conexión SSH).
> * Vuelve a abrir la terminal / reconéctate.

## 🏁 6. La prueba final
Una vez que hayas vuelto a entrar a tu sesión, ejecuta este comando para pedirle a Docker su versión (fíjate que ya no usamos `sudo`):

```bash
docker --version
```

Si te responde algo como `Docker version 24.0.5, build 12345`... ¡Felicidades! Tienes el motor de contenedores más potente del mundo ronroneando en tu servidor y listo para recibir órdenes.

---
[<- Anterior: ¿Qué es Docker?](../01-que-es-docker/README.md) | [Volver al Módulo 9](../README.md) | [Siguiente: Tu primer contenedor ->](../03-tu-primer-contenedor/README.md)