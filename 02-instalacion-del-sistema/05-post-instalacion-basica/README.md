# Tema 5: Post-instalación básica

¡Felicidades! Ya tienes Linux instalado y funcionando. Al iniciar sesión por primera vez, verás un escritorio limpio y rápido. Sin embargo, hay tres tareas fundamentales que todo usuario debe realizar inmediatamente después de la instalación para asegurar que el sistema sea seguro, estable y cómodo.

## 1. Actualización del Sistema
Aunque acabas de instalar el sistema, es muy probable que desde que se creó la imagen ISO hasta hoy se hayan publicado parches de seguridad o mejoras de programas.

1. Al entrar, es probable que aparezca automáticamente un **Gestor de Actualizaciones**.
2. Si no aparece, busca en tu menú de aplicaciones "Actualización de software".
3. Haz clic en **Instalar ahora**. El sistema te pedirá la contraseña que creaste durante la instalación.

> 💡 **Nota pro:** En Linux, casi nunca es necesario reiniciar después de actualizar, a menos que se actualice el Kernel (el corazón del sistema).

## 2. Instalación de Drivers (Controladores) adicionales
Linux incluye drivers libres para casi todo el hardware, pero para sacar el máximo rendimiento a tarjetas gráficas (como NVIDIA) o algunos chips Wi-Fi, necesitamos los drivers "propietarios".

* En Ubuntu/Mint, busca en el menú: **"Controladores adicionales"** o **"Administrador de controladores"**.
* El sistema buscará si hay algo que mejorar y te dará la opción de activarlo con un solo clic.



## 3. Optimizando la Máquina Virtual (Guest Additions)
Si estás usando **VirtualBox**, habrás notado que la pantalla de Linux se ve pequeña y no puedes redimensionarla, o que el ratón se siente un poco "lento". Esto se soluciona instalando las **Guest Additions**.

Son un conjunto de drivers especiales que permiten:
* **Pantalla completa dinámica:** Que la resolución de Linux cambie automáticamente al estirar la ventana de VirtualBox.
* **Portapapeles compartido:** Copiar un texto en tu Windows y pegarlo dentro de tu Linux (y viceversa).
* **Carpetas compartidas:** Mover archivos fácilmente entre tu ordenador real y la máquina virtual.

**Cómo instalarlas:**
1. En la ventana de VirtualBox (arriba, en el menú), ve a **Dispositivos** -> **Insertar imagen de CD de las "Guest Additions"**.
2. En Linux aparecerá un aviso de que se ha insertado un CD. Haz clic en **Ejecutar**.
3. Se abrirá una terminal pidiendo tu contraseña. Espera a que termine el proceso.
4. **Reinicia la máquina virtual.**

## 4. Un vistazo al Centro de Software
Antes de pasar al siguiente módulo donde usaremos la terminal, tómate un momento para explorar la "Tienda de aplicaciones" (Software Center). Es el equivalente a la App Store o Google Play. Desde aquí puedes instalar herramientas populares como:
* **VS Code** (Programación)
* **VLC** (Video)
* **GIMP** (Diseño)
* **Spotify** o **Discord**

---

### ✅ ¡Módulo 2 Completado!
Has pasado de no tener nada a tener un sistema operativo Linux totalmente funcional, actualizado y optimizado. 

**Resumen de lo que hemos logrado:**
1. Descargamos y verificamos una ISO.
2. Preparamos el entorno de arranque.
3. Entendimos cómo se reparte el disco.
4. Completamos el proceso de instalación.
5. Optimizamos el sistema para su uso diario.

En el **Módulo 3**, abandonaremos la comodidad de las ventanas y los clics para adentrarnos en el verdadero poder de Linux: **La Terminal**.

---
[<- Anterior: Instalación paso a paso](../04-instalacion-paso-a-paso/README.md) | [Volver al Módulo 2](../README.md)