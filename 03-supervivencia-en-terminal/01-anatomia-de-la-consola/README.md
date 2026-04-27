# Tema 1: Anatomía de la Consola (Terminal, Shell y Prompt)

Abrir la consola por primera vez impone. Estás acostumbrado a iconos, botones y menús, y de repente te encuentras con una ventana oscura y un cursor parpadeando. Tranquilo, es normal sentir un poco de respeto.

Para empezar a dominar esta herramienta, primero debemos entender qué es exactamente lo que estamos viendo y desmontar un par de confusiones comunes.

## 🖥️ Terminal vs. Shell: ¿Son lo mismo?
En el día a día, usamos las palabras "Terminal" y "Consola" como sinónimos, pero técnicamente hay una diferencia importante que te ayudará a entender cómo funciona Linux:

1. **La Terminal (o Emulador de Terminal):** Es simplemente el programa gráfico. Es la "ventana" negra que abres. Se encarga de dibujar las letras, elegir el color del fondo y de recoger lo que tecleas. 
2. **La Shell:** Este es el verdadero cerebro. Es el programa que corre *dentro* de la terminal. Actúa como un intérprete o traductor. Tú le escribes comandos en texto plano, la Shell los interpreta, se los traduce al Kernel (el núcleo del sistema) para que los ejecute, y luego te devuelve el resultado en texto.

> 💡 **Nota:** La Shell más popular y la que viene por defecto en casi todas las distribuciones (incluyendo Ubuntu y Mint) se llama **Bash** (Bourne Again Shell). 

## 🔍 El Prompt: Tu punto de partida
Cuando abres la terminal (puedes hacerlo presionando `Ctrl + Alt + T` en tu escritorio Linux), lo primero que ves no es una pantalla vacía. Verás una línea de texto que termina en un cursor parpadeante esperando tus órdenes.

A esa línea de texto se le llama **Prompt**.

El Prompt está diseñado para darte información vital sobre "dónde estás y quién eres" en todo momento. Vamos a diseccionarlo. Un prompt típico en Ubuntu o Mint se ve así:

`pedro@ubuntu:~$`

Parece un texto extraño, pero cada parte tiene un significado muy preciso:

* **`pedro` (Nombre de usuario):** Te indica con qué usuario has iniciado sesión.
* **`@` (Arroba):** Literalmente significa "en" (del inglés *at*).
* **`ubuntu` (Nombre del equipo):** Es el nombre que le diste a tu máquina durante la instalación (el *hostname*). Resulta muy útil cuando te conectas a servidores remotos para no confundirte de ordenador.
* **`:` (Dos puntos):** Es solo un separador visual.
* **`~` (Ruta actual):** Te indica en qué carpeta estás metido en este momento. La virgulilla (el símbolo `~`) es un atajo universal en Linux que significa **"Tu carpeta personal"** (por ejemplo, `/home/pedro`). Si te mueves a la carpeta Descargas, el prompt cambiará a `~/Descargas$`.
* **`$` (El nivel de poder):** Este símbolo es el más importante. El dólar indica que eres un **usuario estándar**. Tienes permisos para tocar tus cosas, pero el sistema no te dejará romper archivos críticos.

> ⚠️ **Dato curioso y de seguridad:** Si alguna vez ves que el prompt termina en un símbolo de almohadilla (`#`), significa que estás actuando como el Administrador Supremo del sistema (el usuario **root**). Con el `#` tienes poder absoluto... para lo bueno y para lo malo.

## 🛠️ Tu primer comando
Ahora que sabes qué es esa pantalla, vamos a probar que funciona. Escribe este sencillo comando para que la Shell te devuelva un saludo, y presiona la tecla `Enter`:

```bash
echo "Hola, Linux"
```

El comando `echo` simplemente le dice a la Shell que repita en la pantalla el texto que le pasas a continuación.

¡Felicidades! Acabas de comunicarte directamente con el sistema sin usar el ratón. En el próximo tema veremos los atajos de teclado que te convertirán en un usuario mucho más ágil.

---
[<- Volver al Módulo 3](../README.md) | [Siguiente: Atajos y Autocompletado ->](../02-atajos-y-autocompletado/README.md)