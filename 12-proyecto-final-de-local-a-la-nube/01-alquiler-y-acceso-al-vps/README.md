# Tema 1: Alquiler y Acceso al VPS (El salto a la nube)

Hasta ahora, todo lo que has hecho vivía confinado en tu ordenador personal (localhost o una Máquina Virtual). Si apagabas tu PC, tu servidor moría. 

En el mundo real, necesitamos que nuestra infraestructura esté encendida 24/7, conectada a una red de altísima velocidad y con una IP pública estática. Para eso, alquilamos un **VPS (Virtual Private Server)**.



## ☁️ 1. ¿Qué es un VPS?
Imagina un ordenador físico gigantesco (un nodo) en un centro de datos de altísima seguridad. Ese ordenador tiene 128 núcleos de CPU y 1000 GB de RAM. Un proveedor Cloud coge esa máquina y la "corta" en trozos virtuales más pequeños. 

Un VPS es uno de esos trozos. Te alquilan una porción garantizada de esa máquina (ej: 1 CPU y 2 GB de RAM) para ti solo. Tienes acceso `root` absoluto; es exactamente igual que tu máquina virtual local, pero alojada profesionalmente.

## 🛒 2. Eligiendo a tu proveedor Cloud
No necesitas gastar una fortuna. Para un proyecto personal o un portfolio, un VPS de entre 4€ y 6€ al mes es más que suficiente. Aquí tienes los grandes jugadores:

*   **Hetzner (Recomendado 🏆):** Proveedor alemán. Tiene, de lejos, la mejor relación calidad-precio del mercado. Por menos de 5€ te dan servidores increíblemente potentes. Ideal para proyectos europeos.
*   **DigitalOcean / Linode (Akamai):** Los favoritos de los desarrolladores. Su interfaz es hermosísima y súper fácil de usar. Sus planes más baratos rondan los 5-6$.
*   **AWS (Amazon) / Google Cloud / Azure:** Los gigantes corporativos. Tienen "Capas Gratuitas" (Free Tiers) por un año, pero **¡cuidado!**. Su sistema de facturación es muy complejo y si te equivocas al configurar algo, puedes llevarte una sorpresa desagradable en la tarjeta de crédito. Para aprender, es mejor usar proveedores de tarifa plana como Hetzner o DigitalOcean.

## 🛠️ 3. Creando la instancia (La compra)
El proceso exacto varía según la web, pero en todos los proveedores tendrás que elegir 4 cosas fundamentales:

1.  **El Sistema Operativo (Imagen):** Elige siempre **Ubuntu 24.04 LTS** (o Debian 12 si lo prefieres). Es lo que hemos usado en el Bootcamp y te garantizas compatibilidad total.
2.  **El Tamaño (Plan):** Selecciona el más básico. 1 núcleo compartida (Shared CPU) y 1 GB o 2 GB de RAM es suficiente para empezar.
3.  **La Región (Datacenter):** ¿Dónde están tus clientes o lectores? Si estás en España, elige servidores en Madrid, París o Frankfurt. Si estás en Latinoamérica, elige servidores en Miami o Nueva York. Cuanto más cerca, menor latencia (menos tiempo de carga).
4.  **Autenticación (¡CRÍTICO!):** Aquí la plataforma te preguntará cómo quieres entrar. **NUNCA elijas contraseña**. Elige siempre **SSH Keys**. La web te dará la opción de pegar tu llave pública (el contenido del archivo `id_ed25519.pub` que generaste en el Módulo 11).

Haz clic en "Create" o "Deploy". En apenas 30 segundos, el proveedor arrancará tu servidor y te mostrará en pantalla una serie de números separados por puntos. **Esa es tu IP Pública**.

## 🚀 4. El Primer Contacto
¡Ya tienes servidor! Ahora vamos a entrar.

Abre la terminal de tu ordenador personal (Windows, macOS o Linux) y ejecuta el comando de conexión. (Nota: En DigitalOcean o Hetzner, el usuario por defecto suele ser `root`. En AWS suele ser `ubuntu`).

```bash
ssh root@IP_PUBLICA_DE_TU_NUEVO_VPS
```

Como es la primera vez en la historia que tu PC habla con ese servidor, la criptografía de SSH te lanzará una advertencia de seguridad (el *fingerprint*):
```text
The authenticity of host '198.51.100.45 (198.51.100.45)' can't be established.
ED25519 key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
Debes escribir la palabra **`yes`** completa y pulsar Enter. Esto le dice a tu ordenador: *"Sí, confío en este servidor, anótalo en tu libreta de direcciones conocidas"*.

### 🎉 ¡Bienvenido a Producción!
Si elegiste la opción de Llave SSH al crearlo, entrarás instantáneamente. Verás el mensaje de bienvenida de Ubuntu y un panel de terminal que dice `root@tu-servidor:~#`.

Estás dentro. Estás en la nube.

---

### ⚠️ Próximos pasos
Respira hondo y familiarízate con la terminal remota. Ejecuta un `htop` o un `df -h` para ver tu hardware nuevo. 

De momento, para acceder a la web que instalemos ahí, la gente tendría que memorizar tu IP Pública (ej. `http://198.51.100.45`), lo cual es horrible. En el próximo tema, vamos a solucionar eso **comprando un nombre de dominio**.

---
[<- Volver al Módulo 12](../README.md) | [Siguiente: Dominios y Registros DNS ->](../02-dominios-y-registros-dns/README.md)