# Tema 1: Mi primer script (El comienzo de la automatización)

¡Bienvenido al mundo de la programación en Bash! Un "script" no es más que un archivo de texto plano que contiene una lista de comandos. En lugar de que tú escribas y ejecutes los comandos uno por uno, Linux lee el archivo de arriba a abajo y los ejecuta todos a la velocidad de la luz.

Vamos a crear el clásico programa "Hola Mundo" para entender la estructura básica.

## 📝 1. La anatomía de un Script
Un script en Linux suele tener la extensión **`.sh`** (de *shell*). Aunque a Linux no le importan las extensiones de archivo (podría llamarse `.txt` o no tener extensión y funcionaría igual), usar `.sh` es una buena práctica para que nosotros, los humanos, sepamos de qué trata el archivo.

### El Shebang (`#!`)
Esta es la regla de oro: **La primera línea de cualquier script de Bash debe ser siempre el Shebang.**

```bash
#!/bin/bash
```



¿Qué significa esta extraña combinación de caracteres?
* `#!` se llama "Shebang" (o Hashbang).
* `/bin/bash` es la ruta donde está instalado el programa que sabe leer los comandos.
* En resumen, esta línea le dice a Linux: *"Oye, cuando ejecutes este archivo, usa el intérprete Bash para leer las siguientes líneas"*.

## 🛠️ 2. Creando el archivo paso a paso

Vamos a crear nuestro primer script usando nuestro viejo amigo `nano` (que aprendimos en el Módulo 3).

1. Abre tu terminal.
2. Crea el archivo y ábrelo con nano:
   ```bash
   nano holamundo.sh
   ```
3. Escribe exactamente lo siguiente dentro del archivo:
   ```bash
   #!/bin/bash
   # Las líneas que empiezan por almohadilla (sin el !) son comentarios.
   # Linux ignora los comentarios, sirven para dejar notas a otros humanos.

   echo "¡Hola! Soy tu primer robot."
   ```
4. Guarda y sal (Ctrl+O, Enter, Ctrl+X).

## 🔐 3. El candado de los permisos (`chmod +x`)
Si intentas ejecutar el script ahora mismo, Linux no te dejará. ¿Por qué? ¡Por lo que aprendimos en el **Módulo 5**!

Por defecto, cuando creas un archivo de texto nuevo, Linux le da permisos de lectura y escritura (`rw-`), pero **nunca** de ejecución (`x`). Es una medida de seguridad para evitar que descargues un texto de internet y se ejecute por accidente como si fuera un virus.

Para convertir nuestro texto en un programa ejecutable, debemos darle permiso con `chmod`:

```bash
chmod +x holamundo.sh
```
*(Si haces ahora un `ls -l`, verás que el archivo seguramente ha cambiado de color en tu terminal, indicando que ahora es un ejecutable).*

## 🚀 4. Ejecutando el script (`./`)
Ya tienes el programa y tienes el permiso. Ahora hay que ejecutarlo. 

Si simplemente escribes `holamundo.sh` y pulsas Enter, la terminal te dirá que no encuentra el comando. Esto ocurre porque, por seguridad, Linux solo busca comandos en las carpetas oficiales del sistema (`/bin`, `/usr/bin`, etc.), no en la carpeta donde estás tú ahora mismo.

Para decirle a Linux "ejecuta el archivo que está *exactamente aquí*", usamos el punto y la barra inclinada (`./`):

```bash
./holamundo.sh
```

¡Boom! Deberías ver el mensaje de saludo en tu pantalla. 

---
### 🧪 Mini reto práctico
Vamos a hacer que nuestro robot sea un poco más útil. Edita tu script con `nano holamundo.sh` y modifícalo para que ejecute varios comandos de sistema seguidos:

1. Limpia la pantalla primero (`clear`).
2. Imprime un saludo (`echo "Iniciando sistema..."`).
3. Muestra la fecha y hora actual (`date`).
4. Muestra en qué carpeta te encuentras (`pwd`).

Tu código debería quedar algo así:
```bash
#!/bin/bash
clear
echo "Iniciando sistema..."
date
pwd
```

¡Guarda los cambios, ejecútalo con `./holamundo.sh` y disfruta viendo cómo tu ordenador hace cuatro tareas seguidas en una fracción de segundo!

---
[<- Volver al Módulo 6](../README.md) | [Siguiente: Variables y Entrada de Datos ->](../02-variables-y-entrada-de-datos/README.md)