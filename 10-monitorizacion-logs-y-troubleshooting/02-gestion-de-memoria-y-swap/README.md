# Tema 2: Gestión de Memoria y Swap (El salvavidas del servidor)

Imagina la memoria RAM de tu servidor como una mesa de trabajo. Cuando abres programas (Nginx, Docker, MariaDB), pones herramientas sobre la mesa. Si la mesa se llena y necesitas abrir un programa más, el sistema operativo entra en pánico. 

En Linux, cuando te quedas sin RAM al 100%, se despierta un mecanismo de emergencia llamado **OOM Killer** (Out Of Memory Killer). Este "asesino" revisa qué proceso está consumiendo más memoria y lo destruye sin piedad para salvar al sistema operativo. ¿El problema? Normalmente el proceso que más consume suele ser tu base de datos de producción.

Para evitar esta tragedia, creamos el **Swap**.

## 🧠 1. ¿Qué es el Swap?
El Swap (o espacio de intercambio) es un "engaño" al sistema. Reservamos un trozo de nuestro disco duro (que es mucho más lento que la RAM) para que actúe como memoria de emergencia. 

Cuando la RAM física se está llenando, Linux toma los programas que llevan rato sin usarse y los "mueve" al disco duro (Swap), dejando espacio libre en la RAM rápida para los procesos que están trabajando ahora mismo. Si el disco duro es SSD o NVMe, este proceso es bastante eficiente.

## 📊 2. Consultando la memoria (`free`)
Antes de crear Swap, debemos ver cuánta memoria tenemos. El comando fundamental para esto es `free`.

Ejecuta:
```bash
free -h
```
*(Recuerda: `-h` es de Human-readable, para ver Megas o Gigas).*

Fíjate en las dos filas:
*   **Mem:** Tu memoria RAM real. Presta atención a la columna `available` (es la RAM que realmente tienes disponible para abrir cosas nuevas).
*   **Swap:** Tu espacio de intercambio. Si todos los números en esta fila son `0B`, significa que tu servidor está en peligro y no tiene salvavidas.

## 🛠️ 3. Creando un archivo Swap de emergencia
Si tu fila Swap estaba a cero, vamos a arreglarlo ahora mismo creando un archivo de 2 Gigabytes.

**Paso 1: Crear un archivo vacío en el disco duro**
Vamos a usar el comando `fallocate` para crear un archivo llamado `swapfile` directamente en la raíz del sistema (`/`):
```bash
sudo fallocate -l 2G /swapfile
```
*(Si `fallocate` te da error, el comando alternativo es: `sudo dd if=/dev/zero of=/swapfile bs=1M count=2048`)*.

**Paso 2: Darle permisos de seguridad (CRÍTICO)**
Solo el usuario `root` debe poder leer este archivo, ya que podría contener contraseñas o datos sensibles volcados desde la RAM.
```bash
sudo chmod 600 /swapfile
```

**Paso 3: Formatear el archivo como Swap**
Le decimos a Linux que prepare este archivo con la estructura especial de memoria virtual:
```bash
sudo mkswap /swapfile
```

**Paso 4: Encender el salvavidas**
Activamos el Swap en el sistema:
```bash
sudo swapon /swapfile
```

**¡Comprueba tu trabajo!** Vuelve a ejecutar `free -h` o abre `htop`. Verás que ahora tienes 2 Gigas mágicos en tu sección de Swap.

## 💾 4. Haciendo el Swap permanente (El archivo fstab)
El comando `swapon` funciona al instante, pero **si reinicias el servidor, el Swap se apagará**. Para que Linux encienda el Swap automáticamente cada vez que arranca, debemos añadirlo al archivo de configuración de discos: `/etc/fstab`.

1.  Abre el archivo con Nano:
    ```bash
    sudo nano /etc/fstab
    
```
2.  Ve a la última línea vacía y añade exactamente esto:
    ```text
    /swapfile none swap sw 0 0
    
```
3.  Guarda (Ctrl+O, Enter) y sal (Ctrl+X). Tu servidor ahora está blindado contra reinicios.

## 🎛️ 5. El SysAdmin Avanzado: Ajustando el "Swappiness"
¿Cuándo debe Linux empezar a usar el disco duro? ¿Solo cuando la RAM esté al 99%? ¿O cuando esté al 60%?

Esto se controla con un valor llamado **Swappiness**, que va del 0 al 100.
*   **0:** Linux evitará usar el Swap a toda costa hasta que sea absolutamente vital.
*   **100:** Linux usará el disco duro constantemente, lo que hará el sistema muy lento.
*   **Por defecto (Ubuntu):** Suele estar en **60**.

Para ver tu valor actual:
```bash
cat /proc/sys/vm/swappiness
```

Para servidores web y bases de datos, **un valor de 60 es demasiado alto**. Queremos que la RAM se use al máximo porque es rápida, y que el disco solo se use en emergencias. Los profesionales recomiendan bajarlo a **10**.

**Para cambiarlo temporalmente:**
```bash
sudo sysctl vm.swappiness=10
```

**Para cambiarlo para siempre (sobrevive a reinicios):**
1. Abre el archivo de configuración del Kernel:
   ```bash
   sudo nano /etc/sysctl.conf
   ```
2. Añade esta línea al final del todo:
   ```text
   vm.swappiness=10
   ```
3. Guarda y cierra.

---
[<- Anterior: Monitorización de recursos](../01-monitorizacion-de-recursos/README.md) | [Volver al Módulo 10](../README.md) | [Siguiente: El sistema de logs (/var/log) ->](../03-el-sistema-de-logs-var-log/README.md)