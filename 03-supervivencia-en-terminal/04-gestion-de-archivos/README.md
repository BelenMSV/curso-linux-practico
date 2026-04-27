# Tema 4: Gestión de Archivos (Crear, Mover y Destruir)

Ahora que ya sabes navegar por el sistema como un explorador, es hora de aprender a interactuar con el entorno. En este tema dejaremos de usar el explorador de archivos gráfico (el equivalente a "Mi PC" o "Finder") y aprenderemos a crear, duplicar y eliminar elementos directamente desde la terminal.

La sintaxis básica para casi todos estos comandos suele ser la misma: **`comando [origen] [destino]`**.

## 🏗️ 1. Crear cosas (`mkdir` y `touch`)
Antes de mover nada, vamos a crear nuestra zona de pruebas.

* **Crear una carpeta:** Usamos el comando `mkdir` (Make Directory).
  ```bash
  mkdir MisProyectos
  ```
  *Puedes crear varias carpetas a la vez separándolas por un espacio:* `mkdir fotos musica videos`

* **Crear un archivo vacío:** Usamos el comando `touch`. Es muy útil para crear rápidamente un documento de texto o un archivo de código vacío.
  ```bash
  touch notas.txt
  ```

## 📋 2. Copiar (`cp`)
El comando `cp` (Copy) hace exactamente lo que imaginas: deja el archivo original intacto y crea un clon en el destino que le digas.

* **Copiar un archivo:**
  ```bash
  cp notas.txt notas_copia.txt
  ```
  *(Esto crea una copia en la misma carpeta donde estás).*
  
  ```bash
  cp notas.txt MisProyectos/
  ```
  *(Esto copia el archivo dentro de la carpeta MisProyectos).*

* **Copiar una carpeta entera (El modificador -r):**
  Si intentas usar `cp` en una carpeta, Linux te dará un error. Las carpetas no son archivos simples, son contenedores. Para copiar una carpeta y todo lo que tiene dentro, debes usar la bandera `-r` (recursivo).
  ```bash
  cp -r MisProyectos CopiaProyectos
  ```

## 🚚 3. Mover y Renombrar (`mv`)
En Windows, "Mover" y "Cambiar nombre" son dos acciones distintas. **En Linux, son el mismo comando: `mv` (Move).**

¿Por qué? Porque para el sistema, cambiarle el nombre a un archivo es simplemente "moverlo" a la misma carpeta pero con una etiqueta diferente.

* **Mover un archivo a otra carpeta:**
  ```bash
  mv notas.txt MisProyectos/
  ```

* **Renombrar un archivo:**
  ```bash
  mv viejo_nombre.txt nuevo_nombre.txt
  ```

* **Mover y renombrar a la vez:**
  ```bash
  mv informe.pdf Documentos/informe_final.pdf
  ```

## ⚠️ 4. Borrar (`rm` y `rmdir`)
Presta mucha atención aquí. **En la terminal de Linux NO HAY PAPELERA DE RECICLAJE.** Cuando borras algo con el comando `rm` (Remove), desaparece para siempre en ese mismo milisegundo. No hay botón de deshacer.

* **Borrar un archivo:**
  ```bash
  rm notas_copia.txt
  ```

* **Borrar una carpeta vacía:**
  ```bash
  rmdir CarpetaVacia
  ```

* **Borrar una carpeta con contenido (El peligro absoluto):**
  Para borrar una carpeta que tiene archivos dentro, debes usar de nuevo el modificador `-r` (recursivo).
  ```bash
  rm -r CopiaProyectos
  ```
  
> ☢️ **El comando prohibido (`rm -rf /`):** Nunca, bajo ninguna circunstancia, ejecutes este comando, ni siquiera de broma. La bandera `-f` significa "force" (forzar, no preguntar) y la `/` es la raíz del sistema. Este comando borrará literalmente todo tu disco duro y destruirá tu sistema operativo en cuestión de segundos.

---
### 🧪 Mini reto práctico
Vamos a ponerlo todo junto. Abre tu terminal y ejecuta estos pasos uno por uno:
1. Asegúrate de estar en tu casa (`cd ~`).
2. Crea una carpeta llamada `Entrenamiento` (`mkdir Entrenamiento`).
3. Entra en esa carpeta (`cd Entrenamiento`).
4. Crea un archivo vacío llamado `secreto.txt` (`touch secreto.txt`).
5. Haz una copia del archivo y llámala `publico.txt` (`cp secreto.txt publico.txt`).
6. Renombra `publico.txt` a `borrame.txt` (`mv publico.txt borrame.txt`).
7. Elimina el archivo `borrame.txt` (`rm borrame.txt`).
8. Haz un `ls`. Solo debería quedar el archivo secreto.

---
[<- Anterior: Navegación de Directorios](../03-navegacion-de-directorios/README.md) | [Volver al Módulo 3](../README.md) | [Siguiente: Lectura y edición de texto ->](../05-lectura-y-edicion-de-texto/README.md)