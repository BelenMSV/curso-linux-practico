# Tema 4: Condicionales IF-ELSE (Tomando decisiones)

Un buen administrador de sistemas no ejecuta un comando a ciegas. Antes de copiar un archivo, comprueba si el archivo existe; antes de crear una carpeta, comprueba si ya hay una con ese nombre. 

Para que nuestro script haga estas comprobaciones, usamos la estructura condicional **IF-ELSE** (Si ocurre esto... haz esto, si no... haz lo otro).



[Image of programming if else logic flowchart]


## ⚖️ 1. La anatomía del IF

La estructura básica en Bash puede parecer un poco estricta al principio. Fíjate bien en la sintaxis:

```bash
if [ condición ]; then
    # Comandos si la condición se cumple (es Verdadera)
else
    # Comandos si la condición NO se cumple (es Falsa)
fi
```
*(Nota: La palabra `fi` es simplemente `if` escrito al revés, y sirve para indicarle a Bash que hemos terminado de tomar la decisión).*

> ☢️ **¡LA TRAMPA MORTAL DE LOS CORCHETES!**
> En Bash, los corchetes `[ ]` son en realidad un comando. Por tanto, **DEBE HABER UN ESPACIO en blanco** después del primer corchete y antes del último.
> * ❌ Mal: `if [$EDAD -gt 18]; then` (Dará error)
> * ✅ Bien: `if [ $EDAD -gt 18 ]; then`

## 🔢 2. Comparando Números vs Textos
Aquí es donde Bash es un poco peculiar. No usamos el típico `>` o `<` para comparar números, porque Bash los confunde con la redirección de archivos. Usamos unas letras especiales (que vienen del inglés):

**Para Números:**
* `-eq` (Equal): Igual a `==`
* `-ne` (Not Equal): Diferente de `!=`
* `-gt` (Greater Than): Mayor que `>`
* `-lt` (Less Than): Menor que `<`
* `-ge` (Greater or Equal): Mayor o igual `>=`
* `-le` (Less or Equal): Menor o igual `<=`

**Para Textos (Cadenas):**
* `==` (Igual)
* `!=` (Diferente)

**Ejemplo:**
```bash
EDAD=20

if [ $EDAD -ge 18 ]; then
    echo "Eres mayor de edad. Puedes entrar."
else
    echo "Acceso denegado. Eres menor."
fi
```

## 📁 3. El Superpoder de Bash: Comprobar Archivos
Si Bash fuera malo en matemáticas, lo compensa con creces a la hora de gestionar el disco duro. Bash tiene atajos integrados para hacerle preguntas al sistema de archivos:

* `-d carpeta`: ¿Es un directorio (carpeta) y existe?
* `-e archivo`: ¿Existe este archivo/carpeta?
* `-f archivo`: ¿Es un archivo de texto/datos normal y existe?
* `-r archivo`: ¿Existe y tengo permiso para leerlo?

**Ejemplo de SysAdmin real:**
```bash
if [ -d "/home/pedro/Respaldos" ]; then
    echo "La carpeta de respaldos ya existe. Procediendo..."
else
    echo "La carpeta no existe. Creándola ahora..."
    mkdir /home/pedro/Respaldos
fi
```

## 🔀 4. Múltiples decisiones (ELIF)
A veces no es solo "blanco o negro", sino que hay opciones intermedias. Para eso usamos `elif` (Else If).

```bash
read -p "Introduce una nota del 1 al 10: " NOTA

if [ $NOTA -ge 9 ]; then
    echo "¡Sobresaliente!"
elif [ $NOTA -ge 5 ]; then
    echo "Aprobado."
else
    echo "Suspenso. Tienes que estudiar más."
fi
```

---
### 🧪 Mini reto práctico
Vamos a crear un script de "Instalación Segura". El script comprobará si un programa ya está instalado en tu sistema antes de intentar instalarlo. 

Vamos a comprobar si tienes la herramienta `htop` instalada (es un monitor del sistema muy famoso).

1. Abre tu terminal.
2. Crea el archivo: `nano instalador.sh`
3. Escribe este código:
   ```bash
   #!/bin/bash
   
   clear
   echo "--- COMPROBADOR DE SOFTWARE ---"
   
   # La ruta donde suelen instalarse los programas
   RUTA_PROGRAMA="/usr/bin/htop"
   
   if [ -f $RUTA_PROGRAMA ]; then
       echo "¡Genial! El programa 'htop' ya está instalado en tu sistema."
       echo "Ruta detectada: $RUTA_PROGRAMA"
   else
       echo "El programa 'htop' NO está instalado."
       echo "Por favor, instálalo ejecutando: sudo apt install htop"
   fi
   ```
4. Guarda y cierra (Ctrl+O, Enter, Ctrl+X).
5. Dale permisos: `chmod +x instalador.sh`
6. Ejecútalo (`./instalador.sh`). Si no lo tienes, usa el comando `sudo apt install htop` que te sugiere tu propio script, ¡y vuelve a ejecutar el script para ver cómo ahora toma la otra decisión!

---
[<- Anterior: Operaciones Aritméticas](../03-operaciones-aritmeticas/README.md) | [Volver al Módulo 6](../README.md) | [Siguiente: Bucles FOR y WHILE ->](../05-bucles-for-y-while/README.md)