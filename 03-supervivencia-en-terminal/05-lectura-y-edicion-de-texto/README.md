# Tema 5: Lectura y Edición de Texto (Sin salir de la consola)

Ya sabemos crear archivos vacíos y moverlos de un lado a otro. Pero, ¿qué pasa si queremos leer lo que hay dentro de un documento o escribir un script? En Windows abrirías el Bloc de Notas o Word. En Linux, podemos hacerlo todo sin apartar las manos del teclado ni salir de la terminal.

## 📖 1. Leer archivos de forma rápida (`cat` y `less`)
Si solo quieres "ver" qué hay dentro de un archivo sin modificar nada, tienes dos herramientas principales:

### El comando `cat` (Para textos cortos)
El comando `cat` (de *concatenate*) toma todo el contenido de un archivo y lo "escupe" de golpe en tu pantalla.
```bash
cat mi_texto.txt
```
* **Ventaja:** Es rapidísimo.
* **Desventaja:** Si el archivo tiene 500 líneas de texto, llenará toda tu pantalla y solo verás el final. Tendrás que usar la rueda del ratón para subir.

### El comando `less` (Para textos largos)
Si el archivo es grande, `less` es tu mejor amigo. Abre el archivo en un "visor" interactivo que ocupa toda la pantalla.
```bash
less archivo_muy_largo.txt
```
* **Cómo moverte:** Usa las **flechas arriba y abajo** de tu teclado para leer línea por línea, o la barra espaciadora para avanzar página por página.
* 🚪 **¡CÓMO SALIR!** Este es un punto donde muchos principiantes se quedan atrapados. Para salir de `less` y volver al prompt de tu consola, simplemente **pulsa la tecla `q`** (de *quit*).

## ✍️ 2. Editar archivos con `nano`
Existen muchos editores de texto para la terminal (como `vim` o `emacs`), pero tienen una curva de aprendizaje muy empinada. Para empezar, usaremos **`nano`**. Es sencillo, amigable y viene instalado por defecto en casi todas las distribuciones.

Para abrir un archivo existente (o crear uno nuevo y abrirlo a la vez), simplemente escribe:
```bash
nano mis_apuntes.txt
```

### ¿Cómo funciona la interfaz de nano?
Al pulsar Enter, la consola cambiará y verás una pantalla de edición limpia. 
* Puedes escribir normalmente, usar el botón de borrar, la tecla Enter para saltar de línea y las flechas para mover el cursor.
* En la parte inferior de la pantalla verás un "menú" con opciones. Verás cosas como `^O Guardar` o `^X Salir`.
* Ese símbolo de acento circunflejo (`^`) significa que debes mantener pulsada la tecla **`Ctrl`** (Control).

### Los 3 pasos para sobrevivir en nano:
1. **Escribir:** Teclea tu texto libremente.
2. **Guardar:** Pulsa **`Ctrl + O`** (Write Out). Nano te preguntará en la parte inferior si quieres confirmar el nombre del archivo. Simplemente pulsa **Enter**.
3. **Salir:** Pulsa **`Ctrl + X`** (Exit). Volverás a la terminal normal.

## 🪄 3. El truco rápido: Escribir sin abrir un editor (`>`)
A veces solo quieres meter una línea de texto en un archivo rápido. Puedes combinar el comando `echo` (que vimos en el primer tema) con el símbolo **`>`** (redirección).

El símbolo `>` coge el texto y lo "inyecta" dentro del archivo que le digas.
```bash
echo "Esta es la primera linea de mi archivo" > rapido.txt
```
*Nota: Si usas `>` borrará lo que hubiera antes en el archivo. Si quieres añadir texto al final sin borrar lo anterior, usa doble símbolo: `>>`.*

---
### 🧪 Mini reto práctico
Vamos a crear y modificar un archivo de texto como auténticos SysAdmins:
1. Crea un archivo nuevo y ábrelo: `nano diario.txt`
2. Escribe un par de líneas ("Hola, este es mi primer texto editado en consola").
3. Guarda el archivo (`Ctrl + O`, y luego Enter).
4. Sal de nano (`Ctrl + X`).
5. Lee lo que acabas de escribir usando el comando rápido: `cat diario.txt`
6. Añade una línea extra sin usar nano: `echo "Fin del diario" >> diario.txt`
7. Vuelve a leerlo con `cat diario.txt` para comprobar que se añadió correctamente.

---
[<- Anterior: Gestión de Archivos](../04-gestion-de-archivos/README.md) | [Volver al Módulo 3](../README.md) | [Siguiente: Pidiendo Ayuda ->](../06-pidiendo-ayuda/README.md)