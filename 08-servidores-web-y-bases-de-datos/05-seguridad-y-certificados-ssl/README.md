# Tema 5: Seguridad y Certificados SSL (El candado seguro)

Seguramente te has fijado en que la mayoría de las páginas web modernas tienen un pequeño icono de un candado en la barra de direcciones del navegador y su dirección empieza por **HTTPS** en lugar de HTTP. 

La "S" significa *Secure* (Seguro). Para conseguir esa letra extra, nuestro servidor necesita un **Certificado SSL/TLS**.



## 🔓 1. HTTP vs HTTPS (El cartero espía)
* **HTTP (Puerto 80):** Es como enviar una postal. Cualquiera que participe en el transporte (tu router, tu proveedor de internet, un hacker en una cafetería) puede leer exactamente lo que pone.
* **HTTPS (Puerto 443):** Es como enviar una caja fuerte de titanio. Tú le das la caja al cartero y el servidor tiene la única llave para abrirla. Si alguien roba la caja por el camino, solo verá ruido matemático indescifrable.

## 🌍 2. El Mundo Real: Let's Encrypt y Certbot
En un entorno de producción real (cuando alquilas un servidor en la nube y compras un dominio web como `miempresa.com`), obtener un certificado es gratis y automático gracias a una fundación llamada **Let's Encrypt**.

La herramienta que hace la magia se llama `certbot`. Si tuvieras un dominio real configurado, cifrar tu web sería tan absurdamente fácil como ejecutar esto:
```bash
# ¡NO LO EJECUTES EN TU MÁQUINA VIRTUAL!
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d miempresa.com
```

## 🛠️ 3. El Mundo Local: Certificados Autofirmados
**El problema:** Como ahora mismo estás en tu propia máquina virtual local (con una IP como `192.168.x.x` y sin un dominio real), Let's Encrypt no puede verificar quién eres, por lo que no te dará un certificado oficial.

**La solución para practicar:** Vamos a ser nuestro propio emisor de certificados. Crearemos un **Certificado Autofirmado**. No servirá para el público general (el navegador se quejará), pero cifrará la información perfectamente y nos enseñará cómo se configura Nginx para el puerto 443.

## 🔑 4. Creando nuestro propio Certificado (OpenSSL)
Linux trae instalada una herramienta criptográfica todoterreno llamada `openssl`. Vamos a generar una llave privada y un certificado válido por un año (365 días):

1. Abre tu terminal y ejecuta este largo comando (puedes copiarlo y pegarlo):
   ```bash
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt
   ```
2. Te hará varias preguntas (País, Ciudad, Organización...). **Puedes pulsar Enter en todas para dejarlas en blanco**, excepto en una:
3. Cuando llegues a **`Common Name (e.g. server FQDN or YOUR name)`**, escribe la IP de tu máquina (ej. `192.168.1.50`) y pulsa Enter.

## ⚙️ 5. Enseñando el Certificado a Nginx
Ahora tenemos que decirle a Nginx que empiece a escuchar en el puerto seguro (443) y dónde están las llaves que acabamos de crear.

1. Abre la configuración de tu sitio web:
   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```
2. Baja hasta encontrar la línea `server_name _;`. **Justo debajo**, añade estas líneas para configurar el SSL:
   ```nginx
   listen 443 ssl;
   ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
   ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
   ```
3. Guarda (Ctrl+O, Enter) y cierra (Ctrl+X).
4. Comprueba que no hay errores de sintaxis:
   ```bash
   sudo nginx -t
   ```
5. Recarga el servidor:
   ```bash
   sudo systemctl reload nginx
   ```

---

### 🧪 Mini reto práctico: Afrontando la advertencia
Vamos a probar tu nuevo búnker criptográfico.

1. Abre tu navegador web.
2. Esta vez, **tienes que escribir explícitamente `https://`** antes de tu IP:
   ```text
   https://TU_DIRECCION_IP
   ```
3. **¡ALERTA ROJA!** Verás una pantalla de advertencia gigante diciendo *"Tu conexión no es privada"* o *"Riesgo potencial de seguridad"*. 
   * **¿Por qué pasa esto?** Porque el navegador no reconoce quién emitió el certificado (¡fuiste tú mismo!). En el mundo real, Let's Encrypt está en la lista blanca de tu navegador, pero tú no.
4. **Ignora la advertencia:** Haz clic en "Configuración avanzada" (o "Avanzado") y luego en **"Aceptar el riesgo y continuar"** (o "Continuar a 192.168.x.x").
5. ¡Bienvenido a tu web! Si te fijas en la barra de direcciones, verás un candado (quizás tachado o con una advertencia). Si haces clic en él y vas a los detalles del certificado, verás que todo el tráfico entre tu ordenador y tu máquina virtual ahora está 100% cifrado con tecnología RSA 2048.

---
[<- Anterior: El Stack LEMP y PHP](../04-el-stack-lemp/README.md) | [Volver al Módulo 8](../README.md) | [Siguiente: Proyecto Final - Despliegue ->](../06-proyecto-final-despliegue/README.md)