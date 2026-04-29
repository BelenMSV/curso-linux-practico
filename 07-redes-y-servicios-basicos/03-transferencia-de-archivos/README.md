# Tema 3: Transferencia de archivos (SCP y SFTP)

A menudo, cuando administras un servidor remoto, necesitas subir un script que has escrito en tu PC o descargar un archivo de log para analizarlo. Como ya sabemos usar SSH, tenemos acceso a dos herramientas hermanas que usan la misma tecnología para mover archivos de forma cifrada: **SCP** y **SFTP**.



## 🚀 1. SCP (Secure Copy)
`scp` es el comando más rápido. Funciona exactamente igual que el comando `cp` que aprendimos en el Módulo 3, pero permite que el origen o el destino estén en otra máquina.

### De tu PC al Servidor (Subir)
La sintaxis es: `scp archivo usuario@ip:/ruta/destino`

```bash
scp notas.txt alicia@192.168.1.50:/home/alicia/Documentos
```

### Del Servidor a tu PC (Descargar)
Simplemente inviertes el orden:
```bash
scp alicia@192.168.1.50:/home/alicia/archivo_remoto.txt .
```
*(El punto `.` al final significa "descárgalo en mi carpeta actual").*

### Copiar carpetas enteras
Al igual que con `cp`, si quieres mover una carpeta con todo su contenido, debes usar la bandera **`-r`** (recursivo):
```bash
scp -r mi_proyecto/ usuario@ip:/home/usuario/
```

## 📁 2. SFTP (Secure FTP)
Si `scp` es para acciones rápidas, **SFTP** es para cuando quieres "navegar" por el servidor remoto mientras mueves archivos. Es una sesión interactiva.

Para iniciarla:
```bash
sftp usuario@direccion_ip
```

Una vez dentro, verás que el prompt cambia a `sftp>`. Aquí puedes usar comandos especiales:
* **`put archivo`**: Sube un archivo de tu PC al servidor.
* **`get archivo`**: Descarga un archivo del servidor a tu PC.
* **`ls` / `cd`**: Navegas por las carpetas del servidor remoto.
* **`lls` / `lcd`**: Navegas por las carpetas de **tu propio PC** (la 'l' es de *local*).
* **`exit`**: Cierra la conexión.

## 🖼️ 3. Bonus: FileZilla (La vía gráfica)
Si no te sientes cómodo con la terminal para mover muchos archivos, puedes usar programas como **FileZilla**. 
Al configurar la conexión, asegúrate de elegir el protocolo **SFTP** y usar el puerto **22**. Esto hará exactamente lo mismo que los comandos anteriores pero con una interfaz de "arrastrar y soltar".



---

### 🧪 Mini reto práctico
Vamos a practicar enviándonos un archivo a nosotros mismos usando la IP de bucle de retorno (`127.0.0.1`).

1. Crea un archivo de prueba: `echo "Archivo secreto" > secreto.txt`
2. Intenta "subirlo" a tu propia carpeta de descargas usando SCP:
   ```bash
   scp secreto.txt tu_usuario@127.0.0.1:~/Descargas/copia_secreto.txt
   ```
3. Introduce tu contraseña cuando la pida.
4. Verifica que ha funcionado: `ls ~/Descargas`.
5. ¡Felicidades! Has simulado una transferencia de red exitosa.

---
[<- Anterior: Acceso remoto con SSH](../02-acceso-remoto-con-ssh/README.md) | [Volver al Módulo 7](../README.md) | [Siguiente: El cortafuegos UFW ->](../04-el-cortafuegos-ufw/README.md)