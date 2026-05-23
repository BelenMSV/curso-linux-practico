# Tema 2: Fortificando SSH (El fin de las contraseñas)

Si tu servidor está expuesto a internet y revisas el archivo `/var/log/auth.log` (como vimos en el Módulo 10), verás miles de intentos de inicio de sesión fallidos. Son ejércitos de *bots* probando contraseñas como `123456`, `admin` o `password` las 24 horas del día. A esto se le llama ataque de **Fuerza Bruta**.

Por muy larga que sea tu contraseña, es vulnerable. La solución definitiva de los administradores de sistemas es eliminar las contraseñas por completo y usar **Criptografía Asimétrica (Llaves SSH)**.



## 🔑 1. ¿Cómo funcionan las llaves SSH?
En lugar de una contraseña, creas un par de llaves matemáticas que están vinculadas entre sí:
1.  **La Llave Privada (`id_ed25519`):** Se queda en tu ordenador personal (Windows/macOS/Linux). Es como tu llave física de casa. **NUNCA** debes compartirla con nadie ni subirla a internet.
2.  **La Llave Pública (`id_ed25519.pub`):** Esta llave la subes al servidor. Actúa como la "cerradura". 

Cuando intentas conectarte, el servidor comprueba si tu llave privada encaja en la llave pública (cerradura) que él tiene. Si encajan, entras instantáneamente. Si no, la conexión se rechaza sin siquiera preguntar la contraseña.

## 🛠️ 2. Generando tu par de llaves (En tu PC)
**¡ATENCIÓN!** Este primer paso no se hace en el servidor, se hace en la terminal de **tu propio ordenador personal**.

1.  Abre una terminal en tu PC y ejecuta:
    ```bash
    ssh-keygen -t ed25519 -C "mi_pc_principal"
    ```
    *(Usamos `ed25519` porque es el algoritmo más moderno, rápido y seguro en la actualidad, superior al antiguo RSA).*
2.  Te preguntará dónde guardarla. Pulsa **Enter** para dejar la ruta por defecto.
3.  Te pedirá una **Passphrase** (Contraseña de la llave). Esto es opcional, pero muy recomendado. Es una contraseña extra para proteger tu llave privada por si alguien roba tu ordenador físico. Escribe una y pulsa Enter (o déjalo en blanco si prefieres entrar sin escribir nada).

## 🚀 3. Subiendo la llave pública al servidor
Ahora tenemos que enviarle la "cerradura" (llave pública) al servidor. 

Desde la terminal de tu ordenador personal, ejecuta este comando (cambiando `usuario` por tu usuario en el servidor y la IP):
```bash
ssh-copy-id usuario@TU_IP_DEL_SERVIDOR
```
Te pedirá la contraseña de tu usuario en el servidor por última vez. Verás un mensaje indicando que la llave se ha añadido con éxito.

### 🧪 Prueba de fuego
Intenta conectarte de nuevo a tu servidor:
```bash
ssh usuario@TU_IP_DEL_SERVIDOR
```
¡Magia! Habrás entrado directamente sin escribir la contraseña del servidor (solo te pedirá la *passphrase* de la llave si configuraste una en el paso 2).

## 🛑 4. El Hardening: Prohibir las contraseñas
Ahora que tenemos nuestra llave maestra funcionando, vamos a decirle al servidor que **rechace cualquier intento de inicio de sesión con contraseña tradicional**. Si un hacker no tiene el archivo de tu llave privada, no podrá entrar aunque sepa tu clave.

**¡ADVERTENCIA DE PELIGRO!** Antes de hacer esto, asegúrate de que el Paso 3 te ha funcionado y estás conectado al servidor con tu llave. Si deshabilitas las contraseñas sin tener la llave configurada, **te quedarás encerrado fuera de tu propio servidor para siempre**.

1. Ya dentro de tu servidor, abre el archivo de configuración del servicio SSH:
   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Busca la línea que dice `PasswordAuthentication yes` (puede que tenga un `#` delante). Quítale el `#` y cámbiala a `no`:
   ```text
   PasswordAuthentication no
   ```
3. Mientras estamos aquí, vamos a cerrar la vulnerabilidad número uno. Nunca se debe permitir iniciar sesión directamente como el usuario `root`. Busca la línea `PermitRootLogin` y cámbiala a `no`:
   ```text
   PermitRootLogin no
   ```
4. Guarda (Ctrl+O, Enter) y sal (Ctrl+X).

## 🔄 5. Aplicar los cambios y comprobar
Para que el servidor SSH lea sus nuevas normas de seguridad, debemos reiniciarlo:
```bash
sudo systemctl restart ssh
```
*(Nota: En algunas distribuciones como CentOS se llama `sshd`)*.

### 🕵️‍♀️ Verificación del SysAdmin
No cierres tu terminal actual todavía. Abre **otra ventana** de terminal en tu ordenador e intenta conectarte al servidor deliberadamente forzando el uso de contraseñas:
```bash
ssh -o PubkeyAuthentication=no usuario@TU_IP_DEL_SERVIDOR
```
El servidor te dará un portazo en la cara con un error: `Permission denied (publickey)`.

**¡Felicidades!** Tu servidor acaba de volverse inmune al 99% de los ataques automatizados de internet.

---
[<- Anterior: Auditoría y Hardening Básico](../01-auditoria-y-hardening-basico/README.md) | [Volver al Módulo 11](../README.md) | [Siguiente: Defensa Activa con Fail2Ban ->](../03-defensa-activa-fail2ban/README.md)