# Tema 5: Gestión de servicios (Systemd y systemctl)

¿Alguna vez te has preguntado cómo es que el servidor SSH está siempre listo para recibirte, incluso si acabas de reiniciar el ordenador? No es magia, es un **Servicio** (también llamado *demonio* o *daemon*).

En las distribuciones modernas, el director de orquesta que decide qué programas arrancan, cuáles se detienen y cuáles deben reiniciarse si fallan es **systemd**. Nosotros nos comunicamos con él a través del comando **`systemctl`**.



## 🕹️ 1. Los 5 comandos esenciales
La sintaxis de `systemctl` es muy lógica: `sudo systemctl [acción] [nombre_del_servicio]`.

Tomemos como ejemplo el servicio de SSH (llamado `ssh` en Ubuntu/Debian):

1. **Ver el estado:** ¿Está vivo o muerto?
   ```bash
   systemctl status ssh
   ```
2. **Parar un servicio:** Detenerlo inmediatamente.
   ```bash
   sudo systemctl stop ssh
   ```
3. **Iniciar un servicio:** Arrancarlo ahora mismo.
   ```bash
   sudo systemctl start ssh
   ```
4. **Reiniciar:** Útil cuando cambias una configuración y quieres que se aplique.
   ```bash
   sudo systemctl restart ssh
   ```
5. **Recargar (Reload):** Como el reiniciar, pero sin cortar la conexión de los usuarios (no todos los servicios lo soportan).
   ```bash
   sudo systemctl reload ssh
   ```

## 🏎️ 2. ¿Qué pasa cuando el PC se enciende? (Enable vs Start)
Este es el error más común de los principiantes. Confundir `start` con `enable`.

* **`start` / `stop`:** Afecta al **ahora mismo**. Si apagas el PC, ese estado se olvida.
* **`enable`:** Le dice a Linux: *"Quiero que este programa arranque automáticamente cada vez que el ordenador se encienda"*.
* **`disable`:** El programa ya no arrancará solo al inicio (pero puedes iniciarlo tú a mano cuando quieras).

**Ejemplo profesional:**
```bash
sudo systemctl enable ssh
```

## 📋 3. Listar todos los servicios
Si quieres ver todo lo que tu ordenador está ejecutando en segundo plano, puedes pedirle a systemd una lista completa:
```bash
systemctl list-units --type=service
```

## 🔍 4. Leyendo el estado (Status)
Cuando haces un `systemctl status`, fíjate en estos puntos clave:
* **Loaded:** Si el servicio está instalado y cargado.
* **Active:** Si está `active (running)` (todo bien) o `inactive (dead)` (parado).
* **Logs:** Debajo del estado, systemctl te muestra las últimas líneas de lo que el programa ha dicho (muy útil si el servicio da error al arrancar).

---

### 🧪 Mini reto práctico
Vamos a jugar con el servicio del cortafuegos que aprendimos en el tema anterior (`ufw`).

1. **Consulta el estado:** `systemctl status ufw`. Verás que está "active" si lo encendiste ayer.
2. **Detén el servicio:** `sudo systemctl stop ufw`.
3. **Comprueba el estado:** `systemctl status ufw`. Ahora dirá "inactive (dead)".
4. **Prueba de persistencia:** Si ahora haces `sudo ufw status`, verás que el cortafuegos está apagado.
5. **Vuelve a la normalidad:** `sudo systemctl start ufw`.

---
[<- Anterior: El cortafuegos UFW](../04-el-cortafuegos-ufw/README.md) | [Volver al Módulo 7](../README.md) | [Siguiente: Análisis de puertos y red ->](../06-analisis-de-puertos-y-red/README.md)