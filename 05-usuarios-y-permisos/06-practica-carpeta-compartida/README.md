# Tema 6: Práctica Integradora (El reto de la Carpeta Compartida)

Has aprendido a crear usuarios, organizar grupos y calcular la matriz numérica de permisos. Ahora vamos a unir todas las piezas del puzzle en un escenario 100% real de oficina.

## 🏢 El Escenario

Imagina que eres el nuevo Administrador de Sistemas (SysAdmin) de una empresa. La directora te ha asignado tu primera tarea:

> *"Necesitamos crear una carpeta para el departamento de Recursos Humanos (RRHH). En ese departamento trabajan **Alicia** y **Roberto**. Necesito que ambos puedan entrar a esa carpeta y crear o borrar archivos. Además, tenemos un becario llamado **Carlos**; por seguridad, Carlos no debe poder ver ni entrar en esa carpeta bajo ninguna circunstancia."*

¡Aceptamos el reto! Vamos a resolverlo paso a paso.



## 🛠️ Paso 1: Preparar a los actores (Usuarios y Grupos)
Primero, necesitamos crear el grupo y a nuestros tres empleados. (Recuerda que todas estas acciones afectan al sistema global, así que usaremos `sudo`).

1. **Crear el grupo del departamento:**
   ```bash
   sudo groupadd rrhh
   ```
2. **Crear los usuarios (inventa una contraseña sencilla para ellos, como '1234'):**
   ```bash
   sudo adduser alicia
   sudo adduser roberto
   sudo adduser carlos
   ```
3. **Añadir a Alicia y Roberto al grupo de RRHH (¡Recuerda el `-aG`!):**
   ```bash
   sudo usermod -aG rrhh alicia
   sudo usermod -aG rrhh roberto
   ```

## 📁 Paso 2: Crear la carpeta compartida
Por norma general, las carpetas compartidas de una empresa no se guardan dentro de la carpeta personal (`/home`) de un usuario, sino en el directorio raíz o en carpetas públicas como `/opt` o `/srv`.

Vamos a crear la carpeta en la raíz de nuestro disco duro:
```bash
sudo mkdir /Compartido_RRHH
```

## 🔐 Paso 3: Aplicar la seguridad (El truco de magia)
Si hacemos ahora un `ls -l /`, veremos que nuestra nueva carpeta tiene los permisos por defecto: `drwxr-xr-x` y pertenece a `root:root`. Eso significa que cualquiera puede entrar a mirar. ¡Tenemos que cerrarla!

1. **Cambiar el grupo dueño de la carpeta:**
   Queremos que el dueño siga siendo `root` (por seguridad), pero que el grupo dueño pase a ser `rrhh`.
   ```bash
   sudo chown root:rrhh /Compartido_RRHH
   ```

2. **Calcular y aplicar la matriz numérica (`chmod`):**
   Pensemos qué permisos queremos:
   * **Dueño (`root`):** Debe poder hacer todo -> **7** (`rwx`)
   * **Grupo (`rrhh`):** Debe poder leer, escribir y entrar -> **7** (`rwx`)
   * **Otros (como Carlos):** ¡No pueden hacer nada! -> **0** (`---`)

   Aplicamos nuestro código numérico mágico (770):
   ```bash
   sudo chmod 770 /Compartido_RRHH
   ```

Comprobamos que todo está correcto escribiendo `ls -l / | grep Compartido`. Deberíamos ver: `drwxrwx--- root rrhh`. ¡Perfecto!

## 🧪 Paso 4: La prueba de fuego
Ha llegado el momento de comprobar si hemos configurado bien nuestro sistema simulando que somos los empleados.

1. **Inicia sesión como Roberto:**
   ```bash
   su - roberto
   ```
2. **Roberto intenta entrar y crear un documento:**
   ```bash
   cd /Compartido_RRHH
   touch nominas.txt
   ```
   *(¡No debería dar ningún error! Roberto ha podido entrar y crear un archivo. Salimos escribiendo `exit`).*

3. **Inicia sesión como Carlos (El becario):**
   ```bash
   su - carlos
   ```
4. **Carlos intenta cotillear la carpeta:**
   ```bash
   cd /Compartido_RRHH
   ```
   *(La terminal debe responderle con un contundente: **"bash: cd: /Compartido_RRHH: Permiso denegado"**).*

> 💡 **Nota Pro (El Bit Sticky):** Si eres un alumno curioso, te habrás dado cuenta de un detalle: Si Roberto crea un archivo dentro de la carpeta compartida, el archivo será propiedad de Roberto, y a lo mejor Alicia no puede borrarlo. Para forzar que todos los archivos creados ahí dentro pertenezcan siempre al grupo `rrhh`, los administradores usan un "4º número secreto" en chmod llamado *SetGID*. El comando sería `chmod 2770 /Compartido_RRHH`. 

---
### 🎉 ¡Fin del Módulo 5!
¡Misión cumplida, SysAdmin! Acabas de diseñar tu primer entorno seguro.

Has comprendido que Linux no confía en nadie por defecto y que todo, absolutamente todo en el sistema, obedece a las reglas que impongas en su matriz de permisos. 

---
[<- Anterior: Modificando Permisos y Propietarios](../05-modificando-permisos-y-propietarios/README.md) | [Volver al Módulo 5](../README.md)