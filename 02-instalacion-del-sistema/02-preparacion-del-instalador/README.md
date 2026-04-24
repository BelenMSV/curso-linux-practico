# Tema 2: Preparación del Instalador

Ahora que ya tenemos nuestro archivo `.iso` descargado y verificado, necesitamos "montarlo" para que el ordenador (ya sea físico o virtual) pueda arrancar desde él y comenzar la instalación. 

A este proceso se le llama **preparar un medio de instalación o hacer un USB booteable** (arrancable).

Dependiendo de dónde vayas a instalar Linux, debes seguir uno de estos dos caminos:

---

## Camino A: Instalación en una Máquina Virtual (Recomendado para el curso)

Si seguiste el Módulo 1 y vas a usar **VirtualBox**, no necesitas ningún pendrive físico. Solo tenemos que decirle a la máquina virtual que "inserte" el archivo ISO en su lector de CD virtual.

**Pasos:**
1. Abre VirtualBox y selecciona tu máquina virtual (por ejemplo, `MiPrimerLinux`).
2. Haz clic en el botón de **Configuración** (icono de engranaje naranja).
3. Ve a la sección de **Almacenamiento** en el menú izquierdo.
4. En el recuadro central, verás un icono de un disco que dice **Vacío**. Haz clic sobre él.
5. A la derecha, verás otro icono de un disco pequeño junto a "Unidad óptica". Haz clic en él y selecciona **"Seleccionar un archivo de disco..."**.
6. Busca tu archivo `.iso` descargado y dale a **Abrir**.
7. Haz clic en **Aceptar**.

¡Listo! Cuando le des al botón verde de "Iniciar", tu máquina virtual arrancará directamente desde el instalador de Linux.

---

## Camino B: Instalación en un Ordenador Físico (USB Booteable)

Si vas a instalar Linux de verdad en tu PC o portátil, necesitas grabar la ISO en un pendrive USB. 

⚠️ **Aviso crítico:** *No puedes simplemente "copiar y pegar" el archivo .iso dentro del USB*. Necesitas un programa especial que extraiga el contenido y escriba un sector de arranque en el USB. **Este proceso borrará todo el contenido actual de tu pendrive.**

### Herramienta recomendada: BalenaEtcher
Existen muchas herramientas (como Rufus en Windows), pero recomendamos **BalenaEtcher** porque es gratuita, muy fácil de usar y funciona exactamente igual en Windows, macOS y Linux.

**Pasos:**
1. Descarga e instala [BalenaEtcher](https://etcher.balena.io/).
2. Conecta un pendrive USB a tu ordenador (mínimo de 8 GB). ¡Asegúrate de que no tenga archivos importantes!
3. Abre BalenaEtcher. Su interfaz tiene solo 3 pasos:
   * **Paso 1 (Flash from file):** Haz clic aquí y selecciona tu archivo `.iso` descargado.
   * **Paso 2 (Select target):** Selecciona tu pendrive USB en la lista. ¡Cuidado de no seleccionar un disco duro externo por error!
   * **Paso 3 (Flash!):** Haz clic para comenzar. El programa grabará la ISO y luego verificará que se haya hecho correctamente.

### 🔌 Arrancando tu PC desde el USB
Una vez creado el USB, el último obstáculo es decirle a tu ordenador que no arranque Windows, sino que lea el USB.
1. Conecta el USB y reinicia el ordenador.
2. Justo cuando se encienda la pantalla (antes de que cargue Windows), debes presionar repetidamente una tecla para abrir el **Menú de Arranque (Boot Menu)** o entrar en la **BIOS/UEFI**.
3. La tecla depende de la marca de tu ordenador: suele ser `F12`, `F10`, `F8`, `F2` o `Supr/Del`.
4. Una vez en el menú, selecciona tu pendrive USB y presiona Enter.

---

Si has seguido cualquiera de los dos caminos correctamente, la pantalla se volverá negra por unos segundos y verás aparecer el logo de tu distribución (Ubuntu o Mint), indicando que el instalador está cargando.

---
[<- Anterior: Descarga y Verificación](../01-descarga-y-verificacion/README.md) | [Volver al Módulo 2](../README.md) | [Siguiente: El Particionado de Disco ->](../03-el-particionado-de-disco/README.md)