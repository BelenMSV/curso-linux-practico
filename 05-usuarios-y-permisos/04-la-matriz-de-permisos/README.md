# Tema 4: La Matriz de Permisos (Descifrando rwx)

Si en el Módulo 3 usaste el comando `ls -l` para ver tus archivos en forma de lista, seguramente notaste que a la izquierda de cada línea aparece una extraña cadena de 10 caracteres, como por ejemplo: `drwxr-xr-x` o `-rw-r--r--`.

Esa cadena de texto no es un error de la consola; es el panel de control de seguridad más eficiente que existe. Es la **Matriz de Permisos** de Linux. Vamos a aprender a leerla como si fuera Matrix.

## 🕵️ 1. Diseccionando la cadena (Los 10 caracteres)



La cadena de 10 caracteres se divide siempre en 4 bloques muy específicos. Tomemos como ejemplo esta cadena real:
`d rwx r-x r--`

### El bloque 0: El tipo de archivo (1 carácter)
El primer símbolo a la izquierda te dice qué estás mirando:
* **`-` (Guion):** Es un archivo normal (texto, imagen, zip, etc.).
* **`d` (Directory):** Es una carpeta.
* **`l` (Link):** Es un acceso directo.

### Los 3 bloques de poder (Propietario, Grupo, Otros)
Los siguientes 9 caracteres se leen de tres en tres. Estos tripletes definen **quién** puede hacer qué.
1. **Primer triplete (`rwx`): El Propietario (User).** Los permisos del dueño del archivo.
2. **Segundo triplete (`r-x`): El Grupo (Group).** Los permisos de los miembros del grupo asignado al archivo.
3. **Tercer triplete (`r--`): Los Otros (Others).** Los permisos para el resto del mundo (cualquier persona que tenga una cuenta en el ordenador pero no sea ni el dueño ni del grupo).

## 🔠 2. ¿Qué significan las letras `r`, `w` y `x`?

Dentro de cada triplete, siempre verás estas tres letras en el mismo orden. Si ves un guion (`-`) en lugar de una letra, significa que ese permiso está **denegado**.

### En ARCHIVOS normales (ej. un .txt o un script):
* **`r` (Read - Lectura):** Permite ver el contenido del archivo (ej. usar `cat` o `less`).
* **`w` (Write - Escritura):** Permite modificar o borrar el contenido del archivo (ej. usar `nano`).
* **`x` (eXecute - Ejecución):** Permite ejecutar el archivo como si fuera un programa (vital para los scripts).

### En CARPETAS (Directorios):
Aquí la cosa cambia un poco y es vital entenderlo:
* **`r` (Read):** Permite hacer un `ls` para ver qué archivos hay dentro de la carpeta.
* **`w` (Write):** Permite crear, renombrar o borrar archivos *dentro* de la carpeta.
* **`x` (eXecute):** ¡Ojo aquí! En una carpeta, la "x" no significa ejecutar. **Significa ENTRAR**. Si una carpeta no tiene la `x`, no podrás hacer un `cd` hacia ella, aunque tengas permiso de lectura.

## 🧩 3. Ejemplos de lectura rápida

Vamos a traducir algunas cadenas comunes a lenguaje humano:

**Ejemplo 1: `-rw-r--r--`**
* Es un archivo (`-`).
* El dueño puede leer y escribir (`rw-`).
* El grupo solo puede leer (`r--`).
* El resto del mundo solo puede leer (`r--`).
*(Este es el permiso por defecto cuando creas un documento de texto. Tú puedes editarlo, los demás solo pueden mirarlo).*

**Ejemplo 2: `drwxrwx---`**
* Es una carpeta (`d`).
* El dueño puede ver, modificar y entrar (`rwx`).
* El grupo puede ver, modificar y entrar (`rwx`).
* El resto del mundo no puede hacer **absolutamente nada**, ni siquiera entrar (`---`).
*(Ideal para una carpeta compartida de un departamento de contabilidad, bloqueada para el resto de la empresa).*

**Ejemplo 3: `-rwxr-xr-x`**
* Es un archivo (`-`).
* Todos pueden leer y ejecutar (`r-x`), pero solo el dueño puede modificarlo (`rwx`).
*(Este es el permiso clásico de un programa instalado en el sistema, como el comando `ls` o el navegador web. Todos pueden usarlo, pero solo root puede modificar el código).*

---

### 🧪 Mini reto práctico
Vamos a poner a prueba tu capacidad de lectura en tu propio sistema.
1. Abre tu terminal.
2. Escribe `ls -l /` (Esto listará las carpetas principales del disco duro).
3. Fíjate en la carpeta llamada `root`.
4. Mira su cadena de permisos. Seguramente sea `drwx------`.
5. Tradúcelo en tu cabeza: Es una carpeta (`d`), el dueño tiene poder absoluto (`rwx`), pero el grupo y los demás tienen acceso totalmente denegado (`------`). ¡Por eso en el Tema 1 el sistema no te dejó entrar!

---
[<- Anterior: Gestión de Grupos](../03-gestion-de-grupos/README.md) | [Volver al Módulo 5](../README.md) | [Siguiente: Modificando Permisos y Propietarios ->](../05-modificando-permisos-y-propietarios/README.md)