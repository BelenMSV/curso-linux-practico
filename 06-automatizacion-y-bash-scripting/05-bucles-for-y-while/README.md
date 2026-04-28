# Tema 5: Bucles FOR y WHILE (El trabajador incansable)

Los ordenadores se inventaron para hacer tareas aburridas y repetitivas muy rápido. Imagina que tienes que crear 100 carpetas para un proyecto nuevo (Carpeta_1, Carpeta_2...). Podrías escribir el comando `mkdir` 100 veces, pero estarías desperdiciando tu tiempo. 

Para solucionar esto existen los **Bucles** (o *Loops* en inglés). Un bucle le dice al sistema: *"Toma este comando y repítelo una y otra vez hasta que te diga que pares"*.



## 🔄 1. El Bucle FOR (Cuando sabes el límite)
El bucle `for` es perfecto cuando sabes exactamente cuántas veces quieres repetir algo o tienes una lista concreta de elementos que procesar.

Su estructura se lee así: *"Por (for) cada elemento en esta lista, haz (do) esto, y luego termina (done)"*.

### Ejemplo A: Recorriendo una lista de palabras
```bash
#!/bin/bash
for NOMBRE in "Alicia" "Roberto" "Carlos"
do
    echo "Procesando el usuario: $NOMBRE"
    # Aquí podríamos poner un 'adduser $NOMBRE'
done
```
*(En cada vuelta del bucle, la variable `$NOMBRE` tomará el valor del siguiente nombre de la lista).*

### Ejemplo B: Usando un rango numérico `{inicio..fin}`
Si queremos contar del 1 al 5, no hace falta escribir los cinco números. Bash tiene un atajo usando llaves:
```bash
#!/bin/bash
for NUMERO in {1..5}
do
    echo "Creando informe número $NUMERO..."
done
```

### Ejemplo C: Procesando archivos reales
¡Aquí está el superpoder de los SysAdmins! Podemos usar el bucle `for` junto con el asterisco (`*`) para que el script actúe sobre todos los archivos de una carpeta.
```bash
#!/bin/bash
# Este script añade el prefijo "backup_" a todos los archivos .txt de la carpeta
for ARCHIVO in *.txt
do
    echo "Haciendo copia de $ARCHIVO..."
    cp "$ARCHIVO" "backup_$ARCHIVO"
done
```

## ⏳ 2. El Bucle WHILE (Mientras la condición se cumpla)
El bucle `while` se usa cuando **no sabes cuántas veces** tiene que repetirse la tarea, pero sabes que debe continuar **mientras** una condición sea verdadera. 

La estructura mezcla lo que aprendimos de los condicionales (`if`) y de los bucles:

```bash
#!/bin/bash
CONTADOR=1

# "Mientras el contador sea menor o igual a 3..."
while [ $CONTADOR -le 3 ]
do
    echo "Ciclo número: $CONTADOR"
    
    # ¡Súper importante! Sumar 1 al contador para que el bucle avance
    ((CONTADOR++))
done
echo "El bucle ha terminado."
```

> ☢️ **Cuidado con los bucles infinitos:** Si en el código anterior te olvidas de poner `((CONTADOR++))`, la variable siempre valdrá 1. Como 1 siempre es menor que 3, el bucle nunca se detendrá y bloqueará tu terminal. Si alguna vez te pasa esto, ¡pulsa **Ctrl + C** en tu teclado para matar el proceso de emergencia!

---
### 🧪 Mini reto práctico
Vamos a crear nuestro propio ejército de archivos. Imagina que tienes que preparar el entorno de trabajo para los 5 días de la semana y necesitas 5 archivos de texto vacíos.

1. Abre tu terminal.
2. Crea el archivo: `nano creador.sh`
3. Escribe este código usando un bucle FOR:
   ```bash
   #!/bin/bash
   
   clear
   echo "Iniciando la creación masiva de archivos..."
   
   for DIA in {1..5}
   do
       NOMBRE_ARCHIVO="dia_laborable_$DIA.txt"
       echo "Creando el archivo: $NOMBRE_ARCHIVO"
       touch "$NOMBRE_ARCHIVO"
   done
   
   echo "¡Proceso terminado! Escribe 'ls' para ver tus nuevos archivos."
   ```
4. Guarda y cierra (Ctrl+O, Enter, Ctrl+X).
5. Dale permisos: `chmod +x creador.sh`
6. Ejecútalo (`./creador.sh`).
7. Escribe `ls` en tu terminal. ¡Verás que ha creado los 5 archivos mágicamente en un abrir y cerrar de ojos!

---
[<- Anterior: Condicionales IF-ELSE](../04-condicionales-if-else/README.md) | [Volver al Módulo 6](../README.md) | [Siguiente: Funciones y Organización ->](../06-funciones-y-organizacion/README.md)