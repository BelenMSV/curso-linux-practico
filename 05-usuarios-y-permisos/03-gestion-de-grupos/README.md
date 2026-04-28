# Tema 3: Gestión de Grupos (Organizando equipos)

Imagina que eres el administrador de sistemas de una empresa con 50 empleados en el departamento de "Contabilidad". Tienes una carpeta con las facturas del año. Si tuvieras que darle permiso de lectura a esa carpeta usuario por usuario, perderías horas. 

Para solucionar esto, Linux utiliza los **Grupos**. Creas un grupo llamado "contabilidad", le das permisos a la carpeta para que ese grupo pueda leerla, y luego simplemente metes a los 50 usuarios dentro del grupo. 



## 👥 1. Grupos Principales vs Secundarios
En Linux, un usuario puede pertenecer a muchos grupos al mismo tiempo, pero hay una diferencia fundamental:

* **Grupo Principal:** Cuando creaste tu usuario (ej. `pedro`), Linux creó automáticamente un grupo privado llamado exactamente igual (`pedro`) y te asignó a él como tu grupo principal. Todo archivo nuevo que crees pertenecerá a este grupo.
* **Grupos Secundarios:** Son los grupos adicionales a los que te añaden para darte privilegios extra (por ejemplo, el grupo `sudo` para poder administrar el equipo, o el grupo `cdrom` para usar la disquetera).

## 🏗️ 2. Crear y destruir grupos (`groupadd` y `groupdel`)
La creación de grupos es extremadamente sencilla y silenciosa (no te pide confirmación ni contraseñas adicionales).

* **Para crear un grupo nuevo:**
  ```bash
  sudo groupadd desarrolladores
  ```
* **Para borrar un grupo:**
  ```bash
  sudo groupdel desarrolladores
  ```

## ➕ 3. Añadir un usuario a un grupo (`usermod`)
Aquí es donde debes prestar muchísima atención. El comando para modificar las propiedades de un usuario es `usermod`. Para añadir a un usuario a un grupo secundario, usamos las banderas `-aG`.

Imagina que queremos meter al usuario `pedro` en el grupo `desarrolladores`:
```bash
sudo usermod -aG desarrolladores pedro
```

> ☢️ **¡CUIDADO! La trampa de `usermod`:** > La letra `-a` significa *Append* (Añadir), y la `-G` significa *Groups* (Grupos). 
> Si por error ejecutas `sudo usermod -G desarrolladores pedro` (sin la `a`), le estás diciendo a Linux: *"Saca a Pedro de absolutamente todos los grupos en los que estaba y mételo SOLO en desarrolladores"*. Si haces esto, Pedro perderá su grupo `sudo` y ya no podrá administrar el sistema. **Usa siempre `-aG`**.

## 🚪 4. Quitar a un usuario de un grupo (`gpasswd`)
Si Pedro cambia de departamento y ya no debe tener acceso a las herramientas de desarrollo, podemos sacarlo del grupo usando el comando `gpasswd` con la opción `-d` (Delete).

```bash
sudo gpasswd -d pedro desarrolladores
```

## 🔍 5. ¿A qué grupos pertenezco? (`groups` e `id`)
Para verificar si los cambios se han aplicado correctamente, tienes dos comandos muy útiles:

* **`groups`:** Te muestra una lista simple de los grupos a los que pertenece el usuario actual. Si quieres ver los de otro usuario, añade su nombre: `groups pedro`.
* **`id`:** Te muestra la misma información pero de forma más técnica, incluyendo los identificadores numéricos (UID para el usuario, GID para el grupo) que usa el Kernel de Linux internamente.

> ⚠️ **Nota vital:** Cuando te añades a un grupo nuevo, **el cambio no tiene efecto en tu terminal actual**. Para que Linux reconozca tus nuevos permisos, debes cerrar sesión y volver a entrar (o usar el comando `newgrp nombre_grupo` o `su - tu_usuario` para recargar la sesión).

---
### 🧪 Mini reto práctico
Vamos a crear un grupo "secreto" y a meternos dentro.
1. Abre tu terminal.
2. Comprueba a qué grupos perteneces ahora mismo: `groups`
3. Crea un nuevo grupo llamado "hackers": `sudo groupadd hackers`
4. Añade tu propio usuario a ese grupo (¡recuerda usar `-aG`!): `sudo usermod -aG hackers tu_nombre_de_usuario`
5. Escribe `groups` de nuevo. ¿Aparece "hackers"? Seguramente no.
6. Recarga tu sesión en la terminal tecleando: `su - tu_nombre_de_usuario` (te pedirá tu contraseña).
7. Vuelve a escribir `groups`. ¡Ahora sí deberías ser oficialmente un miembro del grupo hackers!

---
[<- Anterior: Gestión de Usuarios](../02-gestion-de-usuarios/README.md) | [Volver al Módulo 5](../README.md) | [Siguiente: La Matriz de Permisos ->](../04-la-matriz-de-permisos/README.md)