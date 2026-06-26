# Tema 3: Checklist de Producción (El ritual del SysAdmin)

Acabas de alquilar un servidor. Está brillante, nuevo y... **completamente expuesto**. 

Por defecto, muchos proveedores Cloud te dan acceso directo como el superusuario `root`. Esto es cómodo, pero es una pesadilla de seguridad. Antes de instalar Nginx, Docker o tu código, debemos aplicar todo lo aprendido en los Módulos 5, 7 y 11 para blindar el sistema. 

Abre tu terminal, conéctate a tu VPS y ejecuta este checklist.

## ✅ Paso 1: Actualizar el Sistema
Nunca sabes cuánto tiempo hace que el proveedor Cloud creó la "imagen base" que acaba de instalar en tu servidor. Lo primero es parchear todas las vulnerabilidades conocidas hasta el día de hoy.
```bash
apt update && apt upgrade -y
```
*(Como estamos conectados como `root`, no hace falta usar `sudo` de momento).*

## ✅ Paso 2: Crear un usuario mundano
Trabajar todo el tiempo como `root` es como conducir un coche con un bidón de gasolina abierto en el asiento del copiloto; al menor error, todo explota. Vamos a crear un usuario normal con permisos de administrador (`sudo`).

1. **Crea el usuario** (cambia `tu_nombre` por el que prefieras):
   
```bash
   adduser tu_nombre
   ```
   *(Te pedirá crear una contraseña y algunos datos opcionales. Rellena la contraseña y pulsa Enter para lo demás).*
2. **Dale poderes de administrador:**
   ```bash
   usermod -aG sudo tu_nombre
   ```

## ✅ Paso 3: Migrar tu Llave SSH (El truco Pro)
Si en el Tema 1 entraste al VPS usando tu llave SSH, esa llave pública se guardó en la carpeta del usuario `root`. Si intentas entrar ahora con tu nuevo usuario, el servidor te pedirá contraseña.

En lugar de generar llaves nuevas, vamos a **copiar la configuración SSH de root a tu nuevo usuario** con este comando mágico (asegúrate de cambiar `tu_nombre`):
```bash
rsync --archive --chown=tu_nombre:tu_nombre ~/.ssh /home/tu_nombre
```

### 🛑 PRUEBA VITAL 🛑
**NO CIERRES TU TERMINAL ACTUAL.** Abre una **nueva ventana** de terminal en tu ordenador personal e intenta conectarte con tu nuevo usuario:
```bash
ssh tu_nombre@IP_DE_TU_VPS
```
Si entras directamente sin que te pida la contraseña del servidor... ¡Lo has logrado! Ya puedes cerrar la sesión antigua de root y seguir trabajando desde tu nueva sesión segura. *(A partir de ahora volverás a usar `sudo` para comandos de administración).*

## ✅ Paso 4: Cerrar la puerta de `root` y las contraseñas
Ahora que tienes tu usuario y tu llave funcionando, vamos a castigar a los *bots* que intentan hackearte.

1. Edita la configuración de SSH:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Cambia estas dos líneas (quítales el `#` si lo tienen):
   ```text
   PermitRootLogin no
   PasswordAuthentication no
   ```
3. Guarda y reinicia el servicio:
   ```bash
   sudo systemctl restart ssh
   ```

## ✅ Paso 5: Levantar el Cortafuegos (UFW)
Vamos a bloquear todo el tráfico entrante, permitiendo únicamente SSH (para que no nos eche) y los puertos web (para cuando instalemos nuestra página).
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw limit ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```
*(Cuando te pregunte si quieres continuar porque podría cortar tu conexión, dile `y`).*

## ✅ Paso 6: Soltar al perro guardián (Fail2Ban)
Por último, instalamos nuestro sistema de defensa activa para banear a cualquiera que intente forzar nuestro SSH u otros servicios.

1. Instala el programa:
   ```bash
   sudo apt install fail2ban -y
   ```
2. Crea el archivo de cárcel local:
   ```bash
   sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
   ```
3. El servicio se enciende y protege SSH automáticamente por defecto, así que solo verifica que esté corriendo:
   ```bash
   sudo systemctl status fail2ban
   ```

---

### 🏆 ¡Servidor en Estado de Producción!
Tómate un respiro. Lo que acabas de hacer en estos 6 pasos es **exactamente lo mismo** que hace un ingeniero Senior en una empresa cuando levanta una nueva infraestructura.

Tu servidor es ahora una fortaleza. Nadie puede iniciar sesión como root, nadie puede usar contraseñas, los bots están limitados por UFW y bloqueados por Fail2Ban.

Ahora sí, el lienzo está limpio y seguro. En el próximo tema, **vamos a desplegar tu proyecto**.

---
[<- Anterior: Dominios y Registros DNS](../02-dominios-y-registros-dns/README.md) | [Volver al Módulo 12](../README.md) | [Siguiente: Despliegue del Proyecto ->](../04-despliegue-del-proyecto/README.md)