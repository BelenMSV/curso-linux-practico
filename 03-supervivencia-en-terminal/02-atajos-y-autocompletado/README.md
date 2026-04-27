# Tema 2: Atajos y Autocompletado (La magia del teclado)

Uno de los mayores motivos de frustración al empezar con la terminal es escribir mal una ruta larga. Imagina querer ir a `Documentos/Proyectos/CursoLinux/Archivos` y escribir `Documetos` por error. La consola te dirá que no existe, y tendrás que volver a teclear todo.

Para evitar esto, los usuarios de Linux usamos **"la magia del teclado"**. Conoce a tus nuevos mejores amigos.

## 🪄 1. El Autocompletado (La tecla TAB)
La tecla `TAB` (Tabulador, la que está arriba de Bloq Mayús, con dos flechas) es la herramienta más importante de toda la consola. **No escribas rutas enteras nunca más.**

La Shell es inteligente y sabe qué archivos y comandos existen. Si empiezas a escribir el nombre de un archivo o carpeta y presionas `TAB`, la consola escribirá el resto por ti.

**Ejemplo de uso:**
1. Escribe: `cd Doc`
2. Presiona `TAB`.
3. La consola autocompletará mágicamente a: `cd Documentos/`

**¿Y si hay varias opciones? (El doble TAB)**
Imagina que tienes una carpeta llamada `Descargas` y otra llamada `Documentos`. Ambas empiezan por "D". 
Si escribes `D` y pulsas `TAB`, la consola no sabrá cuál quieres y no hará nada. 
*Solución:* Pulsa **`TAB` dos veces seguidas**. La consola te mostrará una lista con todas las opciones posibles. Sabiendo esto, solo tienes que añadir una letra más (ej. `De`) y volver a pulsar `TAB` para que autocomplete `Descargas/`.

## ⬆️ 2. El Historial (Flechas Arriba y Abajo)
¿Acabas de ejecutar un comando larguísimo, te dio un error por una letra, y crees que tienes que volver a escribirlo entero? Falso.

La consola guarda un historial de todo lo que escribes.
* Presiona la **Flecha Arriba** de tu teclado para ver el último comando que ejecutaste.
* Sigue presionando hacia arriba para viajar hacia atrás en el tiempo por tu historial.
* Presiona la **Flecha Abajo** para volver a los comandos más recientes.

Una vez que encuentres el comando en el historial, puedes usar las flechas de izquierda y derecha para moverte por él, corregir la letra equivocada y volver a pulsar `Enter`.

## 🛑 3. El botón de pánico (`Ctrl + C`)
Tarde o temprano, ejecutarás un comando que parece quedarse "congelado" o que empieza a imprimir miles de líneas de texto en la pantalla sin detenerse. 

Tu instinto de Windows te dirá que cierres la ventana de la terminal pulsando la X roja. **No lo hagas.** En Linux, cerrar la ventana de golpe puede interrumpir procesos importantes de mala manera.

La forma correcta, elegante y segura de cancelar o abortar cualquier comando que se esté ejecutando es el atajo:
**`Ctrl + C`** (Control + C)

*Nota: En la terminal de Linux, `Ctrl + C` NO sirve para copiar texto. Sirve para cancelar (del inglés "Cancel" o mandar una señal de interrupción).*

## 🧹 4. Limpiando el desorden (`clear` o `Ctrl + L`)
Después de ejecutar un par de comandos, tu pantalla estará llena de texto. Esto puede resultar abrumador visualmente. 

Para borrar todo y dejar tu terminal como nueva (con el prompt limpio en la parte superior), tienes dos opciones:
* Escribir el comando `clear` y pulsar Enter.
* **Atajo de teclado:** Pulsar **`Ctrl + L`**. Es muchísimo más rápido e instantáneo.

---
### 🧪 Mini reto práctico
Abre tu máquina virtual, lanza la terminal y haz lo siguiente:
1. Escribe `echo "Prueba de historial"` y pulsa Enter.
2. Pulsa la flecha arriba y cambia la palabra "historial" por "éxito".
3. Limpia la pantalla usando `Ctrl + L`.

¡Si dominas estos 4 atajos, te moverás por Linux el doble de rápido que un usuario usando el ratón!

---
[<- Anterior: Anatomía de la Consola](../01-anatomia-de-la-consola/README.md) | [Volver al Módulo 3](../README.md) | [Siguiente: Navegación de Directorios ->](../03-navegacion-de-directorios/README.md)