# Tema 7: Proyecto Final (Tu primer robot de Backup)

¡Felicidades por llegar hasta aquí! Has aprendido a crear variables, usar condicionales, hacer bucles y organizar tu código en funciones. Ahora vamos a construir algo útil de verdad.

Casi todas las empresas necesitan hacer copias de seguridad (backups) de sus archivos importantes todos los días. En lugar de hacerlo a mano, vamos a programar un script que lo haga por nosotros, le ponga la fecha actual al archivo para no sobreescribir las copias anteriores, y nos avise si algo sale mal.



## 🎯 El Objetivo

Vamos a crear un script llamado `backup.sh` que hará lo siguiente:
1. Comprobará si existe la carpeta que queremos guardar (ej. `~/Documentos`).
2. Comprobará si existe la carpeta de destino para los backups (ej. `~/Mis_Backups`). Si no existe, la creará automáticamente.
3. Comprimirá la carpeta en un archivo `.tar.gz` (usando lo aprendido en el Módulo 4).
4. Nombrará el archivo resultante con la fecha y hora exactas (ej. `backup_2026-04-28.tar.gz`).

## 🛠️ El Ingrediente Secreto: El comando `date`
Para que el nombre del archivo cambie cada día automáticamente, necesitamos guardar la fecha actual en una variable. En Bash, podemos guardar el *resultado* de un comando dentro de una variable usando la sintaxis `$(comando)`.

Para obtener la fecha en formato "Año-Mes-Día", usamos:
```bash
FECHA_ACTUAL=$(date +%Y-%m-%d)
```

## 🚀 Manos a la obra: El Código Final

1. Ve a tu carpeta personal (`cd ~`).
2. Crea el archivo de nuestro proyecto: `nano backup.sh`
3. Copia con cuidado el siguiente código. ¡Léelo de arriba a abajo, verás que ahora entiendes absolutamente todo lo que hace!

```bash
#!/bin/bash

# === VARIABLES GLOBALES ===
CARPETA_ORIGEN="$HOME/Documentos"
CARPETA_DESTINO="$HOME/Mis_Backups"
FECHA=$(date +%Y-%m-%d_%H-%M) # Año-Mes-Día_Hora-Minuto
NOMBRE_ARCHIVO="backup_$FECHA.tar.gz"

# === FUNCIONES ===
imprimir_mensaje() {
    echo "========================================"
    echo " >>> $1"
    echo "========================================"
}

# === LÓGICA PRINCIPAL ===
clear
imprimir_mensaje "INICIANDO SISTEMA DE COPIAS DE SEGURIDAD"

# 1. Comprobamos si la carpeta origen existe
if [ ! -d "$CARPETA_ORIGEN" ]; then
    # El símbolo '!' significa NOT (Si NO existe el directorio...)
    echo "ERROR: La carpeta que intentas guardar ($CARPETA_ORIGEN) no existe."
    echo "Por favor, crea la carpeta o revisa la ruta."
    exit 1 # Esto detiene el script por completo con un código de error
fi

# 2. Comprobamos si la carpeta destino existe. Si no, la creamos.
if [ ! -d "$CARPETA_DESTINO" ]; then
    echo "La carpeta de destino no existe. Creándola en $CARPETA_DESTINO..."
    mkdir -p "$CARPETA_DESTINO"
fi

# 3. Hacemos la copia de seguridad comprimida
imprimir_mensaje "Comprimiendo archivos..."
# Explicación de tar: -c (crear), -z (comprimir gzip), -v (ver proceso), -f (nombre archivo)
tar -czvf "$CARPETA_DESTINO/$NOMBRE_ARCHIVO" "$CARPETA_ORIGEN"

imprimir_mensaje "¡COPIA DE SEGURIDAD COMPLETADA CON ÉXITO!"
echo "Tu archivo está guardado en: $CARPETA_DESTINO/$NOMBRE_ARCHIVO"
```

## 🧪 La Prueba Final

1. Guarda el archivo en nano (Ctrl+O, Enter, Ctrl+X).
2. Dale permisos de ejecución a tu nueva herramienta:
   ```bash
   chmod +x backup.sh
   ```
3. Antes de probarlo, asegúrate de tener una carpeta `Documentos` con algo dentro (si no la tienes, créala con `mkdir ~/Documentos` y mete un par de archivos vacíos con `touch ~/Documentos/prueba.txt`).
4. ¡Ejecuta el script!
   ```bash
   ./backup.sh
   ```
5. Si lo has hecho bien, verás la animación de compresión. Haz un `ls ~/Mis_Backups` y maravíllate viendo tu archivo comprimido perfectamente nombrado con la fecha y hora exactas.

*(Nota: Si ejecutas el script 5 veces seguidas esperando un minuto entre cada vez, ¡tendrás 5 copias de seguridad distintas sin machacar ninguna!)*

---

### 🎉 ¡Fin del Módulo 6!
¡Impresionante! Has dado el salto de usuario a creador. 

Ahora sabes que Linux no es solo una pantalla negra donde escribir comandos, sino un lienzo en blanco donde puedes programar tus propias herramientas para hacer tu vida (y tu trabajo) mucho más fácil. Las posibilidades son infinitas.

---
[<- Anterior: Funciones y Organización](../06-funciones-y-organizacion/README.md) | [Volver al Módulo 6](../README.md)