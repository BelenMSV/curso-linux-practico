# Tema 4: Instalación paso a paso

¡Es hora de encender la máquina! Si has configurado correctamente tu Máquina Virtual o tu USB booteable, al arrancar verás un menú que te ofrece "Probar o Instalar". Mi recomendación es seleccionar **"Probar" (Try Linux)**; esto te llevará a un escritorio funcional donde podrás verificar que todo se ve bien antes de darle al icono del escritorio que dice **"Instalar sistema"**.

A continuación, detallamos las etapas clave del asistente de instalación:

## 1. Idioma y Teclado
Parece trivial, pero es vital. 
* Selecciona **Español** para el sistema.
* En la disposición del teclado, asegúrate de probar la tecla `ñ` y los símbolos `@` o `#` en el cuadro de texto de prueba. Si usas un portátil, a veces la distribución correcta es "Español (latinoamericano)" o "Español (variante)".

## 2. Actualizaciones y Software de Terceros
Verás dos casillas muy importantes:
* **Descargar actualizaciones al instalar:** Ahórrate tiempo después activando esto (requiere internet).
* **Instalar software de terceros (Drivers y Multimedia):** **¡Actívala!** Esto instalará controladores para tarjetas Wi-Fi, gráficas y códecs para reproducir MP3 o video que no son estrictamente "libres" pero son necesarios para que todo funcione a la primera.

## 3. Tipo de Instalación (El momento del particionado)
Como vimos en el tema anterior, aquí decides el destino de tu disco:
* **Borrar disco e instalar (Recomendado para el curso):** El instalador formateará el disco virtual y creará las particiones automáticamente. Es la opción más rápida y segura para nuestra práctica.
* **Más opciones:** Aquí es donde entrarías si quisieras hacer el particionado manual que explicamos (Raíz, Home, Swap).



## 4. Localización (Zona Horaria)
Haz clic en el mapa sobre tu ciudad o región. Esto no solo ajusta el reloj, sino que ayuda al sistema a elegir el servidor de descargas más cercano a ti para que las actualizaciones vuelen.

## 5. ¿Quién es usted? (Creación de Usuario)
Este es el paso más importante para la seguridad de tu futuro sistema:
* **Su nombre:** Tu nombre real.
* **Nombre de su equipo:** Cómo se llamará el PC en la red (ej. `pc-linux-pedro`).
* **Nombre de usuario:** Un nombre corto, en minúsculas y sin espacios (ej. `pedro`). **Recuérdalo bien, lo usarás para loguearte.**
* **Contraseña:** En Linux, la contraseña es obligatoria y fundamental. La usarás cada vez que quieras instalar algo o hacer cambios importantes (comando `sudo`).

> ⚠️ **Nota:** Te recomiendo activar "Solicitar mi contraseña para iniciar sesión" por seguridad, especialmente si luego quieres aprender sobre encriptación.

## 6. El proceso final
Una vez confirmes, el instalador empezará a copiar archivos. Mientras tanto, verás una presentación de diapositivas con las bondades de la distribución. 
* **No apagues el ordenador.**
* Al finalizar, aparecerá un mensaje: *"La instalación se ha completado. Necesita reiniciar el equipo"*.

**¡IMPORTANTE!** Al reiniciar, el sistema te pedirá: *"Please remove the installation medium, then press ENTER"*. 
* Si es un USB físico, retíralo. 
* Si es VirtualBox, el programa suele "expulsar" el CD virtual automáticamente, así que solo pulsa **Enter**.

---
[<- Anterior: El Particionado de Disco](../03-el-particionado-de-disco/README.md) | [Volver al Módulo 2](../README.md) | [Siguiente: Post-instalación básica ->](../05-post-instalacion-basica/README.md)