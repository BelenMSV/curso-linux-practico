# Tema 5: Modificando Permisos y Propietarios (`chmod` y `chown`)

Ahora que ya sabes leer la matriz de permisos (`rwx`), es hora de aprender a reescribirla. En este tema aprenderás a transferir la propiedad de un archivo de un usuario a otro, y a abrir o cerrar el "candado" de los permisos.

## 👑 1. Cambiar de dueño (`chown`)
La palabra `chown` proviene de *Change Owner* (Cambiar Dueño). Como transferir la propiedad de un archivo es un acto delicado, **casi siempre necesitarás usar `sudo`**.

La sintaxis básica es: `sudo chown nuevo_usuario nombre_archivo`

Pero el verdadero poder de `chown` es que te permite cambiar el dueño y el grupo al mismo tiempo, separándolos por dos puntos (`:`).

**Ejemplos:**
* Cambiar solo el dueño a "pedro":
  ```bash
  sudo chown pedro proyecto.txt
  ```
* Cambiar el dueño a "pedro" y el grupo a "desarrolladores":
  ```bash
  sudo chown pedro:desarrolladores proyecto.txt
  ```
* Cambiar el dueño de una **carpeta y todo lo que hay dentro** (Usando la bandera recursiva `-R`):
  ```bash
  sudo chown -R pedro:desarrolladores /home/pedro/MisProyectos
  ```

## 🔐 2. Cambiar permisos: El Modo Simbólico (`chmod`)
La palabra `chmod` proviene de *Change Mode* (Cambiar Modo). Hay dos formas de usarlo. La primera es el modo simbólico, que usa letras y signos matemáticos. Es ideal para hacer cambios rápidos.

**La fórmula es: ¿A QUIÉN? + ¿QUÉ ACCIÓN? + ¿QUÉ PERMISO?**

* **¿A quién?:** `u` (dueño/user), `g` (grupo), `o` (otros), `a` (todos/all).
* **Acción:** `+` (Añadir), `-` (Quitar), `=` (Establecer exactamente).
* **Permiso:** `r`, `w`, `x`.

**Ejemplos rápidos:**
* Dar permiso de ejecución al dueño: `chmod u+x script.sh`
* Quitar permiso de escritura a los "otros": `chmod o-w documento.txt`
* Quitar todos los permisos al grupo y a los demás de golpe: `chmod go-rwx secreto.txt`

## 🔢 3. Cambiar permisos: El Modo Numérico (El método Pro)
Escribir letras está bien, pero los administradores de sistemas usamos el "Modo Octal". Se basa en sumar números. En lugar de escribir `rwx`, le asignamos un valor a cada letra:

* **Lectura (`r`) = 4**
* **Escritura (`w`) = 2**
* **Ejecución (`x`) = 1**
* *(Sin permiso (`-`) = 0)*



Para saber qué permiso poner, simplemente **sumas los números**.
* Si quieres `rwx` (Lectura, escritura y ejecución): 4 + 2 + 1 = **7**
* Si quieres `rw-` (Lectura y escritura): 4 + 2 = **6**
* Si quieres `r--` (Solo lectura): 4 + 0 = **4**
* Si no quieres dar ningún permiso `---`: **0**

Como la matriz de permisos tiene 3 bloques (Dueño, Grupo, Otros), **el comando `chmod` necesita 3 números**.

**Ejemplos clásicos que debes memorizar:**
* `chmod 755 archivo`
  * Dueño (7): `rwx` (Puede hacer todo).
  * Grupo (5): `r-x` (Leer y ejecutar, pero no modificar).
  * Otros (5): `r-x` (Leer y ejecutar, pero no modificar).
  * *(Ideal para carpetas públicas o scripts compartidos).*

* `chmod 644 archivo`
  * Dueño (6): `rw-` (Leer y escribir).
  * Grupo (4): `r--` (Solo leer).
  * Otros (4): `r--` (Solo leer).
  * *(El estándar de seguridad para documentos normales y fotos).*

> ☢️ **El Peligro del 777:** Si alguna vez ejecutas `chmod 777 archivo`, le estás dando poder absoluto (7) al dueño, al grupo y a cualquier persona que pase por ahí. **Jamás uses 777** en un servidor de producción para "arreglar un problema de permisos"; es un agujero de seguridad masivo.

---

### 🧪 Mini reto práctico
Vamos a crear un "programa" y a darle permisos para poder ejecutarlo.
1. Crea un archivo vacío llamado `lanzador`: `touch lanzador`
2. Mira sus permisos por defecto: `ls -l lanzador`. Seguramente sea `-rw-rw-r--` (664).
3. Escribe algo de código dentro. Usa este comando rápido: 
   `echo 'echo "¡El programa funciona!"' > lanzador`
4. Intenta ejecutarlo tecleando: `./lanzador`
   *(Te dará un error de "Permiso denegado" porque no tienes la 'x').*
5. Dale permisos de ejecución usando el modo numérico para que el dueño haga todo (7) y el resto no haga nada (00):
   `chmod 700 lanzador`
6. Vuelve a intentar ejecutarlo: `./lanzador`. ¡Ahora sí!

---
[<- Anterior: La Matriz de Permisos](../04-la-matriz-de-permisos/README.md) | [Volver al Módulo 5](../README.md) | [Siguiente: Práctica - Carpeta Compartida ->](../06-practica-carpeta-compartida/README.md)