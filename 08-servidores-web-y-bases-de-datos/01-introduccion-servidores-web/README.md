# Tema 1: Introducción a los Servidores Web (Apache vs Nginx)

Hasta ahora has sido un "cliente". Abres tu navegador, escribes `google.com` y esperas a que la página aparezca. En este módulo, vas a pasar al otro lado del mostrador: tú serás el que entregue las páginas a los clientes.

Para hacer esto, necesitamos un software específico llamado **Servidor Web**.



## 🌐 1. ¿Qué es exactamente un servidor web?
Un servidor web no es más que un programa que se ejecuta en tu máquina Linux en segundo plano (un servicio). Su trabajo es muy simple pero vital:
1.  Se queda "escuchando" permanentemente en el **Puerto 80** (para tráfico HTTP normal) y en el **Puerto 443** (para tráfico cifrado HTTPS).
2.  Cuando alguien teclea tu IP o tu dominio web en su navegador, el servidor web recibe esa "petición".
3.  Busca en el disco duro de tu Linux el archivo solicitado (como `index.html` o una imagen).
4.  Se lo envía de vuelta al navegador del usuario.

Existen muchos programas que hacen esto, pero la historia de internet está dominada por dos gigantes: **Apache** y **Nginx**.

## 🦖 2. Apache (El veterano)
Nacido en 1995, Apache es el servidor web responsable del crecimiento inicial de internet. Es la "A" del famoso stack **LAMP** (Linux, Apache, MySQL, PHP).

* **¿Cómo funciona?** Cada vez que un usuario pide una página web, Apache crea un nuevo "proceso" o "hilo" en el procesador para atender a esa persona de forma exclusiva.
* **Ventajas:** Es increíblemente flexible y compatible con casi todo. Permite a los programadores cambiar la configuración del servidor usando un simple archivo llamado `.htaccess`.
* **Desventajas:** Si tu web se hace viral y entran 10.000 personas de golpe, Apache intentará crear 10.000 procesos. Esto puede devorar toda la memoria RAM de tu servidor y hacer que se caiga.

## 🚀 3. Nginx (El velocista moderno)
Nginx (se pronuncia *"Engine-X"*) nació en 2004 precisamente para solucionar el problema de memoria de Apache. Es la "E" del stack **LEMP**.

* **¿Cómo funciona?** Nginx está basado en "eventos". En lugar de crear un proceso para cada usuario, usa un solo proceso maestro que puede atender miles de peticiones simultáneamente a una velocidad vertiginosa.
* **Ventajas:** Es el rey indiscutible sirviendo archivos estáticos (imágenes, CSS, HTML). Consume una cantidad minúscula de RAM incluso bajo ataques masivos de tráfico.
* **Desventajas:** Su configuración es un poco más estricta y no lee archivos `.htaccess`, por lo que el administrador (tú) tiene el control absoluto.

## 🏆 4. ¿Por qué elegimos Nginx para este curso?
Hoy en día, **Nginx es el servidor web más utilizado en el mundo** para los sitios web de alto tráfico (Netflix, GitHub o WordPress.com lo usan). 

Aprender Nginx te da una ventaja competitiva enorme en el mercado laboral actual. Además, te enseñará a configurar servicios directamente desde los archivos centrales del sistema, lo cual es una habilidad imprescindible para un buen SysAdmin.

---

### 🧪 Mini reto práctico
Antes de instalar nada en el próximo tema, vamos a usar las herramientas de auditoría que aprendimos en el Módulo 7 para asegurarnos de que nuestro Puerto 80 está libre y esperando a Nginx.

1.  Abre tu terminal.
2.  Ejecuta el comando para ver los puertos que están escuchando:
    ```bash
    ss -tuln
    ```
3.  Busca en la columna `Local Address:Port`. ¿Ves algún `:80` o `:443`? 
    * Si **no** lo ves, ¡perfecto! Tu máquina está limpia y lista.
    * Si **sí** lo ves, significa que ya tienes algún servidor web instalado (quizás Apache se instaló por defecto en tu sistema). Si es así, puedes detenerlo temporalmente con `sudo systemctl stop apache2`.

---
[<- Volver al Módulo 8](../README.md) | [Siguiente: Instalación y configuración de Nginx ->](../02-instalacion-y-configuracion-nginx/README.md)