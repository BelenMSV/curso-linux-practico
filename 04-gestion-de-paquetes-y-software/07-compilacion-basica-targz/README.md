# Tema 7: Compilación Básica (El nivel avanzado)

Llegamos al final del módulo con la técnica más antigua y pura de instalar software en Linux. A veces encontrarás un programa increíble en GitHub que no está en la tienda de Ubuntu, no tiene un archivo `.deb`, ni Snap, ni Flatpak. El creador simplemente ha subido un archivo **`.tar.gz`** que contiene el "código fuente" (el texto escrito por los programadores).

Para que tu ordenador entienda ese texto, tienes que traducirlo a lenguaje de máquina (ceros y unos). A ese proceso se le llama **Compilar**.

## 🛠️ 1. Preparando el laboratorio (`build-essential`)
Antes de poder compilar nada, necesitas las herramientas adecuadas (los "traductores"). En Ubuntu y Mint, todas estas herramientas vienen agrupadas en un súper-paquete llamado `build-essential` (que incluye lenguajes como C o C++ y herramientas como `make`).

Instálalo una vez en tu vida y olvídate:
```bash
sudo apt install build-essential
```

## 📦 2. Extraer el código (`tar`)
El archivo `.tar.gz` es el equivalente de Linux a un archivo `.zip` o `.rar`. Para descomprimirlo desde la terminal, usamos el comando `tar` con unas letras mágicas:

```bash
tar -xzvf nombre-del-archivo.tar.gz
```
* **x**: Extraer.
* **z**: Porque está comprimido en formato gzip.
* **v**: Verbose (para ver en pantalla los archivos que van saliendo).
* **f**: Archivo (File).

## 🧪 3. La Santísima Trinidad de la Compilación
Una vez extraído, entra en la carpeta que se acaba de crear (`cd nombre-de-la-carpeta`). Dentro suele haber cientos de archivos, pero tú solo vas a ejecutar tres comandos en este orden estricto:

### Paso 1: `./configure`
Este comando revisa tu ordenador. Comprueba si tienes el procesador correcto, la memoria suficiente y las librerías necesarias. 
```bash
./configure
```
*Si te da un error aquí, suele ser porque te falta instalar alguna librería que el programa necesita.*

### Paso 2: `make`
Aquí ocurre la magia. Este comando lee el código y empieza a construir el programa real.
```bash
make
```
*Este paso puede tardar desde unos segundos hasta horas, dependiendo de si estás compilando una calculadora o un navegador web entero. Verás miles de líneas de texto pasar a toda velocidad por tu pantalla.*

### Paso 3: `sudo make install`
El paso anterior creó el programa terminado, pero lo dejó dentro de tu carpeta de descargas. Para que el sistema lo reconozca como un programa oficial y puedas abrirlo desde cualquier sitio, hay que moverlo a las carpetas del sistema.
```bash
sudo make install
```
*(Usamos `sudo` porque estamos escribiendo en las carpetas protegidas del disco duro).*

## 📖 4. La regla de oro: Lee el README
Lo explicado arriba es la forma estándar que usan el 90% de los programas en C/C++. Sin embargo, si el programa está escrito en otros lenguajes (como Python, Node.js o Rust), los comandos serán diferentes.

**Siempre, absolutamente siempre**, después de descomprimir el archivo, haz un `ls` y busca un archivo llamado `README` o `INSTALL`. Léelo con el comando `cat` o `less`, porque ahí el creador te explica los comandos exactos que debes usar.

---
### 🧪 Mini reto práctico
Vamos a practicar la descompresión sin romper nada. No vamos a compilar un programa real porque tardaría mucho, pero vamos a dominar el `.tar.gz`.
1. Ve a tu carpeta de inicio (`cd ~`).
2. Descarga un código fuente pequeño directamente desde la terminal con este comando (`wget` sirve para descargar cosas de internet):
   `wget http://ftp.gnu.org/gnu/hello/hello-2.10.tar.gz`
3. Descomprímelo: `tar -xzvf hello-2.10.tar.gz`
4. Entra en la carpeta nueva que se ha creado: `cd hello-2.10`
5. Haz un `ls` y comprueba la cantidad de archivos que hay. Busca el archivo `README` y léelo con `cat README`.

*(Si te sientes valiente, puedes intentar hacer `./configure`, luego `make` y luego ejecutar `./hello` para ver qué hace el programa).*

---
[<- Anterior: Mantenimiento y Reparación](../06-mantenimiento-y-reparacion/README.md) | [Volver al Módulo 4](../README.md)