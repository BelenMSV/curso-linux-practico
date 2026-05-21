# Tema 1: Auditoría y Hardening Básico (Reduciendo la superficie de ataque)

La seguridad informática en Linux no consiste en instalar un antivirus mágico. Se basa en un concepto militar llamado **Superficie de Ataque**. 

Imagina tu servidor como un castillo. Cuantas más puertas, ventanas y puentes levadizos tenga, más lugares tendrá que defender la guardia. El **Hardening** (fortificación) consiste en tapiar todas las ventanas que no usas, destruir los puentes innecesarios y dejar solo una puerta blindada.

Vamos a realizar la primera auditoría de tu sistema.



## 🧹 1. Lo básico: Actualizaciones y limpieza
Parece obvio, pero el 90% de los hackeos exitosos en el mundo ocurren explotando vulnerabilidades viejas para las que **ya existía un parche**. Un servidor desactualizado es un servidor hackeado.

1. **Aplica todos los parches de seguridad:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   
```
2. **Elimina software que ya no usas:**
   Si instalaste herramientas para probar algo (por ejemplo, un servidor FTP) y ya no lo usas, bórralo. Un programa que no existe no puede ser hackeado.
   ```bash
   sudo apt autoremove -y
   
```

## 🚪 2. Auditoría de Servicios Expuestos (`ss`)
¿Sabes exactamente qué programas están "escuchando" en tu servidor, esperando conexiones de internet? Vamos a comprobarlo.

Ejecuta este comando (el sucesor moderno de `netstat`):
```bash
sudo ss -tulpn
```
*(**t**=tcp, **u**=udp, **l**=listening, **p**=processes, **n**=numeric)*

**¿Cómo leer esto?**
Mira la columna `Local Address:Port`. 
* Si ves `127.0.0.1:puerto` o `[::1]:puerto`, ese servicio solo escucha hacia adentro (seguro).
* Si ves `0.0.0.0:puerto` o `*:puerto`, ese servicio **está expuesto a todo internet**. 

Si ves un puerto expuesto que no reconoces (como el 111 de `rpcbind`, muy común en Ubuntu), averigua qué es y apágalo si no lo necesitas:
```bash
sudo systemctl stop rpcbind
sudo systemctl disable rpcbind
```

## 👥 3. El Principio del Menor Privilegio (Usuarios)
La regla de oro de la seguridad: **Dale a los usuarios y programas solo los permisos estrictamente necesarios para hacer su trabajo, y ni un poco más.**

Vamos a auditar quién tiene derecho a entrar a tu servidor.
Ejecuta este comando para ver qué usuarios tienen una terminal (shell) válida para iniciar sesión:
```bash
cat /etc/passwd | grep -E "(/bin/bash|/bin/sh)"
```
*   Si ves usuarios antiguos, cuentas de prueba o ex-empleados, elimínalos inmediatamente con `sudo userdel usuario`.
*   El usuario `root` aparecerá aquí, pero en el próximo tema le cortaremos las alas.

## ⚠️ 4. Cazando archivos peligrosos
En el Módulo 5 aprendimos sobre los permisos `rwx`. Ahora vamos a ponernos el sombrero de hacker y a buscar los dos mayores agujeros de seguridad a nivel de archivos.

### A. Archivos huérfanos sin dueño
Si borraste un usuario, es posible que haya dejado archivos atrás. Estos archivos son peligrosos porque si otro usuario hereda ese mismo ID en el futuro, tomará control sobre ellos.
```bash
sudo find / -xdev \( -nouser -o -nogroup \) -print
```
*(Si este comando te devuelve rutas extrañas, investiga y bórralos si es necesario).*

### B. Archivos SUID (El poder de Root prestado)
¿Recuerdas que un usuario normal puede usar el comando `sudo` o `passwd`? Esto es posible porque esos comandos tienen un permiso especial llamado **SUID** (Set User ID). Cuando ejecutas un archivo SUID, no lo ejecutas con tus permisos, sino con los permisos del *dueño* del archivo (normalmente Root).

Si un hacker encuentra un archivo SUID vulnerable o creado por error, lo usará para convertirse en Root.

Vamos a listar todos los archivos SUID del sistema:
```bash
sudo find / -perm -4000 -type f -exec ls -la {} \; 2>/dev/null
```
*   Verás cosas normales como `/usr/bin/passwd` o `/usr/bin/sudo`.
*   Pero si ves aquí tu propio script o un programa extraño... **peligro rojo**. Deberás quitarle ese permiso con `sudo chmod u-s /ruta/al/archivo`.

## 🛡️ 5. Deshabilitar los puertos USB (Opcional pero pro)
Si tu servidor es una máquina física en una oficina o centro de datos, un ataque muy común es que alguien conecte un "Rubber Ducky" (un USB que simula ser un teclado) o un pendrive con malware.

Para decirle al Kernel de Linux que ignore completamente cualquier memoria USB, creamos un archivo de regla:
```bash
echo "install usb-storage /bin/true" | sudo tee /etc/modprobe.d/disable-usb-storage.conf
```
*(Nota: Esto no aplica a los servidores VPS en la nube, ya que ¡no tienen puertos físicos!)*

---

### 🧠 Conclusión de la Auditoría
Hardening no es hacer una cosa increíble, es hacer cientos de cosas pequeñas de forma consistente. Ahora que sabemos que no tenemos puertas traseras obvias ni archivos peligrosos, vamos a fortificar la puerta principal.

En el siguiente tema, vamos a **prohibir las contraseñas** en nuestro servidor.

---
[<- Volver al Módulo 11](../README.md) | [Siguiente: Fortificando SSH (Llaves criptográficas) ->](../02-fortificando-ssh-llaves-criptograficas/README.md)