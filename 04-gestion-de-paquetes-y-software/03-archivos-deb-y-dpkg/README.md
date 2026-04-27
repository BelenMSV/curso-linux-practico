# Tema 3: Archivos DEB y dpkg (El "instalador" manual)

Aunque los repositorios oficiales son gigantescos, a veces querrás instalar un software muy específico o privativo que no está en la tienda (como **Google Chrome**, **Discord**, **Steam** o **TeamViewer**). 

En estos casos, las páginas web te ofrecerán descargar un archivo con extensión **`.deb`**. Este archivo es el equivalente al `.msi` o `.exe` de Windows.

## 📦 1. ¿Qué es un archivo .deb?
Un archivo `.deb` es un paquete comprimido que contiene todos los archivos del programa, su ubicación en el sistema y una lista de instrucciones sobre qué necesita para funcionar. Es el formato nativo de **Debian** (de ahí su nombre) y sus derivados como Ubuntu y Mint.

## 🛠️ 2. Cómo instalar un .deb de forma gráfica
La forma más sencilla para un principiante es usar el ratón:
1. Descarga el archivo `.deb` desde la web oficial.
2. Haz **doble clic** sobre el archivo.
3. Se abrirá el "Instalador de paquetes" (o GDebi).
4. Haz clic en **Instalar paquete** e introduce tu contraseña.

## 💻 3. Cómo instalar un .deb desde la terminal
A veces, el instalador gráfico puede fallar o simplemente queremos ser más rápidos. Aquí entra en juego la herramienta de bajo nivel llamada `dpkg` o, mejor aún, el propio `apt`.

### Opción A: Usando APT (Recomendado)
Desde las versiones recientes, `apt` puede instalar archivos locales y, lo más importante, **buscará automáticamente las dependencias que falten en internet**.

```bash
sudo apt install ./nombre-del-paquete.deb
```
*⚠️ Importante: Es necesario poner `./` delante para indicarle a Linux que el archivo está en la carpeta actual y no en los repositorios de internet.*

### Opción B: Usando dpkg
Es la herramienta tradicional de gestión de paquetes.
```bash
sudo dpkg -i nombre-del-paquete.deb
```
*(La `-i` viene de install).*



## 🧩 4. El problema de las dependencias rotas
A diferencia de los repositorios oficiales, cuando instalas un `.deb` con `dpkg`, es posible que te encuentres con un error de **"Dependencias no satisfechas"**. Esto significa que el programa necesita algo que no tienes instalado.

No entres en pánico. Linux tiene un comando "médico" para arreglar esto automáticamente:
```bash
sudo apt install -f
```
*(La `-f` significa "fix-broken").* Este comando detectará qué le falta a tu instalación manual, lo bajará de internet y terminará de configurar el programa por ti.

## 🗑️ 5. Cómo desinstalarlo
Aunque lo hayas instalado manualmente, una vez instalado, el sistema lo trata como un programa más. Puedes borrarlo con el comando que ya conoces:
```bash
sudo apt remove nombre-del-programa
```
*(Ojo: el nombre del programa puede ser distinto al nombre del archivo .deb que descargaste).*

---
### 🧪 Mini reto práctico
1. Abre el navegador en tu Máquina Virtual.
2. Ve a la página de [Google Chrome](https://www.google.com/chrome/) y descarga la versión para **64 bits .deb (para Debian/Ubuntu)**.
3. Abre la terminal y ve a tu carpeta de descargas: `cd ~/Descargas`
4. Instálalo usando apt: `sudo apt install ./google-chrome-stable_current_amd64.deb`
5. ¡Búscalo en tu menú y lánzalo!

---
[<- Anterior: El comando APT](../02-el-comando-apt/README.md) | [Volver al Módulo 4](../README.md) | [Siguiente: Formatos Universales ->](../04-formatos-universales/README.md)