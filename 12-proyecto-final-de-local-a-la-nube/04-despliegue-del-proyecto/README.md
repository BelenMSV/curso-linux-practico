# Tema 4: Despliegue del Proyecto (Tu código en la nube)

Existen muchas formas de subir un proyecto a un servidor. En el pasado, los administradores usaban programas como FileZilla (FTP) para arrastrar archivos uno a uno. Hoy en día, usamos métodos mucho más rápidos y profesionales.

En este tema, vamos a desplegar una página web profesional utilizando Nginx y el nombre de dominio que configuraste en el Tema 2.

## 📦 1. Llevando tu código al servidor

Tienes dos opciones principales para introducir archivos en tu VPS:

### Opción A: Usar Git (La vía profesional)
Si tu código está en un repositorio de GitHub, la mejor forma de descargarlo en tu servidor es simplemente clonarlo.
```bash
sudo apt install git -y
git clone [https://github.com/TU_USUARIO/tu-proyecto.com.git](https://github.com/TU_USUARIO/tu-proyecto.com.git)
```

### Opción B: Copia segura con SCP (La vía directa)
Si tienes los archivos en una carpeta de tu ordenador personal y no quieres usar GitHub, puedes enviarlos directamente a través del túnel seguro de SSH usando el comando `scp` (Secure Copy). 
*Abre una terminal en **tu PC local** y ejecuta:*
```bash
scp -r /ruta/a/tu/carpeta_web usuario@IP_DE_TU_VPS:/home/usuario/
```

---
*(Para este simulacro, si no tienes una web preparada, vamos a crear una carpeta de prueba directamente en el servidor en el siguiente paso).*

## 🏗️ 2. Preparando el terreno (El enfoque clásico)

Vamos a usar Nginx para servir nuestra página web, aplicando lo que aprendimos en el Módulo 8 sobre *Virtual Hosts* (Server Blocks).

**1. Instala Nginx:**
```bash
sudo apt update
sudo apt install nginx -y
```

**2. Crea la carpeta para tu dominio:**
Sustituye `tu-dominio.com` por el nombre real de tu dominio.
```bash
sudo mkdir -p /var/www/[tu-dominio.com/html](https://tu-dominio.com/html)
```

**3. Dale los permisos correctos:**
Para que Nginx pueda leer los archivos, el usuario `www-data` (el trabajador de Nginx) o tu propio usuario debe tener permisos.
```bash
sudo chown -R $USER:$USER /var/www/[tu-dominio.com/html](https://tu-dominio.com/html)
sudo chmod -R 755 /var/www/tu-dominio.com
```

**4. Crea un archivo `index.html` de prueba:**
```bash
nano /var/www/[tu-dominio.com/html/index.html](https://tu-dominio.com/html/index.html)
```
Pega este código HTML básico para celebrar tu victoria:
```html
<!DOCTYPE html>
<html>
<head>
    <title>¡Misión Cumplida!</title>
    <style>
        body { font-family: Arial; text-align: center; margin-top: 20%; background-color: #1a1a1a; color: white; }
        h1 { color: #00ffcc; }
    </style>
</head>
<body>
    <h1>🚀 ¡Servidor en Producción!</h1>
    <p>Este es el proyecto final del Bootcamp de Linux Práctico.</p>
    <p>Administrado por un futuro SysAdmin/DevOps.</p>
</body>
</html>
```
*(Guarda con Ctrl+O, Enter, y sal con Ctrl+X).*

## 🚦 3. Configurando el Virtual Host de Nginx

Ahora tenemos que decirle a Nginx: *"Oye, cuando alguien llegue a este servidor preguntando por `tu-dominio.com`, muéstrale la carpeta que acabamos de crear"*.

**1. Crea el archivo de configuración:**
```bash
sudo nano /etc/nginx/sites-available/tu-dominio.com
```

**2. Pega este bloque de servidor:**
*(⚠️ ¡Importante! Cambia `tu-dominio.com` por tu dominio real en la línea `server_name` y en la ruta de `root`).*
```nginx
server {
    listen 80;
    listen [::]:80;

    root /var/www/[tu-dominio.com/html](https://tu-dominio.com/html);
    index index.html index.htm index.nginx-debian.html;

    server_name tu-dominio.com [www.tu-dominio.com](https://www.tu-dominio.com);

    location / {
        try_files $uri $uri/ =404;
    }
}
```

**3. Activa la configuración creando un enlace simbólico:**
```bash
sudo ln -s /etc/nginx/sites-available/tu-dominio.com /etc/nginx/sites-enabled/
```

**4. Comprueba que no hay errores de sintaxis:**
```bash
sudo nginx -t
```
*(Debería responderte `syntax is ok` y `test is successful`).*

**5. Reinicia Nginx para aplicar los cambios:**
```bash
sudo systemctl restart nginx
```

## 🌍 4. ¡Prueba tu dominio en el navegador!

Abre tu navegador web favorito (Chrome, Firefox, Safari) y escribe tu dominio:
`http://tu-dominio.com`

Si la propagación DNS del Tema 2 ya ha terminado, **¡verás tu página web en vivo para todo el planeta!** 

---

### 🚨 Un último problema
Si te fijas en la barra de direcciones de tu navegador, verás un mensaje feo y preocupante que dice **"No seguro"**. 

Esto significa que el tráfico entre tu servidor y los usuarios viaja en texto plano (HTTP). En el mundo moderno, esto es inaceptable. En el siguiente (y absolutamente último) tema del Bootcamp, vamos a instalar un **Certificado SSL gratuito con Let's Encrypt** para ponerle el candado verde a tu dominio.

---
[<- Anterior: Checklist de Producción](../03-checklist-de-produccion/README.md) | [Volver al Módulo 12](../README.md) | [Siguiente: HTTPS y Certificados SSL ->](../05-https-y-certificados-ssl-reales/README.md)