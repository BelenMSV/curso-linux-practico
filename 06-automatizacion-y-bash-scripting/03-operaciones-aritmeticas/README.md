# Tema 3: Operaciones Aritméticas (Haciendo cálculos)

Bash es increíblemente bueno manejando textos, archivos y carpetas, pero curiosamente, no fue diseñado originalmente para ser bueno en matemáticas. Si intentas escribir `RESULTADO=5+5` en tu script y luego haces un `echo $RESULTADO`, Linux literalmente imprimirá en pantalla el texto "5+5", ¡no un 10!

Para decirle a Bash que queremos que se comporte como una calculadora y no como una máquina de escribir, tenemos que usar una sintaxis especial.

## 🧮 1. La sintaxis mágica: `$(( ))`
Para evaluar una expresión matemática (sumar, restar, etc.), debemos encerrar la operación dentro de un símbolo de dólar y **dobles paréntesis**. A esto se le llama *Expansión Aritmética*.

```bash
# Correcto:
RESULTADO=$(( 5 + 5 ))
echo "El resultado es $RESULTADO"
```
*💡 Nota: Dentro de los dobles paréntesis `(( ))`, a Bash ya no le importan tanto los espacios. Puedes poner `$((5+5))` o `$(( 5 + 5 ))` y funcionará igual.*

## ➕ 2. Los operadores básicos
Bash soporta los operadores matemáticos clásicos que ya conoces:
* **Suma:** `+`
* **Resta:** `-`
* **Multiplicación:** `*`
* **División:** `/`
* **Módulo (Resto de una división):** `%`

**Ejemplo usando variables:**
```bash
NUM1=20
NUM2=5

SUMA=$(( NUM1 + NUM2 ))
MULTI=$(( NUM1 * NUM2 ))

echo "La suma es $SUMA y la multiplicación es $MULTI"
```

## ⚠️ 3. La gran limitación de Bash: Solo números enteros
Hay algo muy importante que debes saber sobre las matemáticas en Bash: **por defecto, no entiende de decimales**. 

Si intentas hacer una división que no es exacta, Bash simplemente truncará (cortará) los decimales sin redondear.
```bash
DIV=$(( 10 / 3 ))
echo $DIV
```
*(El resultado que verás en pantalla será `3`, no `3.33`).*

Si en el mundo real necesitas hacer cálculos complejos con decimales en un script de Bash, los administradores suelen llamar a una herramienta externa llamada `bc` (Basic Calculator), pero para el 99% de los scripts de automatización (como contar cuántos archivos has borrado), los números enteros son suficientes.

## 🔄 4. Autoincremento (Contadores)
Cuando lleguemos a los bucles (repetir una tarea muchas veces), necesitaremos que el script sepa contar (1, 2, 3...). Bash tiene un atajo para sumar 1 a una variable rápidamente usando `++`:

```bash
CONTADOR=1
((CONTADOR++))
echo $CONTADOR  # Imprimirá 2
```
*(Fíjate que aquí no usamos el `$` delante de los dobles paréntesis porque no estamos guardando el resultado en otra variable, solo estamos modificando la variable `CONTADOR` internamente).*

---
### 🧪 Mini reto práctico
Vamos a crear una pequeña "Calculadora de Jubilación". El script te preguntará tu edad y te dirá cuántos años te faltan para jubilarte (suponiendo que la jubilación es a los 65 años).

1. Abre tu terminal.
2. Crea un archivo nuevo: `nano jubilacion.sh`
3. Escribe el siguiente código:
   ```bash
   #!/bin/bash
   
   clear
   echo "--- CALCULADORA DE JUBILACIÓN ---"
   
   read -p "Por favor, introduce tu edad actual: " EDAD
   
   # Hacemos el cálculo
   EDAD_JUBILACION=65
   FALTAN=$(( EDAD_JUBILACION - EDAD ))
   
   echo "---------------------------------"
   echo "Tienes $EDAD años."
   echo "Te faltan $FALTAN años para poder jubilarte."
   echo "¡Ánimo!"
   ```
4. Guarda y cierra (Ctrl+O, Enter, Ctrl+X).
5. Dale permisos de ejecución: `chmod +x jubilacion.sh`
6. Ejecútalo con `./jubilacion.sh` y prueba a introducir distintas edades.

---
[<- Anterior: Variables y Entrada de Datos](../02-variables-y-entrada-de-datos/README.md) | [Volver al Módulo 6](../README.md) | [Siguiente: Condicionales IF-ELSE ->](../04-condicionales-if-else/README.md)