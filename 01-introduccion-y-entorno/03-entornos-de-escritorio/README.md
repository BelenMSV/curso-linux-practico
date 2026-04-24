# Tema 3: Entornos de Escritorio (La Capa Visual)

En Windows o macOS, el sistema operativo y lo que ves en la pantalla (las ventanas, la barra de tareas, los iconos) son una sola entidad inseparable. Si no te gusta cómo se ve la barra de tareas de Windows 11, tus opciones para cambiarla son muy limitadas. 

En Linux, la realidad es muy distinta: **la interfaz gráfica es solo un programa más que se ejecuta sobre el sistema.** Y como cualquier programa, si no te gusta, lo puedes desinstalar y cambiar por otro.

A este conjunto visual lo llamamos **Entorno de Escritorio** (Desktop Environment o DE, por sus siglas en inglés).

## 🖼️ ¿Qué incluye un Entorno de Escritorio?
Un entorno de escritorio no es solo un fondo de pantalla bonito. Es un ecosistema visual completo que incluye:
* **El Gestor de Ventanas:** El encargado de dibujar los bordes, los botones de cerrar/minimizar y permitirte arrastrar las ventanas.
* **Paneles y Menús:** Barras de tareas, menús de inicio, bandeja del sistema (donde está el reloj y el wifi).
* **Gestor de Archivos:** El equivalente al "Explorador de Windows" o "Finder" en Mac.
* **Aplicaciones base:** Calculadora, visor de imágenes, terminal gráfica, editor de texto simple, etc.

## 🏆 Los "Tres Grandes" Entornos de Escritorio
Aunque hay decenas de opciones, la mayoría de los usuarios de Linux utilizan uno de estos tres. Conocerlos te ayudará a elegir cómo quieres que se vea y se sienta tu sistema.

### 1. GNOME 👣
Es el entorno por defecto en distribuciones gigantes como Ubuntu y Fedora.
* **Estilo:** Moderno, minimalista y centrado en la productividad. No tiene una barra de tareas tradicional; en su lugar, usa una vista de "Actividades" para gestionar ventanas y buscar aplicaciones rápidamente.
* **Consumo de recursos:** Medio-Alto. Necesita un ordenador medianamente moderno para ir fluido.
* **Ideal para:** Quienes buscan una experiencia sin distracciones y diferente al paradigma clásico de Windows.

### 2. KDE Plasma ⚙️
El rey indiscutible de la personalización. 
* **Estilo:** Su diseño por defecto es muy familiar para los usuarios de Windows (menú de inicio abajo a la izquierda, barra de tareas, reloj a la derecha). Es increíblemente potente y te permite modificar hasta el último píxel, sombra o animación del sistema.
* **Consumo de recursos:** Medio (ha mejorado muchísimo en los últimos años y hoy en día es muy eficiente).
* **Ideal para:** Quienes quieren control visual absoluto y aprecian las herramientas con muchísimas opciones y configuraciones.

### 3. XFCE 🐭
El campeón de los pesos ligeros. Un entorno clásico y robusto.
* **Estilo:** Tradicional, sencillo y directo al grano. No tiene animaciones complejas ni efectos 3D, porque su objetivo es la velocidad y la estabilidad.
* **Consumo de recursos:** Muy bajo.
* **Ideal para:** Revivir ordenadores viejos (incluso de hace 10 o 15 años), instalar en máquinas virtuales con pocos recursos o para usuarios que prefieren que toda la potencia del PC vaya a sus programas y no a la interfaz visual.

## 🍦 El concepto de "Sabores" (Flavors)
Ahora que entiendes qué es una distribución y qué es un entorno de escritorio, podemos juntar los dos conceptos. 

Muchas distribuciones ofrecen diferentes versiones del mismo sistema operativo, cambiando únicamente el entorno de escritorio. A esto se le llama **"Sabores"**. 

El mejor ejemplo es Ubuntu:
* **Ubuntu:** El sistema base + entorno **GNOME**.
* **Kubuntu:** El sistema base de Ubuntu + entorno **KDE Plasma**.
* **Xubuntu:** El sistema base de Ubuntu + entorno **XFCE**.

Por debajo, todos funcionan exactamente igual, usan los mismos comandos y los mismos repositorios. Solo cambia su "ropa".

---
[<- Anterior: Distribuciones](../02-distribuciones/README.md) | [Volver al Módulo 1](../README.md) | [Siguiente: Alternativas de uso ->](../04-alternativas-de-uso/README.md)