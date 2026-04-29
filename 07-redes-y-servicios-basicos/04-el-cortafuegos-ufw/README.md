# Tema 4: El cortafuegos UFW (Blindando tu sistema)

Tener un servidor con SSH (puerto 22) activo es genial, pero también es una invitación para que bots de todo el mundo intenten entrar en tu máquina. En Linux, usamos un **Cortafuegos** (Firewall) para decidir qué tráfico permitimos entrar y cuál bloqueamos radicalmente.

En Ubuntu y distribuciones basadas en Debian, la herramienta reina es **UFW**. Su nombre lo dice todo: *Uncomplicated Firewall*. Es una capa sencilla que maneja las complejas reglas internas del sistema (`iptables`).



## 🛡️ 1. Estado del cortafuegos
Por defecto, en la mayoría de sistemas de escritorio, UFW viene instalado pero **desactivado**. Para ver si está funcionando, ejecuta:

```bash
sudo ufw status
```
*Si dice `Status: inactive`, tu sistema está totalmente abierto.*

## 🚀 2. La regla de oro del Administrador
Antes de encender el cortafuegos, los profesionales aplicamos dos reglas básicas de política general:
1. **Denegar todo lo que entra:** `sudo ufw default deny incoming`
2. **Permitir todo lo que sale:** `sudo ufw default allow outgoing`

Esto significa: *"Nadie entra a menos que yo le dé permiso explícito, pero mi ordenador puede conectarse a internet libremente"*.

## 🔑 3. Abriendo puertas (Allow)
Si activas el cortafuegos sin abrir el puerto de SSH, **te quedarás fuera de tu propio servidor** la próxima vez que intentes entrar de forma remota.

* **Permitir un servicio por nombre:**
  ```bash
  sudo ufw allow ssh
  ```
* **Permitir un puerto específico (ej. el 80 para una web):**
  ```bash
  sudo ufw allow 80/tcp
  ```

## 🔌 4. Activación y Desactivación
Una vez que hayas configurado tus permisos (al menos el de SSH), puedes encenderlo:

* **Activar:** `sudo ufw enable`
* **Desactivar:** `sudo ufw disable`

Si ahora ejecutas `sudo ufw status`, verás una lista limpia de qué puertos están abiertos y cuáles no.

## 🗑️ 5. Borrar reglas
Si te equivocas o ya no necesitas un puerto abierto, puedes borrar la regla fácilmente:
```bash
sudo ufw delete allow 80/tcp
```

---

### 🧪 Mini reto práctico
Vamos a configurar una seguridad básica pero profesional en tu máquina.

1.  **Mira el estado inicial:** `sudo ufw status`.
2.  **Asegura tu entrada remota:** `sudo ufw allow ssh`. (¡Muy importante!).
3.  **Activa el firewall:** `sudo ufw enable`. (Confirma con 'y' si te pregunta).
4.  **Simula que montas un servidor web:** Abre el puerto 80 (`sudo ufw allow 80`).
5.  **Comprueba el resultado:** `sudo ufw status numbered`.
    * *Nota: La opción `numbered` es genial porque te da un número de índice para cada regla, lo que facilita borrarlas después con `sudo ufw delete [número]`.*

---
[<- Anterior: Transferencia de archivos (SCP y SFTP)](../03-transferencia-de-archivos/README.md) | [Volver al Módulo 7](../README.md) | [Siguiente: Gestión de servicios con Systemd ->](../05-gestion-de-servicios-systemd/README.md)