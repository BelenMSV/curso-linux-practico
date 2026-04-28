# Tema 2: Gestión de Usuarios (Crear, modificar y destruir)

Como mencionamos en la introducción, Linux nació con la mentalidad de que un servidor iba a ser utilizado por decenas de personas a la vez. Cada persona necesita su propio espacio privado (su carpeta personal en `/home`), sus propias configuraciones y su propia contraseña.

Incluso si usas tu ordenador tú solo, los programas que instalas (como bases de datos o servidores web) a menudo crean "usuarios invisibles" por motivos de seguridad, para aislar sus procesos del resto del sistema.

Vamos a aprender cómo gestionar quién entra en nuestro sistema. Como estas son tareas críticas, **todos estos comandos requerirán el uso de `sudo`**.



## 🧑‍💻 1. Crear un usuario nuevo (`adduser`)
En el ecosistema Ubuntu/Mint (y Debian en general), disponemos de un comando maravillosamente interactivo para crear usuarios llamado `adduser`. 

*Nota: Existe otro comando llamado `useradd`, pero es de muy bajo nivel, no crea la carpeta personal por defecto y es más difícil de usar. Acostúmbrate a usar `adduser`.*

Para crear un usuario llamado "pedro", ejecutamos:
```bash
sudo adduser pedro
```

**¿Qué hace este comando automáticamente?**
1. Crea la cuenta de usuario "pedro".
2. Crea una carpeta privada para él en `/home/pedro`.
3. Te pide que le asignes una **contraseña** (y que la repitas por seguridad).
4. Te hace una serie de preguntas opcionales (Nombre completo, Teléfono, etc.). Puedes simplemente pulsar `Enter` para saltártelas.

## 🔑 2. Cambiar contraseñas (`passwd`)
Las contraseñas no son eternas. Si necesitas cambiar la tuya o la de otro usuario, usamos el comando `passwd`.

* **Cambiar TU propia contraseña:**
  ```bash
  passwd
  ```
  *(El sistema te pedirá tu contraseña actual por seguridad, y luego la nueva).*

* **Cambiar la contraseña de OTRO usuario (Requiere poder de root):**
  Imagina que "pedro" ha olvidado su clave. Como administrador, puedes forzar un cambio de contraseña sin saber cuál era la antigua:
  ```bash
  sudo passwd pedro
  ```

## 🔄 3. Cambiar de usuario en la terminal (`su`)
Si has creado un usuario nuevo y quieres comprobar que funciona, no hace falta que cierres tu sesión gráfica. Puedes cambiar de usuario directamente desde la terminal usando `su` (*Switch User*).

```bash
su - pedro
```
* **Importante:** El guion (`-`) no es un adorno. Le indica al sistema que cargue el "entorno" del nuevo usuario, es decir, que te teletransporte directamente a la carpeta `/home/pedro` y cargue sus configuraciones personales.

Para volver a tu usuario original, simplemente escribe `exit` y pulsa Enter.

## 🗑️ 4. Borrar un usuario (`deluser`)
Cuando un usuario ya no necesita acceso al sistema, debemos eliminar su cuenta por seguridad. Para ello usamos `deluser`.

* **Borrar solo la cuenta (pero conservar sus archivos):**
  ```bash
  sudo deluser pedro
  ```
  *(La cuenta desaparece, pero la carpeta `/home/pedro` y sus documentos seguirán ahí por si necesitas recuperarlos).*

* **Borrar la cuenta y destruir sus archivos:**
  Si quieres eliminar cualquier rastro de esa persona en el ordenador, debes añadir un modificador:
  ```bash
  sudo deluser --remove-home pedro
  ```

---
### 🧪 Mini reto práctico
Vamos a crearle una cuenta a un amigo imaginario y a comprobar el aislamiento de Linux.

1. Abre tu terminal.
2. Crea un usuario llamado "invitado": `sudo adduser invitado` (asígnale una contraseña sencilla como "1234").
3. Cambia tu sesión a la de ese nuevo usuario: `su - invitado`
4. Comprueba quién eres escribiendo: `whoami`. Debería responder "invitado".
5. Comprueba dónde estás escribiendo: `pwd`. Debería decir `/home/invitado`.
6. ¡Intenta leer una carpeta que no es tuya! Escribe: `ls /root` o intenta entrar en tu carpeta de usuario original `cd /home/tu_usuario_real`. Deberías recibir un mensaje de "Permiso denegado".
7. Sal de la cuenta del invitado: `exit`
8. Borra al invitado y todas sus cosas para dejar el sistema limpio: `sudo deluser --remove-home invitado`

---
[<- Anterior: El usuario Root y sudo](../01-el-usuario-root-y-sudo/README.md) | [Volver al Módulo 5](../README.md) | [Siguiente: Gestión de Grupos ->](../03-gestion-de-grupos/README.md)