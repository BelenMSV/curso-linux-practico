# Tema 2: Variables y Entrada de Datos (La memoria de tu script)

En el tema anterior creamos un script que hacía cosas útiles, pero era "estático": siempre hacía exactamente lo mismo. Para que un programa sea verdaderamente inteligente, necesita recordar información y poder interactuar con la persona que lo está usando. Aquí es donde entran las variables y el comando `read`.



## 📦 1. ¿Qué es una variable?
Imagina que una variable es una **caja de cartón** con una etiqueta pegada fuera. 
* En la etiqueta escribes un nombre (ej. `EDAD`).
* Dentro de la caja metes un dato (ej. `25`).
* Cuando el script necesite saber la edad, simplemente mira dentro de la caja con la etiqueta `EDAD`.

## ✍️ 2. Creando y usando variables
En Bash, crear una variable es tan fácil como escribir su nombre, poner un signo igual (`=`) y escribir el valor. 

> ☢️ **¡LA REGLA MÁS ESTRICTA DE BASH!**
> **NUNCA pongas espacios antes o después del signo igual.**
> * ❌ Mal: `NOMBRE = "Juan"`
> * ✅ Bien: `NOMBRE="Juan"`

Para "mirar" dentro de la caja y usar el valor, **siempre debes poner un símbolo de dólar (`$`)** delante del nombre de la variable.

**Ejemplo en un script:**
```bash
#!/bin/bash
MI_NOMBRE="Alicia"
MI_EDAD=30

echo "Hola, me llamo $MI_NOMBRE y tengo $MI_EDAD años."
```

## 🌍 3. Variables del Sistema (Variables de Entorno)
Linux ya tiene cajas creadas por defecto que contienen información súper útil sobre tu sistema. Estas variables suelen estar escritas completamente en MAYÚSCULAS. Algunas de las más útiles son:

* `$USER`: Contiene el nombre del usuario que está ejecutando el script.
* `$HOME`: Contiene la ruta a la carpeta personal del usuario (ej. `/home/pedro`).
* `$PWD`: Contiene la carpeta actual en la que estás.
* `$HOSTNAME`: El nombre de tu ordenador.

Puedes probarlas directamente en tu terminal escribiendo, por ejemplo: `echo "Bienvenido, $USER"`.

## 🎤 4. Hablando con el usuario (`read`)
Si quieres que tu script le haga una pregunta a la persona que lo ejecuta y guarde su respuesta en una variable, usamos el comando `read`.

`read` pausa el script, espera a que el usuario escriba algo en su teclado y pulse Enter, y luego guarda lo que escribió en la variable que tú le digas.

**Ejemplo:**
```bash
#!/bin/bash
echo "¿Cómo te llamas?"
read NOMBRE_USUARIO

echo "¡Encantado de conocerte, $NOMBRE_USUARIO!"
```

### El truco Pro (`read -p`)
En lugar de usar un `echo` y luego un `read`, puedes hacerlo todo en la misma línea usando la bandera `-p` (prompt):
```bash
read -p "Por favor, introduce tu ciudad: " CIUDAD
echo "Vaya, $CIUDAD debe ser muy bonito en esta época del año."
```

---
### 🧪 Mini reto práctico
Vamos a crear tu primer script interactivo, como si fuera el proceso de registro de una nave espacial.

1. Abre tu terminal.
2. Crea un archivo nuevo: `nano registro.sh`
3. Escribe el siguiente código:
   ```bash
   #!/bin/bash
   
   clear
   echo "--- TERMINAL DE ACCESO ---"
   echo "Usuario del sistema detectado: $USER"
   
   read -p "Por favor, introduce tu rango espacial (ej. Capitán, Recluta): " RANGO
   read -p "¿A qué planeta te diriges?: " PLANETA
   
   echo "--------------------------"
   echo "Acceso concedido."
   echo "Buen viaje, $RANGO $USER. Configurando coordenadas para $PLANETA..."
   ```
4. Guarda y cierra (Ctrl+O, Enter, Ctrl+X).
5. ¡No olvides darle permisos de ejecución! `chmod +x registro.sh`
6. Ejecútalo: `./registro.sh` y responde a las preguntas.

---
[<- Anterior: Mi primer script](../01-mi-primer-script/README.md) | [Volver al Módulo 6](../README.md) | [Siguiente: Operaciones Aritméticas ->](../03-operaciones-aritmeticas/README.md)