# Tema 6: Mantenimiento y Reparación (El botiquín de Linux)

A diferencia de Windows, donde el sistema suele degradarse y volverse lento con los años requiriendo un formateo, Linux está diseñado para funcionar perfectamente durante décadas si se le da un mantenimiento mínimo.

En este tema aprenderás las tres "artes curativas" de la terminal: limpiar basura, eliminar dependencias huérfanas y reparar instalaciones a medias.

## 🧹 1. El caché de paquetes (`clean`)
Cada vez que instalas un programa desde los repositorios (con `apt install`), Linux descarga el archivo instalador (el `.deb`) de internet, lo guarda en una carpeta oculta y luego lo instala. 

El problema es que **esos archivos descargados nunca se borran**. Si llevas un año usando tu sistema, podrías tener gigabytes de archivos instaladores antiguos ocupando espacio sin motivo.

Para borrar este historial de descargas y liberar espacio en tu disco duro, usa:
```bash
sudo apt clean
```
*(Tranquilo, esto no desinstala tus programas. Solo borra los archivos temporales que se usaron para instalarlos).*

## 💔 2. Los paquetes "huérfanos" (`autoremove`)
¿Recuerdas cómo funcionan las dependencias? Cuando instalas un programa de dibujo, a lo mejor te instala 5 "mini-programas" (librerías) que necesita para funcionar.

Si un mes después decides desinstalar el programa de dibujo (usando `apt remove`), el programa principal se borra, **pero las 5 librerías se quedan instaladas**, ocupando espacio y sin que ningún otro programa las use. A esto se le llama paquetes "huérfanos".

Para decirle a Linux que busque y elimine todo lo que ya no sirve para nada:
```bash
sudo apt autoremove
```

## 🚑 3. ¡Socorro! Mi instalación se ha roto
Este es el error que más asusta a los principiantes. Imagina que estás actualizando el sistema y, de repente, se va la luz o cierras la terminal por accidente a mitad del proceso. 

Al volver a encender y intentar instalar algo, la consola te mostrará un texto rojo diciendo: *"E: No se pudo bloquear el directorio de administración"* o *"E: Hay paquetes rotos"*. **No formatees tu ordenador.**

Linux sabe que algo se quedó a medias. Solo tienes que usar uno de estos dos comandos "médicos":

**El Reparador de APT:**
```bash
sudo apt --fix-broken install
```
*(Este comando buscará qué instalación se quedó a medias, descargará lo que falte y la terminará de configurar correctamente).*

**El Reconfigurador Maestro:**
Si el error persiste, dile al sistema base de paquetes que se revise a sí mismo de arriba a abajo:
```bash
sudo dpkg --configure -a
```

---
### 🧪 Mini reto práctico
Vamos a hacerle una limpieza de primavera a tu sistema.
1. Abre tu terminal.
2. Actualiza tu lista de software por costumbre: `sudo apt update`
3. Borra el caché de archivos descargados antiguos: `sudo apt clean`
4. Comprueba si tienes programas huérfanos y bórralos: `sudo apt autoremove`
*(Si acabas de instalar el sistema, es posible que el último comando te diga que "0 paquetes han sido eliminados", ¡eso es que tu sistema ya está impoluto!)*

---
[<- Anterior: PPAs y Repositorios Externos](../05-ppas-y-repos-externos/README.md) | [Volver al Módulo 4](../README.md) | [Siguiente: Compilación Básica ->](../07-compilacion-basica-targz/README.md)