# Tema 1: Conceptos y comandos de red (Tu DNI digital)

Para que dos ordenadores se comuniquen, necesitan saber "dónde" está el otro. En el mundo de las redes, no usamos nombres de calles, usamos números. Entender cómo tu sistema Linux maneja estos números es el primer paso para dominar las redes.

## 🌐 1. Conceptos Básicos: IP, Máscara y Puerta de Enlace

Antes de teclear comandos, debemos tener claros tres conceptos fundamentales de cualquier red (ya sea la wifi de tu casa o los servidores de Google):

* **Dirección IP (Internet Protocol):** Es el número de teléfono de tu ordenador. Nadie más en tu red puede tener el mismo número. Suele tener el formato `192.168.1.50`.
* **Puerta de Enlace (Gateway):** Es la IP de tu router. Es el "jefe" de la red local. Si tu ordenador quiere hablar con un equipo que está fuera de tu casa (en internet), le entrega el mensaje a la Puerta de Enlace para que lo saque al exterior.
* **DNS (Domain Name System):** Los humanos somos malos memorizando números como `142.250.184.46`. El DNS es una agenda telefónica que traduce nombres fáciles como `google.com` a su dirección IP real.



## 🔍 2. ¿Cuál es mi IP? (El comando `ip`)

Durante muchos años, el comando rey para ver tu IP en Linux fue `ifconfig` (y si vienes de Windows, te sonará `ipconfig`). Sin embargo, en los sistemas Linux modernos, `ifconfig` se considera obsoleto y ha sido reemplazado por un comando mucho más potente y corto: **`ip`**.

Para ver tus direcciones IP, ejecuta:
```bash
ip a
```
*(La 'a' es la abreviatura de 'address' - dirección).*

**Cómo leer la salida de `ip a`:**
Verás varios bloques de texto, cada uno representa una "tarjeta de red" de tu ordenador:
1.  **`lo` (Loopback):** Es una tarjeta virtual. Su IP siempre es `127.0.0.1`. Se usa para que el ordenador hable consigo mismo.
2.  **`eth0`, `enp3s0` (Nombres que empiezan por 'e'):** Es tu tarjeta de red por cable (Ethernet).
3.  **`wlan0`, `wlp2s0` (Nombres que empiezan por 'w'):** Es tu tarjeta de red inalámbrica (Wi-Fi).

Busca la línea que dice **`inet`** dentro de tu tarjeta conectada. Esa es tu dirección IP local.

## 🚪 3. ¿Cuál es mi Router? (El comando `ip route`)

Si quieres saber cuál es la IP de tu Puerta de Enlace (tu router), puedes usar el comando que nos muestra la tabla de rutas del sistema:

```bash
ip route
```
Busca la línea que empieza por la palabra **`default via`**. El número que viene a continuación (casi siempre `192.168.1.1` o `192.168.0.1`) es tu router.

## 🏓 4. ¿Hay alguien ahí? (El comando `ping`)

El comando `ping` es el sónar de los submarinos aplicado a la informática. Envías un paquete de datos a una IP y esperas a que rebote y vuelva. Sirve para saber si un ordenador está encendido y conectado.

```bash
ping google.com
```

> ☢️ **¡ATENCIÓN A LA DIFERENCIA CON WINDOWS!**
> En Windows, si haces un ping, envía 4 paquetes y se detiene solo. **En Linux, el ping es infinito.** Seguirá enviando paquetes hasta el fin de los tiempos para que puedas monitorizar caídas de red en tiempo real. 
> **Para detener un ping en Linux, debes pulsar `Ctrl + C`.**

Si quieres que Linux solo envíe una cantidad concreta de paquetes (por ejemplo, 4), debes usar la bandera `-c` (count):
```bash
ping -c 4 google.com
```

---

### 🧪 Mini reto práctico
Vamos a hacer un diagnóstico completo de tu red para comprobar que tienes conexión tanto local como internacional.

1.  Abre tu terminal.
2.  **Descubre tu IP:** Ejecuta `ip a` y localiza tu IP local en la línea `inet`. Apúntala mentalmente.
3.  **Descubre tu router:** Ejecuta `ip route`. Fíjate en la IP que aparece después de `default via`.
4.  **Prueba la red local:** Haz un ping a tu router para ver si el cable o el Wi-Fi funcionan bien: `ping -c 4 [IP_DE_TU_ROUTER]`. Si responde, tu conexión en casa es perfecta.
5.  **Prueba la red exterior (Internet):** Haz un ping a los servidores DNS de Google: `ping -c 4 8.8.8.8`.
6.  **Prueba el DNS:** Haz un ping a un nombre: `ping -c 4 wikipedia.org`. Si responde, significa que tu ordenador sabe traducir nombres a IPs correctamente.

---
[<- Volver al Módulo 7](../README.md) | [Siguiente: Acceso remoto con SSH ->](../02-acceso-remoto-con-ssh/README.md)