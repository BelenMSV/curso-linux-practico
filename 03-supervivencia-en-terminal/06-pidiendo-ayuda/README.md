# Tema 6: Pidiendo Ayuda (No tienes que memorizarlo todo)

Llegamos al final del Módulo 3 con la lección más importante de todas: **Nadie se sabe todos los comandos y modificadores de memoria**. Ni siquiera los administradores de sistemas con 20 años de experiencia. 

La diferencia entre un novato y un profesional no es cuántos comandos memoriza, sino lo rápido que sabe encontrar la respuesta. Linux tiene su propia enciclopedia integrada para ayudarte.

## 🆘 1. La ayuda rápida (`--help`)
Si recuerdas el nombre del comando (por ejemplo, `ls` o `mkdir`) pero no te acuerdas de qué letras usar para sus opciones (los modificadores), la forma más rápida de refrescar la memoria es añadir `--help` al final.

```bash
mkdir --help
```

Esto imprimirá en la pantalla un resumen rápido de cómo se usa el comando y una lista con todas las letras que puedes añadirle. 
*Nota: Es un texto corto y directo. Ideal para consultas rápidas.*

## 📖 2. El manual completo (`man`)
Si `--help` es el resumen rápido, el comando `man` (de *manual*) es la enciclopedia británica. Prácticamente todo programa instalado en Linux viene con su propia página del manual.

Para leer el manual de cualquier comando, simplemente escribe `man` seguido del comando que quieres investigar:

```bash
man ls
```

### ¿Cómo sobrevivir dentro de `man`?
Al ejecutar ese comando, la pantalla cambiará por completo y verás un documento larguísimo. Usa estas teclas para moverte:
* **Flechas Arriba/Abajo:** Bajar línea a línea.
* **Barra Espaciadora:** Bajar una página entera de golpe.
* **`/` (Barra inclinada):** Sirve para buscar una palabra. Pulsa `/`, escribe "size", pulsa Enter y te llevará a donde se hable del tamaño.
* 🚪 **`q` (Quit):** ¡El botón mágico! Cuando termines de leer, pulsa la `q` para salir del manual y volver a tu terminal.

## 🌐 3. El mundo real (Google y la comunidad)
El comando `man` es genial si no tienes internet, pero a veces su lenguaje es demasiado técnico (está escrito por programadores, para programadores).

En el mundo real, la herramienta número uno de soporte técnico es buscar en internet. Aprende a hacer las preguntas correctas:
* ❌ *Mala búsqueda:* "Cómo borrar"
* ✅ *Buena búsqueda:* "Cómo borrar una carpeta con archivos dentro en Linux consola" o "How to delete non-empty directory bash"

Páginas como **StackOverflow**, **AskUbuntu** o los foros de **Linux Mint** están llenos de gente que ha tenido exactamente tu mismo problema hace 5 años y ya lo dejó resuelto con el comando exacto que necesitas copiar y pegar.

---
### 🧪 Mini reto práctico
Vamos a poner a prueba tus habilidades de detective:
1. Usa el comando `man ls` para abrir el manual.
2. Usando las flechas, lee la descripción de lo que hace la letra `-h` (o `--human-readable`).
3. Sal del manual pulsando `q`.
4. Ahora, ve a tu carpeta personal (`cd ~`) y ejecuta este combo de letras para listar tus archivos: `ls -lah`
5. ¿Notas la diferencia en los tamaños de los archivos? ¡Ahora están en Kilobytes (K) y Megabytes (M) para que un humano los lea fácilmente!

---

### 🎉 ¡Fin del Módulo 3!
¡Felicidades! Has sobrevivido a tu inmersión en la terminal. Ahora sabes:
1. Leer el prompt de la consola.
2. Usar atajos para no escribir como un robot.
3. Navegar por carpetas con rutas relativas.
4. Crear y destruir archivos a voluntad.
5. Editar textos sin salir de la pantalla negra.
6. Pedir ayuda al sistema.

En el **Módulo 4**, usaremos esta consola para algo increíble: conectarnos a los enormes almacenes de software de Linux e instalar nuevos programas.

---
[<- Anterior: Lectura y edición de texto](../05-lectura-y-edicion-de-texto/README.md) | [Volver al Módulo 3](../README.md)