# Tema 1: El usuario Root y sudo (La jerarquía de poder)

Si vienes de usar Windows de forma doméstica, probablemente tu cuenta de usuario sea la de "Administrador". Eso significa que puedes instalar programas, borrar archivos del sistema y cambiar configuraciones en cualquier momento. 

En Linux, esa filosofía se considera extremadamente peligrosa. Linux separa estrictamente el uso diario de la administración del sistema mediante una jerarquía de poder muy clara.

## 👑 1. ¿Quién es `root`?
En todos los sistemas Linux existe un usuario supremo, creado automáticamente durante la instalación, llamado **`root`** (raíz).

* Es el **Superusuario** o el Dios del sistema.
* Tiene **poder absoluto**. No hay ningún archivo que no pueda leer, modificar o destruir.
* Linux nunca le dirá "Permiso denegado" a `root`.

Debido a este poder absoluto, **iniciar sesión directamente con el usuario `root` es una terrible idea**. Si te equivocas tecleando un comando de borrado, o si descargas un script malicioso mientras navegas por internet como `root`, el sistema no te detendrá y se destruirá.



## 🛡️ 2. El salvavidas: El comando `sudo`
Para evitar los desastres, las distribuciones modernas (como Ubuntu o Mint) bloquean la cuenta de `root` por defecto. En su lugar, creas una cuenta de **usuario normal** (la que hiciste al instalar el sistema).

Pero entonces, ¿cómo instalamos programas si somos usuarios normales? Usando el comando **`sudo`** (*SuperUser DO* - El superusuario hace).

`sudo` es un mecanismo que te permite **"pedir prestada" la corona de `root` por unos instantes** para ejecutar un único comando, y luego te la quita inmediatamente.

**¿Cómo funciona?**
1. Escribes `sudo` delante del comando peligroso (ej. `sudo apt update`).
2. El sistema te pide **tu** contraseña (no la de root, la tuya) para verificar que eres tú.
3. El comando se ejecuta con poder absoluto.
4. Vuelves a ser un usuario normal inofensivo.

> 💡 **La regla de oro:** Trabaja siempre como usuario normal. Usa `sudo` solo cuando el sistema te diga "Permiso denegado" para una tarea administrativa justificada.

## 🔄 3. Convertirse temporalmente en root (`su` y `sudo -i`)
A veces, tienes que hacer 20 tareas de administración seguidas y escribir `sudo` antes de cada línea resulta agotador. Puedes abrir una sesión temporal como `root` directamente en tu terminal.

* **`sudo -i`** (o `sudo su`): Te convierte en `root`. Verás que el símbolo de tu *prompt* cambia de un dólar (`$`) a una almohadilla (`#`).
* **¡Cuidado!** Mientras veas el `#`, todo lo que escribas tiene poder destructivo.
* Para salir de este modo y volver a ser tu usuario normal, simplemente escribe **`exit`**.

## 📝 4. El archivo sudoers (¿Quién puede usar sudo?)
No todos los usuarios del sistema pueden usar `sudo`. Si creas una cuenta para tu hermano pequeño, no querrás que pueda instalar programas.

La lista de quién tiene permiso para usar la corona se guarda en un archivo hiper-protegido llamado `/etc/sudoers`. Cuando instalas Linux, tu primer usuario se añade automáticamente a un grupo especial (llamado `sudo` en Ubuntu o `wheel` en otras distros) que tiene permiso para usar este comando.

---
### 🧪 Mini reto práctico
Vamos a comprobar la diferencia de poder entre tu usuario y `root`. Intentaremos leer el archivo donde Linux guarda las contraseñas encriptadas de todos los usuarios (`/etc/shadow`), un archivo altamente confidencial.

1. Abre tu terminal.
2. Intenta leer el archivo como un usuario normal: 
   ```bash
   cat /etc/shadow
   ```
   *(Deberías recibir un mensaje de error: "Permiso denegado").*
3. Ahora, pídele prestada la corona a root:
   ```bash
   sudo cat /etc/shadow
   ```
4. Introduce tu contraseña. *(Ahora verás un montón de texto incomprensible; son las contraseñas cifradas del sistema. ¡Acabas de actuar como administrador!)*
5. Opcional: Entra en modo Dios escribiendo `sudo -i`, fíjate cómo el *prompt* termina en `#`, y luego escribe `exit` para volver a la seguridad.

---
[<- Volver al Módulo 5](../README.md) | [Siguiente: Gestión de Usuarios ->](../02-gestion-de-usuarios/README.md)