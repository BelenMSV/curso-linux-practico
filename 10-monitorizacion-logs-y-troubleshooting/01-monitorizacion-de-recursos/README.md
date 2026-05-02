# Tema 1: Monitorización de recursos (Tomando las constantes vitales)

Cuando un servidor va lento, el primer instinto de un novato es reiniciarlo. El instinto de un SysAdmin es averiguar **por qué** va lento. ¿Es la CPU que está al 100%? ¿Nos hemos quedado sin memoria RAM? ¿El disco duro está lleno?

En este tema aprenderemos las cuatro herramientas fundamentales de la terminal para responder a estas preguntas en segundos.

## 🫀 1. El pulso del sistema: `top` y `htop`

Estas herramientas nos muestran qué programas (procesos) se están ejecutando en tiempo real y cuánta CPU o RAM están consumiendo.

### El clásico: `top`
Viene preinstalado en absolutamente todas las distribuciones de Linux del mundo. Ejecuta en tu terminal:
```bash
top
```
*(Para salir, pulsa la letra `q`).*

Es útil en emergencias, pero su interfaz es de los años 90 y puede ser difícil de leer. Fíjate en la primera línea, donde dice **"load average"** (carga media). Son tres números que representan la carga de la CPU en el último minuto, en los últimos 5 minutos y en los últimos 15 minutos. Si tienes 1 núcleo de CPU y el número es `1.00`, significa que tu procesador está al 100% de capacidad.

### La evolución moderna: `htop`
`htop` es la versión vitaminada, a color y mucho más interactiva. Normalmente hay que instalarlo:
```bash
sudo apt update
sudo apt install htop
```

Ejecútalo:
```bash
htop
```


**¿Cómo usar htop?**
*   **Barras superiores:** Te muestran de forma visual (con barras de colores) el uso de cada núcleo de tu CPU, el uso de memoria RAM (Mem) y la memoria Swap (Swp).
*   **Navegación:** Puedes usar las **flechas arriba/abajo** de tu teclado para moverte por los procesos.
*   **Ordenar:** Si pulsas `F6` (o haces clic con el ratón, ¡sí, el ratón funciona en htop!), puedes ordenar la lista para ver qué proceso consume más `%CPU` o más `%MEM`.
*   **Matar procesos:** Si un proceso se ha quedado colgado, selecciónalo con las flechas, pulsa `F9` (Kill), presiona Enter y lo fulminarás.
*   *(Para salir, pulsa `F10` o la letra `q`).*

## 💾 2. ¿Cuánto espacio queda? (`df`)

Llenar el disco duro al 100% es la causa número uno de caídas catastróficas en bases de datos. Para ver cuánto espacio libre nos queda, usamos el comando `df` (Disk Free).

Ejecuta:
```bash
df -h
```
*(La bandera `-h` significa "Human readable". Si no la pones, te mostrará el tamaño en bloques de bytes incomprensibles. Con `-h` te lo muestra en Megabytes (M) y Gigabytes (G)).*

**¿En qué fijarse?**
Busca la línea que en la columna "Mounted on" diga `/` (la raíz de tu sistema). Mira la columna **Use%** (Porcentaje de uso). Si está por encima del 90%... ¡peligro!

## 🕵️‍♂️ 3. ¿Quién se está comiendo el disco? (`du`)

Vale, `df` nos dice que el disco está casi lleno. Pero, ¿qué carpeta o archivo es el culpable? Para eso usamos `du` (Disk Usage).

Si ejecutas `du` a secas, te imprimirá miles de líneas. Necesitamos ser más precisos. El combo definitivo del SysAdmin para encontrar al culpable es este:

1.  Ve a la carpeta raíz:
    ```bash
    cd /
    ```
2.  Ejecuta este comando (puede tardar un poco y darte algunos errores de "Permiso denegado", es normal):
    ```bash
    sudo du -sh * | sort -h
    ```

### 🧠 Anatomía del comando mágico:
*   `sudo du`: Ejecuta Disk Usage como administrador para poder leer todas las carpetas.
*   `-s`: (Summarize) Solo dame el total de la carpeta, no me listes cada archivo dentro de ella.
*   `-h`: (Human readable) Muéstralo en Megas o Gigas.
*   `*`: Analiza todo lo que hay en la carpeta actual.
*   `| sort -h`: Coge todos esos resultados y ordénalos de menor a mayor tamaño.

Al final de la lista verás las carpetas más pesadas. Normalmente, los culpables suelen estar dentro de `/var/log` (archivos de registro gigantes) o `/var/lib/docker` (demasiadas imágenes de contenedores sin borrar).

---

### 🧪 Mini reto práctico: El detective de carpetas
Vamos a poner en práctica lo aprendido para investigar tu propio sistema:

1. Ve a la carpeta `/var` (`cd /var`).
2. Usa el "comando mágico" que acabamos de aprender para ver qué subcarpeta dentro de `/var` es la que más pesa.
3. Ahora entra en esa subcarpeta pesada y vuelve a lanzar el comando. ¡Repite el proceso hasta encontrar los archivos específicos que están ocupando más espacio!

---
[<- Volver al Módulo 10](../README.md) | [Siguiente: Gestión de Memoria y Swap ->](../02-gestion-de-memoria-y-swap/README.md)