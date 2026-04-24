# Tema 1: Descarga y Verificación de la Imagen ISO

Para instalar Linux, el primer paso es conseguir el sistema operativo. A diferencia de Windows, donde normalmente el sistema ya viene preinstalado en el ordenador, en el mundo Linux nosotros nos encargamos de descargar el "disco de instalación".

Este archivo de instalación se conoce como **Imagen ISO**.

## 💿 ¿Qué es una Imagen ISO?
Un archivo `.iso` es literalmente una copia exacta (una "imagen") de un disco óptico (CD o DVD). Aunque hoy en día ya casi no usamos lectores de CD, el formato se ha mantenido. Este archivo contiene todo el sistema operativo comprimido y listo para ser extraído e instalado.

## 📥 Dónde descargar Linux de forma segura
**Regla de oro:** Descarga siempre tu distribución desde la **página oficial** del proyecto. Nunca uses sitios de descargas de terceros, ya que podrían haber modificado el sistema para incluir software malicioso.

Para este curso, recomendamos encarecidamente una de estas dos opciones (ambas son excelentes para empezar):

1. **Ubuntu Desktop:**
   * Página oficial: [https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)
   * *Nota:* Busca la versión que diga **LTS** (Long Term Support). Esto significa que es una versión muy estable y con soporte garantizado por varios años.
2. **Linux Mint (Edición Cinnamon):**
   * Página oficial: [https://linuxmint.com/download.php](https://linuxmint.com/download.php)
   * *Nota:* La edición "Cinnamon" es la que ofrece la interfaz más parecida a Windows, ideal para transiciones suaves.

*El archivo que descargues pesará entre 3 GB y 4 GB, por lo que puede tardar un poco dependiendo de tu conexión a internet.*

## 🛡️ Verificación del archivo (Checksum)
Imagínate que durante la descarga (que es pesada) hay un micro-corte de internet y se pierde un pequeño fragmento del archivo. La descarga terminará, pero la ISO estará "corrupta". Si intentas instalar el sistema con ese archivo, te dará errores extraños a mitad del proceso. 

Para evitar esto, usamos el **Checksum** (Suma de comprobación). 

El Checksum es como la "huella dactilar" digital única de un archivo. En la página de descarga de Ubuntu o Mint verás un código largo llamado `SHA256`. Si calculamos la huella digital del archivo que hemos descargado en nuestro ordenador y coincide con la que publica la web oficial, sabemos que el archivo es 100% perfecto y seguro.

### ¿Cómo verificar el Checksum SHA256?

**Si estás en Windows:**
1. Abre **PowerShell** (búscalo en el menú de inicio).
2. Escribe el siguiente comando y presiona Enter (cambia la ruta por donde esté tu archivo descargado):
   ```powershell
   Get-FileHash -Path C:\Usuarios\TuUsuario\Descargas\ubuntu.iso -Algorithm SHA256
   ```
3. Compara el resultado con el de la página web.

**Si estás en macOS o Linux:**
1. Abre la **Terminal**.
2. Escribe el siguiente comando y presiona Enter:
   ```bash
   shasum -a 256 /ruta/a/tus/descargas/ubuntu.iso
   ```
*(En algunas versiones de Linux el comando es `sha256sum archivo.iso`)*

Si las letras y números coinciden exactamente, ¡enhorabuena! Tienes una imagen perfecta y lista para ser utilizada.

---
[<- Volver al Módulo 2](../README.md) | [Siguiente: Preparación del Instalador ->](../02-preparacion-del-instalador/README.md)