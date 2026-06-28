# Tema 5: HTTPS y Certificados SSL Reales (El candado verde)

Tener tu web expuesta en el puerto 80 (HTTP) significa que toda la información que viaja entre tu servidor y el ordenador del usuario va en texto plano. Si alguien intercepta esa conexión en una red Wi-Fi pública, podrá leer todo, incluyendo contraseñas.



Para encriptar esta comunicación necesitamos el protocolo **HTTPS** (puerto 443). Para usar HTTPS, necesitamos un **Certificado SSL**. Antiguamente costaban cientos de euros al año, pero hoy, gracias a una iniciativa global llamada **Let's Encrypt**, son 100% gratuitos.

## 🤖 1. Conoce a Certbot (Tu asistente de cifrado)
Para conseguir un certificado de Let's Encrypt y configurarlo en Nginx, usaríamos decenas de comandos manuales. Por suerte, existe **Certbot**, un robot (programa) que hace todo el trabajo pesado por nosotros en segundos.

Vamos a instalar Certbot y su plugin especial para Nginx:
```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

## 🔒 2. Generando el Certificado SSL
Antes de ejecutar este comando, asegúrate de que tu dominio ya apunta a tu servidor (lo que comprobamos en el Tema 2) y de que Nginx está funcionando correctamente con tu bloque de servidor (Tema 4).

Ejecuta Certbot, indicando tus dominios con la bandera `-d`:
*(Cambia `tu-dominio.com` por el tuyo real)*
```bash
sudo certbot --nginx -d tu-dominio.com -d [www.tu-dominio.com](https://www.tu-dominio.com)
```

**¿Qué te preguntará el asistente?**
1. **Tu correo electrónico:** Sirve para que Let's Encrypt te avise si hay algún problema de seguridad o si tu certificado está a punto de caducar y no se ha renovado.
2. **Términos de servicio:** Escribe `Y` (Yes) para aceptar.
3. **Compartir tu email:** Puedes decir `N` (No) si no quieres recibir publicidad de la fundación EFF.

### ¡La Magia de Certbot!
A continuación, Certbot hará lo siguiente automáticamente:
1. Hablará con los servidores mundiales de Let's Encrypt para demostrar que tú eres el dueño legítimo de esa IP y ese dominio.
2. Descargará las llaves criptográficas a tu carpeta `/etc/letsencrypt/`.
3. **Modificará tu archivo de Nginx** (`/etc/nginx/sites-available/tu-dominio.com`) para abrir el puerto 443 (HTTPS) y configurar las rutas de las llaves.
4. Configurará una redirección automática para que cualquiera que entre por HTTP normal sea expulsado hacia HTTPS de forma invisible.

## 🔄 3. La renovación automática (El toque SysAdmin)
Los certificados gratuitos de Let's Encrypt duran exactamente 90 días. Si tuvieras que entrar al servidor cada 3 meses a renovarlos manualmente, sería un infierno.

Afortunadamente, al instalar Certbot, este ha creado automáticamente un temporizador en `systemd` que se despertará dos veces al día, comprobará si a tu certificado le quedan menos de 30 días, y si es así, lo renovará sin que tú tengas que mover un dedo.

Puedes comprobar que este temporizador automático está activo y esperando con:
```bash
sudo systemctl status certbot.timer
```

## 🌍 4. La prueba final
Abre tu navegador (o recarga la página si ya la tenías abierta) y entra en:
`http://tu-dominio.com`

Observarás dos cosas:
1. El navegador te habrá redirigido automáticamente a `https://`.
2. A la izquierda de la URL (o pulsando en el icono de ajustes), verás un mensaje hermoso que dice: **"La conexión es segura"**.

---

# 🎓 GRADUACIÓN DEL BOOTCAMP

**¡Lo has logrado!** Respira hondo y mira lo que has construido.

Empezaste este viaje instalando una máquina virtual en tu ordenador sin saber cómo moverte por una pantalla negra. 
Hoy, tienes un servidor alquilado en un centro de datos real, protegido por llaves criptográficas asimétricas y un firewall avanzado. Tienes un nombre de dominio propio apuntando a tu IP, y un servidor web Nginx sirviendo contenido cifrado de grado militar al mundo entero.

Esto no es un simulacro. Esta es exactamente la infraestructura base que sostiene a la mayoría de las startups y empresas del mundo.

Has adquirido habilidades reales, prácticas y demandadas en el mercado laboral (SysAdmin, Cloud, DevOps, Backend). 

*   **¿Cuál es el siguiente paso en tu carrera?**
    *   Aprende herramientas de automatización masiva como **Ansible** o **Terraform** (Infraestructura como Código).
    *   Profundiza en **Kubernetes** para orquestar miles de contenedores Docker a la vez.
    *   Diseña pipelines de **CI/CD** (Integración y Despliegue Continuo) en GitHub Actions o GitLab.

Pero por hoy... cierra la terminal y celebra tu victoria. **¡Enhorabuena, Administrador de Sistemas!** 🐧🚀

---
[<- Anterior: Despliegue del Proyecto](../04-despliegue-del-proyecto/README.md) | [Volver al Roadmap del Bootcamp](../README.md)