# Tema 3: Tu primer contenedor (El despertar de la bestia)

El comando principal que usarás el 90% del tiempo en Docker es `docker run`. Este comando es mágico porque hace tres cosas a la vez:
1. Busca si tienes la imagen (la receta) en tu disco duro.
2. Si no la tienes, va a internet (Docker Hub) y la descarga (`pull`).
3. Crea el contenedor y lo arranca.



## 👶 1. El bautismo de fuego (`hello-world`)
La tradición manda. Vamos a ejecutar el contenedor más pequeño y famoso del mundo para comprobar que todo funciona perfectamente.

Ejecuta:
```bash
docker run hello-world
```

**¿Qué acaba de pasar?**
Verás que Docker te avisa: *"Unable to find image 'hello-world:latest' locally"*. Como no tenías la imagen, la ha descargado de internet. Luego ha arrancado el contenedor, el cual ha impreso un mensaje de bienvenida en tu terminal, ha terminado su trabajo y se ha "apagado" automáticamente.

## 🌍 2. Un servidor web en 1 segundo
El "hello-world" está bien, pero no es muy útil. Vamos a hacer algo de SysAdmins reales. Vamos a levantar el servidor web **Nginx** (el mismo que instalamos a mano en el Módulo 8), pero esta vez usando Docker.

Ejecuta esto:
```bash
docker run -d -p 8080:80 nginx
```

### 🧠 Anatomía de este comando (CRÍTICO):
* `docker run`: "Crea y arranca un contenedor".
* `-d` (**Detached**): Ejecuta el contenedor en "segundo plano" para que no bloquee tu terminal. Te devolverá un código largo (el ID del contenedor) y te dejará seguir escribiendo.
* `-p 8080:80` (**Ports**): Esto es magia pura. Le estamos diciendo: *"Conecta el puerto **8080** de mi servidor Linux real, con el puerto **80** de dentro del contenedor"*.
* `nginx`: El nombre de la imagen oficial que queremos descargar de Docker Hub.

**¡Pruébalo!** Abre el navegador web en tu ordenador y entra a la IP de tu servidor seguida del puerto 8080 (ej. `http://TU_IP:8080`). ¡Verás la página de bienvenida de Nginx! 

## 📋 3. Pasando lista (`docker ps`)
Ahora tienes un contenedor corriendo en las sombras. ¿Cómo lo vemos?

Ejecuta:
```bash
docker ps
```
*(Significa "Process Status").* Verás una tabla con tu contenedor Nginx. Fíjate en dos columnas clave:
* **CONTAINER ID:** Una cadena de letras y números (ej. `a1b2c3d4e5f6`). Es el DNI de tu contenedor.
* **NAMES:** Si no le das un nombre al contenedor, Docker se inventa uno divertido (ej. `crazy_einstein` o `sleepy_turing`).

> 💡 **Nota:** Si quieres ver **TODOS** los contenedores (incluso los que ya se han apagado, como el `hello-world`), añade la bandera `-a` (All): 
> `docker ps -a`

## 🛑 4. Detener y destruir
Un administrador debe saber limpiar su desorden. Vamos a apagar nuestro servidor web Nginx y a borrar el contenedor.

1. **Detener el contenedor:**
   Copia los primeros 3 o 4 caracteres del `CONTAINER ID` de tu Nginx (no hace falta copiarlo entero) y ejecuta:
   ```bash
   docker stop <ID_DEL_CONTENEDOR>
   ```
   *(Ejemplo: `docker stop a1b2`)*. Si recargas tu navegador, la web ya no cargará.

2. **Borrar el contenedor:**
   El contenedor está apagado, pero sigue existiendo en tu disco duro. Para destruirlo por completo, usamos `rm` (Remove):
   ```bash
   docker rm <ID_DEL_CONTENEDOR>
   ```

*(Truco: Si quieres apagar y borrar un contenedor de un solo golpe, puedes forzar el borrado de un contenedor encendido con `docker rm -f <ID>`)*.

---

### 🧪 Mini reto práctico: El contenedor interactivo (`-it`)
No todos los contenedores son servicios en segundo plano como Nginx. A veces queremos entrar *dentro* del contenedor como si fuera otra máquina virtual.

Vamos a arrancar un contenedor con **Ubuntu** puro, pero en lugar de dejarlo en segundo plano, vamos a meternos dentro de su terminal.

1. Ejecuta este comando:
   ```bash
   docker run -it ubuntu bash
   ```
   *(Las banderas `-it` significan "Interactive Terminal", y `bash` le dice qué programa ejecutar al arrancar).*
2. Fíjate en tu terminal. El prompt habrá cambiado a algo como `root@8f9a2b3c4d5e:/#`. **¡Ya no estás en tu servidor! Estás dentro de un contenedor Ubuntu aislado.**
3. Ejecuta `cat /etc/os-release` para comprobar que, en efecto, es un Ubuntu limpio.
4. Escribe `exit` y pulsa Enter.
5. El contenedor se apagará y volverás a tu querido servidor Linux.

Has creado un sistema operativo en 2 segundos, has entrado en él y lo has apagado. ¿Te das cuenta del poder que tienes ahora entre manos?

---
[<- Anterior: Instalación de Docker](../02-instalacion-de-docker/README.md) | [Volver al Módulo 9](../README.md) | [Siguiente: Persistencia de datos y volúmenes ->](../04-persistencia-de-datos-y-redes/README.md)