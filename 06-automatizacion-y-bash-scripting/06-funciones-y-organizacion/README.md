# Tema 6: Funciones y Organización (Tu código ordenado)

En el mundo de la programación existe una regla de oro llamada **DRY** (*Don't Repeat Yourself* - No te repitas). Si en un script de 100 líneas te das cuenta de que has copiado y pegado el mismo bloque de 5 comandos varias veces en distintos lugares, lo estás haciendo mal. 

Para solucionar esto, empaquetamos esos comandos dentro de una **Función**. Una función es como un "mini-script" dentro de tu script principal. Le pones un nombre y, cada vez que lo necesites, simplemente la llamas por su nombre.



## 📦 1. La anatomía de una Función
Crear una función es muy sencillo. Escribes el nombre que quieras darle, seguido de paréntesis `()` y abres unas llaves `{}`. Todo lo que pongas dentro de las llaves pertenecerá a esa función.

```bash
# Definimos la función
saludar() {
    echo "--------------------------"
    echo "¡Hola! Sistema iniciado."
    echo "--------------------------"
}
```
*⚠️ Importante: Definir la función no hace que se ejecute. Solo le enseña a Bash qué hacer cuando se lo pidas.*

## 🗣️ 2. Llamando a la Función
Para que los comandos dentro de la función se ejecuten, tienes que "llamarla". Para hacerlo, simplemente escribes su nombre como si fuera un comando más de Linux.

```bash
#!/bin/bash

# 1. Primero definimos la función (Bash la lee y se la guarda en memoria)
saludar() {
    echo "--------------------------"
    echo "¡Hola! Sistema iniciado."
    echo "--------------------------"
}

# 2. Ahora empieza el script real. Llamamos a la función 3 veces:
saludar
echo "Haciendo tareas..."
saludar
echo "Terminando tareas..."
saludar
```
*(Si ejecutas esto, verás que el bloque de las tres líneas de texto se imprime tres veces, pero tú solo tuviste que escribir la palabra `saludar`).*

## 📥 3. Pasando datos a la función (Parámetros)
A veces queremos que una función haga siempre lo mismo, pero con datos diferentes. Por ejemplo, una función para imprimir errores en color rojo.

A diferencia de otros lenguajes de programación donde pones variables dentro de los paréntesis `(variable)`, **Bash no usa los paréntesis para eso**. En Bash, le pasas el dato simplemente escribiéndolo a la derecha del nombre de la función (dejando un espacio). 

Dentro de la función, Bash guardará el primer dato que le pases en una variable automática llamada **`$1`**, el segundo dato en **`$2`**, y así sucesivamente.

```bash
#!/bin/bash

# Definimos la función
mostrar_error() {
    echo "¡ALERTA CRÍTICA!: $1"
}

# Llamamos a la función pasándole un texto
mostrar_error "No hay espacio en el disco"
mostrar_error "El usuario no existe"
```

## 🏗️ 4. Estructura profesional de un script
Los SysAdmins profesionales organizan sus scripts siempre de la misma forma para que cualquier otra persona pueda leerlos y entenderlos rápido:

1. **El Shebang:** `#!/bin/bash`
2. **Variables Globales:** Todas las rutas, nombres y configuraciones.
3. **Funciones:** Se definen todas las herramientas que se van a usar.
4. **Lógica Principal:** El código real que empieza a llamar a las funciones.

---
### 🧪 Mini reto práctico
Vamos a crear un script organizado profesionalmente con una función que nos sirva para crear "Títulos" bonitos en nuestra terminal, así no tenemos que escribir guiones (`---`) todo el tiempo.

1. Abre tu terminal.
2. Crea el archivo: `nano organizador.sh`
3. Escribe este código:
   ```bash
   #!/bin/bash
   
   # === VARIABLES GLOBALES ===
   USUARIO_ACTUAL=$USER
   
   # === FUNCIONES ===
   imprimir_titulo() {
       echo ""
       echo "========================================"
       echo "   >>> $1 <<<"
       echo "========================================"
   }
   
   # === LÓGICA PRINCIPAL ===
   clear
   imprimir_titulo "INICIO DEL SISTEMA"
   echo "Bienvenido de nuevo, $USUARIO_ACTUAL."
   
   imprimir_titulo "COMPROBANDO DISCO"
   echo "El disco está al 45% de capacidad."
   
   imprimir_titulo "ACTUALIZACIONES"
   echo "El sistema está actualizado."
   ```
4. Guarda y cierra (Ctrl+O, Enter, Ctrl+X).
5. Dale permisos: `chmod +x organizador.sh`
6. Ejecútalo (`./organizador.sh`). Fíjate en lo limpio y espectacular que queda el resultado en tu pantalla, y lo poco que has tenido que escribir en la lógica principal.

---
[<- Anterior: Bucles FOR y WHILE](../05-bucles-for-y-while/README.md) | [Volver al Módulo 6](../README.md) | [Siguiente: Proyecto Final - Backup ->](../07-proyecto-final-backup/README.md)