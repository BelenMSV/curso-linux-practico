# Tema 3: El Particionado de Disco (Entendiendo el espacio)

Llegamos al punto que más miedo da a los principiantes durante la instalación: el particionado. Pero no te preocupes, no es magia oscura. 

Particionar un disco duro es simplemente **trazar líneas imaginarias** para dividir un disco físico en varios "discos lógicos" más pequeños. Es como comprar una casa grande (el disco duro) y levantar paredes para crear habitaciones independientes (particiones).

## 🔤 El choque cultural: Adiós a C: y D:
En Windows, estás acostumbrado a que cada disco o partición tiene una letra: el sistema está en `C:`, los datos en `D:`, y el USB es `E:`.

**En Linux las letras de unidad no existen.** Todo el sistema es un único y gigantesco "Árbol de Directorios" que nace de un único punto de origen llamado **Directorio Raíz**, que se representa con una simple barra inclinada: **`/`**.

Todo lo que conectes (discos duros, USBs, CDs) se "colgará" como una carpeta más dentro de este árbol.

## 🍰 La "Santísima Trinidad" de las particiones Linux
Aunque puedes instalar Linux en una sola partición, las buenas prácticas dictan que dividamos nuestro disco en al menos dos o tres partes clave:

### 1. La Raíz (`/`)
Es el equivalente a `C:\Windows` y `C:\Archivos de Programa`.
* **¿Qué contiene?** El núcleo del sistema operativo, las herramientas base y todos los programas que instales.
* **Tamaño recomendado:** Mínimo 20 GB. Si vas a instalar muchos programas grandes, 40 GB - 50 GB es ideal.

### 2. La memoria de intercambio (`swap`)
Es el equivalente al "Archivo de paginación" de Windows.
* **¿Qué es?** Es una partición especial a la que Linux recurre como un "salvavidas" cuando la memoria RAM física de tu ordenador se llena por completo. Mueve datos inactivos de la RAM al disco duro temporalmente.
* **Tamaño recomendado:** Una regla clásica es asignarle el mismo tamaño que tu memoria RAM física (ej. si tienes 8GB de RAM, le pones 8GB de swap).

### 3. La casa (`/home`)
Es el equivalente a `C:\Usuarios`.
* **¿Qué contiene?** Todos tus archivos personales (Descargas, Documentos, Imágenes) y, muy importante, **las configuraciones personales** de tus programas.
* **Tamaño recomendado:** Todo el espacio que te sobre en el disco duro.

## 🛡️ ¿Por qué separar la `/home` de la Raíz (`/`)?
Hacer esto es el "superpoder" de Linux. Imagina que tu sistema se rompe irremediablemente o decides que quieres cambiar Ubuntu por Fedora. 

Si tienes la `/home` en una partición separada, durante la instalación puedes decirle al instalador: *"Borra la partición Raíz y pon el nuevo sistema ahí, pero **no toques** la partición Home"*.
Resultado: Tienes un sistema operativo nuevo, pero todos tus documentos, fondos de pantalla y preferencias siguen exactamente donde los dejaste.

## 🤖 Particionado Automático vs. Manual
Cuando arranques el instalador de Linux (lo haremos en el siguiente tema), te dará a elegir cómo quieres particionar:

1. **Automático ("Borrar disco e instalar Linux"):** El instalador hace todo por ti. Borra todo el disco y crea la Raíz y la Swap automáticamente (normalmente no separa la Home).
   * *Ideal para:* Máquinas Virtuales o si vas a dedicar un disco físico entero a Linux sin importarte los datos anteriores.
2. **Manual ("Más opciones"):** Tú defines tamaño, formato y función de cada partición.
   * *Ideal para:* Usuarios avanzados, separar la `/home` o para hacer **Dual Boot** (instalar Linux junto a Windows sin borrar Windows).

Para nuestro ejercicio práctico en la Máquina Virtual, usaremos el **método automático**, ya que el disco virtual que creamos está vacío y no hay riesgo de perder datos.

---
[<- Anterior: Preparación del Instalador](../02-preparacion-del-instalador/README.md) | [Volver al Módulo 2](../README.md) | [Siguiente: Instalación paso a paso ->](../04-instalacion-paso-a-paso/README.md)