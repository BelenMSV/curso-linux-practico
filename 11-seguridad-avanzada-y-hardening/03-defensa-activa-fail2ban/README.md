# Tema 3: Defensa Activa con Fail2Ban (Tu perro guardián)

Prohibir las contraseñas está muy bien, pero los atacantes automatizados no lo saben. Seguirán intentando conectarse cientos de veces por minuto. Aunque no puedan entrar, este "ruido" continuo satura el servidor y dificulta la lectura de los logs reales.

Aquí es donde entra **Fail2Ban**. Es un sistema de prevención de intrusos (IPS) increíblemente ingenioso. 



## 🧠 1. ¿Cómo funciona Fail2Ban?
Fail2Ban se pasa el día leyendo tus archivos de registro (logs) en tiempo real, como si estuviera ejecutando un `tail -f`. 

Si detecta que una misma dirección IP ha fallado al iniciar sesión 5 veces en los últimos 10 minutos (por ejemplo), Fail2Ban se comunica inmediatamente con tu Firewall (UFW o iptables) y crea una regla para **bloquear (banear) esa IP** durante el tiempo que tú decidas.

## 🛠️ 2. Instalación de Fail2Ban
Como siempre, empezamos actualizando e instalando el paquete desde los repositorios oficiales:
```bash
sudo apt update
sudo apt install fail2ban -y
```

Una vez instalado, el servicio se iniciará automáticamente en segundo plano.

## 👮 3. Configurando "La Cárcel" (`jail.local`)
Fail2Ban llama a sus configuraciones **"Jails"** (Cárceles). Cada servicio (SSH, Nginx, MariaDB) tiene su propia cárcel.

**Regla de oro de Fail2Ban:** NUNCA modifiques el archivo de configuración original (`/etc/fail2ban/jail.conf`), porque cuando el programa se actualice, borrará tus cambios. Siempre debes crear una copia llamada `jail.local`. Fail2Ban leerá este archivo con prioridad.

1.  Copia el archivo de configuración:
    ```bash
    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
    ```
2.  Abre tu nuevo archivo para editarlo:
    ```bash
    sudo nano /etc/fail2ban/jail.local
    
```
3.  Busca la sección `[DEFAULT]` (suele estar al principio). Aquí definiremos las reglas globales para todas las cárceles. Configura estos tres parámetros clave:
    *   `bantime = 1h` *(El tiempo que el atacante pasará bloqueado. Puedes usar `10m`, `1h`, `1d` (un día), o `-1` para un baneo permanente).*
    *   `findtime = 10m` *(La ventana de tiempo en la que se cuentan los fallos).*
    *   `maxretry = 5` *(El número de intentos fallidos permitidos antes de lanzar el martillo del ban).*
4.  Guarda (Ctrl+O, Enter) y sal (Ctrl+X).

## 🚀 4. Activando el servicio
Para que Fail2Ban lea nuestras nuevas reglas, debemos reiniciar el servicio:

```bash
sudo systemctl restart fail2ban
sudo systemctl enable fail2ban
```

## 📊 5. El panel de control del guardia (`fail2ban-client`)
Fail2Ban tiene su propio comando para interactuar con él y ver cómo va la caza de hackers.

Para ver un resumen general de las cárceles activas (por defecto, la cárcel de `sshd` siempre viene activada):
```bash
sudo fail2ban-client status
```

Para ver información detallada de una cárcel específica (ej. `sshd`) y **ver la lista exacta de IPs que están bloqueadas en este momento**:
```bash
sudo fail2ban-client status sshd
```

## 🔓 6. El indulto (Cómo desbanear una IP)
*¿Qué pasa si te equivocas de contraseña o de llave varias veces y tu propio servidor te banea a ti?* 
¡Tranquilidad! Si puedes acceder al servidor desde otra IP (por ejemplo, desde los datos móviles de tu teléfono, o usando la consola web de tu proveedor Cloud), puedes levantar el castigo manualmente.

Ejecuta este comando, cambiando `TU_IP` por la dirección bloqueada:
```bash
sudo fail2ban-client set sshd unbanip TU_IP
```

---

### 🛡️ Conclusión de Defensa Activa
Con Fail2Ban y las llaves SSH configuradas, tu servidor acaba de pasar de ser un blanco fácil a ser una fortaleza que se defiende sola. Puedes dormir tranquilo sabiendo que cualquier bot que intente hacer ruido será silenciado por el firewall en cuestión de segundos.

---
[<- Anterior: Fortificando SSH](../02-fortificando-ssh-llaves-criptograficas/README.md) | [Volver al Módulo 11](../README.md) | [Siguiente: Firewall Avanzado y Límites ->](../04-firewall-avanzado-y-limites/README.md)