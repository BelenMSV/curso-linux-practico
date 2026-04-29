# Tema 6: Análisis de Puertos y Red (Visión de rayos X)

Has configurado tu red, te has conectado por SSH y has levantado un cortafuegos. Pero, como buen administrador, nunca debes dar por sentado lo que ocurre en tu sistema. ¿Cómo sabes exactamente qué programas están esperando conexiones de internet en este momento? 

Para descubrirlo, tenemos que hablar de los **Puertos** y aprender a auditar nuestra red.



## 🚪 1. ¿Qué es un Puerto? (La analogía del edificio)
Si la **Dirección IP** es la dirección de un edificio de apartamentos (ej. `192.168.1.50`), el **Puerto** es el número de la puerta del apartamento específico al que quieres llamar.

Un servidor tiene miles de "puertas" (exactamente 65.535 puertos posibles). Diferentes programas "escuchan" detrás de diferentes puertas:
* **Puerto 22:** Aquí suele escuchar el servidor SSH.
* **Puerto 80:** Aquí escucha el servidor Web (HTTP) para páginas normales.
* **Puerto 443:** Aquí escucha el servidor Web Seguro (HTTPS).
* **Puerto 3306:** Aquí suele escuchar una base de datos MySQL.

Si tu cortafuegos (UFW) tiene el puerto cerrado, es como si hubieras tapiado esa puerta con ladrillos: nadie puede llamar.

## 🕵️ 2. Auditando puertos con `ss` (Socket Statistics)
Durante décadas, los administradores usaron un comando llamado `netstat` para ver los puertos abiertos. Aunque aún funciona en muchos sitios, la herramienta moderna, más rápida y que viene por defecto en los Linux actuales es **`ss`**.

Si escribes `ss` a secas, verás cientos de líneas incomprensibles. Para que la información sea útil, usamos una combinación mágica de letras (banderas):

```bash
ss -tuln
```
**¿Qué significa cada letra?**
* **`-t` (TCP):** Muestra los puertos que usan el protocolo TCP (el más común y fiable).
* **`-u` (UDP):** Muestra los puertos que usan el protocolo UDP (usado para streaming o juegos).
* **`-l` (Listening):** Muestra **solo** los puertos que están "escuchando" (esperando conexiones nuevas), ignorando los que ya están ocupados.
* **`-n` (Numeric):** Muestra los números de puerto reales en lugar de intentar adivinar el nombre del servicio (ej. mostrará `22` en lugar de `ssh`).

## 📖 3. Cómo leer la salida de `ss -tuln`
Al ejecutar el comando, verás una tabla. La columna que más te interesa es **`Local Address:Port`**.

Si ves algo como:
* `0.0.0.0:22` -> Significa que el puerto 22 (SSH) está abierto y escuchando conexiones desde *cualquier* dirección de internet.
* `127.0.0.1:3306` -> Significa que la base de datos (3306) está escuchando, pero *solo* acepta conexiones internas de la propia máquina (Loopback). Nadie desde fuera puede acceder.

## 🔪 4. ¿Qué programa está usando ese puerto? (`-p`)
Si ves un puerto abierto sospechoso (ej. el puerto `8080`) y quieres saber qué programa exacto lo ha abierto, puedes añadir la letra **`-p`** (Processes) a tu comando. 

*(Nota: Para ver los procesos necesitas privilegios de administrador, así que añadimos `sudo`).*

```bash
sudo ss -tulnp
```
Ahora, al final de la línea del puerto 8080, verás algo como `users:(("python3",pid=4512,fd=3))`. ¡Misterio resuelto! Es un programa de Python.

---
### 🧪 Mini reto práctico
Vamos a levantar un servidor temporal en un puerto aleatorio y a "cazarlo" usando nuestras nuevas herramientas.

1. Abre tu terminal.
2. Vamos a decirle a Python (que viene instalado por defecto en Ubuntu) que cree un servidor web súper básico que escuche en el puerto `9000`. Ejecuta esto y **déjalo corriendo**:
   ```bash
   python3 -m http.server 9000
   ```
   *(La terminal se quedará bloqueada diciendo "Serving HTTP on 0.0.0.0 port 9000...").*
3. Abre **una segunda pestaña** o ventana de tu terminal (usualmente con `Ctrl+Shift+T`).
4. En esta nueva pestaña, ejecuta nuestro comando de auditoría:
   ```bash
   ss -tuln
   ```
   ¿Ves el puerto `:9000` en la lista en la columna Local Address?
5. Ahora vamos a identificar al culpable:
   ```bash
   sudo ss -tulnp | grep 9000
   ```
   ¡Ahí está! El comando te chivará que el proceso `python3` es el responsable.
6. Vuelve a la primera pestaña de la terminal y pulsa **`Ctrl+C`** para matar el servidor web temporal de Python.

---
[<- Anterior: Gestión de Servicios (systemd)](../05-gestion-de-servicios-systemd/README.md) | [Volver al Módulo 7](../README.md)