# Tema 5: Seguridad del Kernel con AppArmor (La jaula de contención)

Hemos fortificado SSH y configurado el Firewall. Nuestro perímetro es de hierro. Pero imagina este escenario: un atacante descubre una vulnerabilidad (Zero-Day) en el código de Nginx o en un plugin de tu WordPress. Logra engañar al servidor web para que ejecute comandos maliciosos. 

Como el atacante ya está "dentro", el Firewall no sirve de nada. Aquí es donde entra la última línea de defensa de Linux: **El Control de Acceso Obligatorio (MAC)** mediante **AppArmor**.

## 🛡️ 1. DAC vs MAC (¿Por qué los permisos no bastan?)
Hasta ahora conoces los permisos de lectura, escritura y ejecución (`rwx`). A esto se le llama **DAC** (Discretionary Access Control). Si un programa se ejecuta bajo el usuario `root`, tiene permisos DAC para hacer absolutamente lo que quiera en el sistema.

**AppArmor** implementa **MAC** (Mandatory Access Control). Funciona como un nivel de seguridad superior dictado directamente por el Kernel (el núcleo) de Linux. 
Con AppArmor, tú le das a cada programa un "perfil" (una lista de tareas permitidas). Si Nginx intenta abrir el archivo de contraseñas (`/etc/shadow`), AppArmor se lo prohibirá instantáneamente y hará saltar las alarmas, **incluso si Nginx está ejecutándose como `root`**.

## 🔍 2. Comprobando el estado de AppArmor
AppArmor viene preinstalado y activado por defecto en Ubuntu y Debian (CentOS/RedHat usan una alternativa similar llamada SELinux).

Vamos a comprobar que tu escudo invisible está encendido. Ejecuta:
```bash
sudo aa-status
```
*(O también puedes usar `sudo apparmor_status`)*.

Verás un resumen que te dirá:
1. Cuántos perfiles están cargados.
2. Cuántos perfiles están en modo **Enforce** (Cumplimiento estricto).
3. Cuántos perfiles están en modo **Complain** (Modo queja/auditoría).

## 🚦 3. Modos de Operación (Enforce vs Complain)
Los perfiles de AppArmor son archivos de texto que definen a qué carpetas y capacidades del sistema puede acceder un programa específico. Estos perfiles pueden estar en dos estados:

*   **Modo Complain (Aprendizaje):** Si Nginx intenta hacer algo prohibido, AppArmor **le deja hacerlo**, pero registra un mensaje de error grave en `/var/log/syslog`. Se usa para probar aplicaciones nuevas sin romperlas.
*   **Modo Enforce (Bloqueo activo):** Si Nginx intenta hacer algo prohibido, AppArmor **bloquea la acción** sin piedad y lo registra. Es el modo de producción.

## 🕵️‍♂️ 4. El escudo invisible en acción (Un ejemplo real)
No vamos a crear un perfil desde cero porque es un trabajo muy avanzado que requiere conocer el código exacto de cada aplicación, pero vamos a ver cómo los perfiles preinstalados te protegen en el día a día.

Por ejemplo, Docker genera perfiles de AppArmor automáticamente para tus contenedores. Si levantas un contenedor de WordPress comprometido, el hacker intentará escalar privilegios accediendo al hardware del servidor o a las carpetas del sistema operativo base.

Gracias al perfil `docker-default` de AppArmor, ese contenedor está enjaulado. Cualquier intento del hacker de salir del contenedor resultará en un "Permiso Denegado", y tú, como SysAdmin, verás este mensaje de alerta en tus logs:
```bash
sudo dmesg | grep apparmor | grep DENIED
```
*(Este comando busca en los mensajes del Kernel directamente las veces que AppArmor le ha parado los pies a un programa).*

## 🛑 5. Gestión de perfiles básicos
En Ubuntu, los perfiles de AppArmor se guardan en la carpeta `/etc/apparmor.d/`.

Si alguna vez instalas un programa oficial (como MariaDB o un servidor DNS) y por alguna extraña razón no arranca y lanza un error de "Permiso denegado" en sus propios archivos, es posible que su perfil de AppArmor esté desactualizado. 

Como SysAdmin, puedes pasar ese perfil a "Modo Complain" temporalmente para comprobar si AppArmor es el culpable de que falle:
```bash
sudo apt install apparmor-utils
sudo aa-complain /etc/apparmor.d/usr.sbin.mysqld
```
Y una vez solucionado, lo devuelves a la máxima seguridad:
```bash
sudo aa-enforce /etc/apparmor.d/usr.sbin.mysqld
```

---

### 🏆 ¡Felicidades, Comandante!
Has finalizado el **Módulo 11: Seguridad Avanzada y Hardening**. 

Tu servidor ya no es una víctima fácil. Has cerrado las vulnerabilidades básicas, has reemplazado las contraseñas por criptografía asimétrica, has instalado un sistema que banea atacantes en tiempo real (Fail2Ban), has mitigado ataques DoS (UFW Rate Limiting) y has comprendido cómo el Kernel enjaula los procesos comprometidos (AppArmor).

Ya tienes los conocimientos de infraestructura, contenedores y seguridad. El siguiente (y último) paso lógico es llevar todo esto al mundo real. Prepárate para el **Proyecto Final**.

---
[<- Anterior: Firewall Avanzado y Límites](../04-firewall-avanzado-y-limites/README.md) | [Volver al Roadmap del Bootcamp](../README.md)