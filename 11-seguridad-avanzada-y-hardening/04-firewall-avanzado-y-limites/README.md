# Tema 4: Firewall Avanzado y Límites (Rate Limiting)

Hasta ahora hemos usado UFW (Uncomplicated Firewall) como un guardia de seguridad binario: o te deja pasar (`allow`) o no te deja pasar (`deny`). 

Pero, ¿qué ocurre si tienes un puerto abierto legalmente (como el puerto 80 para tu web o el 22 para SSH), y un atacante decide enviarte 10.000 peticiones por segundo para intentar tumbar tu servidor? A esto se le conoce como un ataque **DoS** (Denegación de Servicio). 

Para mitigar esto, usamos una técnica llamada **Rate Limiting** (Limitación de Tasa).

## 🚦 1. ¿Qué es el Rate Limiting?
El Rate Limiting consiste en decirle al firewall: *"Permite el tráfico en este puerto, pero si una misma dirección IP realiza demasiadas conexiones en muy poco tiempo, bloquéala temporalmente"*.

Es una capa de seguridad excelente que trabaja en equipo con Fail2Ban. Mientras Fail2Ban lee los logs buscando contraseñas incorrectas, UFW simplemente cuenta paquetes a nivel de red, lo cual es muchísimo más rápido y consume menos CPU.

## 🛑 2. Aplicando límites con UFW
UFW tiene una regla integrada y preconfigurada exactamente para esto. El comando mágico es `limit`.

Si en el Módulo 7 abrimos el puerto SSH con `sudo ufw allow ssh`, ahora vamos a reemplazar esa regla por una más estricta:
```bash
sudo ufw limit ssh
```
*(También puedes usar el número del puerto: `sudo ufw limit 22/tcp`)*.

**¿Qué hace exactamente este comando?**
Por defecto, la regla `limit` de UFW denegará las conexiones desde una IP si esa misma IP ha intentado iniciar **6 o más conexiones en los últimos 30 segundos**. Es el equilibrio perfecto: te permite a ti iniciar sesión sin problemas, pero frena en seco a los scripts automatizados.

Puedes comprobar que la regla se ha aplicado ejecutando:
```bash
sudo ufw status
```
*(Verás que la acción ahora dice `LIMIT` en lugar de `ALLOW`).*

## 🎯 3. Reglas Granulares (Listas Blancas)
Una de las peores prácticas en ciberseguridad es abrir un puerto de administración al mundo entero si no es necesario. 

Imagina que tienes una base de datos MariaDB (puerto 3306) a la que necesitas conectarte desde tu casa. Si haces `ufw allow 3306`, todo el planeta podrá ver tu base de datos. Lo correcto es crear una **Lista Blanca**, permitiendo el acceso *solo* a tu IP pública.

El comando sería así (sustituyendo la IP por la tuya):
```bash
sudo ufw allow from 198.51.100.25 to any port 3306
```

Y para bloquear explícitamente a un atacante pesado del que ya conoces la IP:
```bash
sudo ufw deny from 203.0.113.50
```

*Recuerda que en UFW, las reglas se leen de arriba a abajo. Asegúrate de poner tus reglas de bloqueo o listas blancas específicas antes de las reglas generales.*

## 📝 4. Activando el modo chivato (Logs de UFW)
A veces las cosas no funcionan, un contenedor de Docker no se conecta o un cliente no puede entrar a la web, y sospechas que el Firewall tiene la culpa. UFW puede registrar todo el tráfico que bloquea, pero esta función suele venir desactivada para ahorrar espacio en disco.

Para encender los logs de nivel bajo (registra solo los paquetes bloqueados):
```bash
sudo ufw logging on
```

Una vez activado, si UFW bloquea un paquete, dejará un mensaje en el archivo del kernel. Puedes ver a UFW trabajando en tiempo real con este comando:
```bash
sudo tail -f /var/log/syslog | grep "\[UFW BLOCK\]"
```

Si alguna vez tu servidor está recibiendo un ataque masivo y el archivo de logs crece demasiado rápido, puedes volver a apagar el registro con:
```bash
sudo ufw logging off
```

---

### 🛡️ Tu perímetro exterior está sellado
Con las llaves SSH, Fail2Ban y el Rate Limiting de UFW, hemos fortificado al máximo las "murallas" exteriores de tu servidor. Es extremadamente difícil que alguien entre por la fuerza desde internet.

Pero, ¿qué pasa si el atacante no entra por la fuerza, sino que se cuela por una vulnerabilidad de tu página web (Nginx o PHP)? En el próximo (y último) tema de este módulo, aprenderemos a contener el daño en el interior usando **AppArmor**.

---
[<- Anterior: Defensa Activa (Fail2Ban)](../03-defensa-activa-fail2ban/README.md) | [Volver al Módulo 11](../README.md) | [Siguiente: Seguridad del Kernel (AppArmor) ->](../05-seguridad-del-kernel-apparmor/README.md)