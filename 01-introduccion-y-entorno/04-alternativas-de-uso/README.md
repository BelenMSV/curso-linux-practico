# Tema 4: Alternativas de Uso (Cómo probar Linux sin romper nada)

Una de las mayores barreras de entrada para los principiantes es el miedo a perder sus archivos o estropear su instalación de Windows o macOS. Afortunadamente, la tecnología ha avanzado muchísimo y hoy en día instalar Linux como sistema único (borrando todo el disco duro) es solo una de muchas opciones.

En este tema repasaremos las formas más populares de utilizar Linux, desde las más conservadoras hasta las más avanzadas.

## 🚀 1. Modo "Live USB" (Probar sin compromiso)
La mayoría de las distribuciones modernas (como Ubuntu o Linux Mint) te permiten crear un pendrive arrancable ("booteable"). 

Cuando enciendes tu ordenador con ese USB conectado, el sistema operativo completo se carga directamente en la memoria RAM, sin tocar un solo archivo de tu disco duro.
* **Ventajas:** Cero riesgo. Puedes probar si te gusta la interfaz, si detecta tu Wi-Fi, tu tarjeta gráfica y tu sonido antes de instalar nada.
* **Inconvenientes:** El rendimiento es un poco más lento (depende de la velocidad de tu USB) y, por defecto, **todo lo que hagas se borrará cuando apagues el ordenador**.
* **Ideal para:** Una primera toma de contacto o para diagnosticar y reparar ordenadores estropeados.

## 💻 2. Máquinas Virtuales (El laboratorio seguro)
Una máquina virtual (MV) es, literalmente, un "ordenador de mentira" que se ejecuta dentro de tu ordenador real a través de un programa (como VirtualBox o VMware). Para tu sistema principal (Windows/Mac), la máquina virtual es solo una ventana más; pero dentro de esa ventana, hay un Linux completo funcionando.
* **Ventajas:** Es un entorno aislado. Si rompes el sistema Linux por accidente, simplemente borras la máquina virtual y creas otra en segundos. Tu ordenador físico está 100% a salvo.
* **Inconvenientes:** Requiere que tu ordenador tenga recursos suficientes (idealmente 8GB de RAM o más) para poder ejecutar dos sistemas operativos al mismo tiempo.
* **Ideal para:** **¡Hacer este curso!** Es el entorno perfecto para aprender, romper cosas y experimentar sin miedo.

## 🏢 3. WSL (Windows Subsystem for Linux)
Si usas Windows 10 o Windows 11, Microsoft ha integrado una herramienta oficial que te permite instalar un entorno de Linux "dentro" de Windows, de forma nativa. 
* **Ventajas:** No necesitas máquinas virtuales lentas ni pendrives. Tienes acceso a toda la potencia de la terminal de Linux (ej. Ubuntu) directamente desde tu menú de inicio de Windows. Consume muy pocos recursos.
* **Inconvenientes:** Está centrado principalmente en la consola (terminal). Aunque se pueden ejecutar aplicaciones con interfaz gráfica, no está pensado para darte la "experiencia completa" de un escritorio Linux.
* **Ideal para:** Programadores y desarrolladores que trabajan en Windows pero necesitan herramientas de Linux para su código.

## 🌗 4. Dual Boot (Compartiendo el disco duro)
El "Arranque Dual" consiste en hacerle un hueco a Linux en tu disco duro físico junto a Windows. Al encender el ordenador, aparecerá un menú (llamado GRUB) que te preguntará: *¿Qué sistema quieres usar hoy?*
* **Ventajas:** Rendimiento máximo. Linux aprovechará al 100% la tarjeta gráfica, el procesador y la RAM de tu equipo físico.
* **Inconvenientes:** El proceso de instalación requiere modificar las particiones del disco duro. Un error aquí **sí puede borrar tus datos o romper tu Windows**.
* **Ideal para:** Usuarios que ya han probado Linux, se sienten cómodos y quieren usarlo como su sistema operativo principal del día a día (pero necesitan mantener Windows para algún juego o programa específico).

---

### 💡 Nuestro enfoque para el curso
Para garantizar que todos podamos avanzar al mismo ritmo y sin poner en riesgo nuestros ordenadores personales, en el próximo tema nos centraremos en **preparar una Máquina Virtual**. 

---
[<- Anterior: Entornos de Escritorio](../03-entornos-de-escritorio/README.md) | [Volver al Módulo 1](../README.md) | [Siguiente: Máquinas Virtuales ->](../05-maquinas-virtuales/README.md)