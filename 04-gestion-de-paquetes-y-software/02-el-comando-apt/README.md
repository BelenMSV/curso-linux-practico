# Tema 2: El comando APT (El motor de software)

En el tema anterior vimos la "cara amable" (la tienda gráfica). Ahora vamos a abrir el capó y aprender a usar el motor que la mueve: **APT** (*Advanced Package Tool*). 

Este comando es el estándar en la familia de distribuciones **Debian** y **Ubuntu** (incluyendo Linux Mint). Dominarlo te permitirá gestionar todo tu sistema con una velocidad y precisión increíbles.

## 🔑 1. El poder de Superusuario: `sudo`
Instalar programas es una tarea de administración que afecta a todo el sistema. Por seguridad, Linux no permite que un usuario normal instale software. 
Por eso, casi todos los comandos de `apt` deben ir precedidos por la palabra **`sudo`** (*SuperUser DO*), que le dice al sistema: "Soy el administrador y autorizo esta acción". Te pedirá tu contraseña (no verás asteriscos mientras la escribes, es normal).

## 🛰️ 2. El ciclo de actualización: `update` vs `upgrade`
Este es el error más común de los principiantes. Son dos pasos distintos y necesarios:

### Paso A: `sudo apt update`
Este comando **no instala nada**. Lo que hace es descargar una "lista de precios" actualizada. Se conecta a los repositorios y mira si hay versiones nuevas de los programas que ya tienes. 
* *Hazlo siempre antes de instalar algo nuevo.*

### Paso B: `sudo apt upgrade`
Este comando es el que **descarga e instala** las actualizaciones que el paso anterior encontró. Es el que mantiene tu sistema al día.



## 📥 3. Instalar y Buscar programas
Aquí es donde `apt` brilla por su sencillez:

* **Buscar un programa:** Si no sabes exactamente cómo se llama un paquete (ej. quieres un editor de fotos).
  ```bash
  apt search gimp
  ```
* **Instalar un programa:**
  ```bash
  sudo apt install vlc
  ```
  *(Puedes instalar varios a la vez: `sudo apt install vlc gimp filezilla`)*

## 🗑️ 4. Desinstalar programas
Si ya no necesitas una herramienta, tienes dos formas de quitarla:

* **Borrar el programa:**
  ```bash
  sudo apt remove vlc
  ```
* **Borrar el programa y sus archivos de configuración:** (Limpieza total).
  ```bash
  sudo apt purge vlc
  ```

## 🧹 5. Mantener la casa limpia
A veces, al desinstalar un programa, las "dependencias" (aquellas librerías pequeñas que se instalaron automáticamente) se quedan ocupando espacio sin que nadie las use. Para limpiar esa basura, usa:

```bash
sudo apt autoremove
```

---
### 🧪 Mini reto práctico
Vamos a hacer un mantenimiento completo desde la terminal:
1. Actualiza las listas de software: `sudo apt update`
2. Instala una herramienta de dibujo llamada "Tux Paint": `sudo apt install tuxpaint`
3. Búscala en tu menú de aplicaciones y ábrela.
4. Ahora, desinstálala completamente desde la terminal: `sudo apt purge tuxpaint`
5. Limpia los restos que hayan quedado: `sudo apt autoremove`

---
[<- Anterior: Tiendas gráficas y Repositorios](../01-tiendas-graficas-y-repositorios/README.md) | [Volver al Módulo 4](../README.md) | [Siguiente: Archivos DEB y dpkg ->](../03-archivos-deb-y-dpkg/README.md)