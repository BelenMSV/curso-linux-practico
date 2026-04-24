# Tema 5: Máquinas Virtuales (Tu Laboratorio Seguro)

Como vimos en el tema anterior, la forma más segura e inteligente de aprender Linux sin poner en riesgo tu ordenador principal es usando una **Máquina Virtual (MV)**. 

En este tema vamos a preparar tu "laboratorio de pruebas". Usaremos **VirtualBox**, ya que es gratuito, de código abierto y funciona igual de bien en Windows, macOS y Linux.

## 🧰 Paso 1: Descargar los materiales
Antes de empezar a montar la máquina, necesitamos dos cosas:
1. **El software de virtualización:** Ve a la página oficial de [VirtualBox](https://www.virtualbox.org/) y descarga la versión correspondiente a tu sistema operativo (Windows, macOS o Linux). Instálalo como cualquier otro programa (siguiente, siguiente, aceptar).
2. **La imagen de Linux (Archivo ISO):** Necesitas el "CD de instalación" virtual. Ve a la página oficial de [Ubuntu](https://ubuntu.com/download/desktop) o [Linux Mint](https://linuxmint.com/download.php) y descarga el archivo `.iso`. Suele pesar entre 3GB y 4GB.

## ⚠️ Paso 2: El "Secreto" Técnico (Virtualización en BIOS)
*Nota importante:* Para que tu ordenador permita ejecutar otro sistema operativo en su interior, una función llamada **Virtualización de Hardware (VT-x para Intel o AMD-V para AMD)** debe estar activada.

En la mayoría de los ordenadores modernos ya viene activada de fábrica. Si al intentar encender tu máquina virtual más adelante te da un error extraño, lo más probable es que tengas que reiniciar tu ordenador físico, entrar en la BIOS/UEFI y activar esta opción.

## 🏗️ Paso 3: Creando la Máquina Virtual
Abre VirtualBox y sigue estos pasos:

1. **Nueva Máquina:** Haz clic en el botón "Nueva" o "New".
2. **Nombre y Sistema:** * Ponle un nombre (ej. `MiPrimerLinux`).
   * En "Tipo", selecciona `Linux`.
   * En "Versión", selecciona `Ubuntu (64-bit)` (incluso si descargaste Linux Mint, elige Ubuntu ya que comparten la misma base).
3. **Memoria RAM:** Se te pedirá que asignes memoria. 
   * *Regla de oro:* Asigna aproximadamente la mitad de la memoria que tenga tu ordenador físico. Si tienes 8GB en total, asígnale `4096 MB` (4GB). Nunca te quedes en la zona roja de la barra.
4. **Procesador (CPU):** En la pestaña de procesador, asígnale al menos **2 núcleos** para que el sistema vaya fluido.
5. **Disco Duro Virtual:** Selecciona "Crear un disco duro virtual ahora".
   * Asígnale un tamaño de al menos **25 GB** (recomendado 30 GB o más si tienes espacio de sobra). No te preocupes, este espacio no se consume de golpe de tu disco duro real, irá creciendo a medida que metas cosas en Linux.

## 💿 Paso 4: Insertar el "CD" y arrancar
Ya tienes el ordenador virtual montado (pantalla, disco, memoria), pero está vacío. Tenemos que meterle el sistema operativo.

1. Selecciona tu máquina virtual recién creada y haz clic en **"Configuración"** (icono de engranaje).
2. Ve al apartado de **"Almacenamiento"**.
3. Verás un icono de un CD que dice "Vacío". Haz clic en él.
4. A la derecha, haz clic en el icono del CD pequeño y selecciona **"Seleccionar un archivo de disco..."**.
5. Busca y selecciona el **archivo `.iso`** que descargaste en el Paso 1.
6. Haz clic en Aceptar.

¡Felicidades! Ya tienes tu máquina lista. Si ahora haces clic en el botón verde de **"Iniciar"**, la máquina arrancará y leerá el instalador de Linux, exactamente igual que si hubieras metido un USB en un ordenador físico.

---

### 🎉 ¡Fin del Módulo 1!
Con este paso, ya tienes tu entorno completamente preparado. Has aprendido qué es Linux, cómo funciona su ecosistema y has construido un laboratorio seguro. En el próximo módulo, encenderemos esta máquina y realizaremos la instalación paso a paso.

---
[<- Anterior: Alternativas de uso](../04-alternativas-de-uso/README.md) | [Volver al Módulo 1](../README.md)