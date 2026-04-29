# Tema 2: Acceso remoto con SSH (Teletransportación digital)

Imagina que tienes un servidor en un centro de datos en otra ciudad, o una Raspberry Pi conectada a tu router sin pantalla ni teclado. ¿Cómo lo controlas? La respuesta es **SSH** (*Secure Shell*).

SSH es un protocolo que te permite abrir una terminal en un ordenador remoto a través de la red. Todo lo que escribas en tu teclado se enviará de forma cifrada y se ejecutará en la otra máquina.



## 🔑 1. ¿Qué necesito para conectarme?
Para entrar en otro Linux por SSH, necesitas tres datos:
1.  **La dirección IP** del ordenador remoto (la aprendimos a sacar con `ip a`).
2.  **Un nombre de usuario** que exista en esa máquina.
3.  **La contraseña** de ese usuario.

## 🚀 2. El comando de conexión
La sintaxis es muy intuitiva, es como escribir una dirección de correo electrónico:

```bash
ssh usuario@direccion_ip
```

**Ejemplo real:**
```bash
ssh alicia@192.168.1.50
```

### ¿Qué pasa la primera vez?
Cuando te conectas a un equipo por primera vez, SSH te mostrará un aviso diciendo que no conoce la "huella digital" (*fingerprint*) de ese equipo y te preguntará si confías en él.
* Escribe **`yes`** y pulsa Enter.
* A partir de ahí, el equipo se guardará en tu lista de "conocidos" (`~/.ssh/known_hosts`).
* Luego te pedirá la contraseña (recuerda que en Linux no se ven asteriscos al escribir claves).

## 🛠️ 3. Preparando el servidor (`openssh-server`)
Por seguridad, la mayoría de las distribuciones de escritorio (como Ubuntu) traen el "cliente" SSH instalado (para que tú puedas entrar en otros), pero no traen el "servidor" (para que otros entren en ti).

Si quieres que tu máquina virtual pueda recibir conexiones, debes instalar el servicio:

```bash
sudo apt update
sudo apt install openssh-server
```

Una vez instalado, el servicio se activa solo. Puedes comprobar que está "escuchando" visitas con:
```bash
sudo systemctl status ssh
```

## 🔐 4. Seguridad Básica: El Puerto 22
Por defecto, SSH siempre viaja por el **Puerto 22**. Es como la "puerta número 22" de tu ordenador. Los hackers siempre escanean este puerto para intentar entrar por la fuerza bruta.

**Consejo de oro:** Si alguna vez expones un servidor real a internet, una de las primeras medidas de seguridad es cambiar el puerto 22 por uno aleatorio (como el 4532) para pasar desapercibido.

---

### 🧪 Mini reto práctico
Vamos a hacer un "Inception": vamos a conectarnos por SSH a nuestra propia máquina. Es la mejor forma de probar si tu servidor SSH funciona sin necesitar un segundo ordenador.

1.  Asegúrate de tener el servidor instalado: `sudo apt install openssh-server`.
2.  Averigua tu IP local: `ip a` (supongamos que es `192.168.1.15`).
3.  Intenta entrar en tu propio equipo:
    ```bash
    ssh tu_usuario@localhost
    ```
    *(También puedes usar `ssh tu_usuario@127.0.0.1` o tu IP real).*
4.  Acepta la huella digital escribiendo `yes`.
5.  Introduce tu contraseña.
6.  Fíjate en el mensaje de bienvenida. ¡Ahora estás dentro de una sesión remota... de ti mismo!
7.  Para terminar la conexión remota y volver a tu terminal normal, escribe: **`exit`**.

---
[<- Anterior: Conceptos y comandos de red](../01-conceptos-y-comandos-de-red/README.md) | [Volver al Módulo 7](../README.md) | [Siguiente: Transferencia de archivos (SCP y SFTP) ->](../03-transferencia-de-archivos/README.md)