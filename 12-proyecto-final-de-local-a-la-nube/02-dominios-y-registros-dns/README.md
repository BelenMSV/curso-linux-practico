# Tema 2: Dominios y Registros DNS (Tu identidad en internet)

Compartir tu proyecto diciendo *"Entra en http://198.51.100.45"* no es muy profesional. Hoy vamos a comprar un nombre propio (como `tu-proyecto.com`) y vamos a enseñarle a internet cómo conectar ese nombre con la IP pública del VPS que alquilamos en el tema anterior.

## 🛒 1. Comprando tu nombre (Los Registradores)
Nadie "compra" un dominio para siempre; en realidad se alquilan por años. Las empresas que gestionan esto se llaman **Registradores de Dominios**.

**¿Dónde comprarlo?**
Huye de empresas que te ofrezcan "el primer año a 1€" y luego te cobren 30€ por la renovación (ejem, GoDaddy). Aquí tienes las mejores opciones del mercado para SysAdmins:
*   **Porkbun:** Tienen los precios de renovación más honestos y baratos, además de una interfaz excelente.
*   **Namecheap:** Un clásico, muy fiables y económicos.
*   **Cloudflare:** Venden los dominios a precio de coste (sin margen de beneficio), pero necesitas tener un poco más de conocimientos técnicos para usarlos.

*Consejo:* Si un `.com` está pillado o es muy caro, los dominios `.dev`, `.tech` o `.io` son perfectos para portfolios tecnológicos.

## 📖 2. ¿Qué son los DNS? (La agenda telefónica)
El Sistema de Nombres de Dominio (DNS) es la agenda telefónica de internet. Cuando alguien escribe `tu-proyecto.com` en su navegador, su ordenador no sabe a dónde ir. Primero consulta a un servidor DNS para preguntarle: *"Oye, ¿qué número de IP tiene este nombre?"*.



Nuestro trabajo ahora es escribir nuestro "número de teléfono" (la IP del VPS) en esa agenda telefónica pública. A esto se le llama configurar la **Zona DNS**.

## 🛠️ 3. Configurando los Registros (A y CNAME)
Una vez hayas comprado tu dominio, ve al panel de control de tu registrador y busca una opción llamada **"DNS Management"** (Gestión de DNS), **"Advanced DNS"** o **"Zonas DNS"**.

Allí verás una tabla donde puedes añadir registros. Vamos a crear los dos más importantes:

### El Registro `A` (Address)
Este es el registro principal. Conecta directamente tu dominio raíz (sin las www) con la dirección IP de tu servidor (IPv4).
*   **Tipo (Type):** `A`
*   **Nombre/Host/Alias:** `@` *(La arroba significa "el dominio raíz", ej. tu-proyecto.com. Algunos paneles te piden que lo dejes en blanco).*
*   **Valor/Destino (Value):** `IP_DE_TU_VPS` (ej. 198.51.100.45)
*   **TTL:** Automático o el valor más bajo posible (ej. 5 min).

### El Registro `CNAME` (Canonical Name)
¿Qué pasa si alguien escribe `www.tu-proyecto.com`? Para no tener que repetir la IP otra vez, usamos un CNAME, que es simplemente un "alias" o redirección hacia otro nombre. Le decimos: *"Las www son exactamente lo mismo que el dominio principal"*.
*   **Tipo (Type):** `CNAME`
*   **Nombre/Host/Alias:** `www`
*   **Valor/Destino (Value):** `tu-proyecto.com` (Tu dominio base)
*   **TTL:** Automático.

*(Nota: Si en el futuro quieres añadir algo como `blog.tu-proyecto.com`, crearías otro Registro A donde el Nombre sea `blog` y el Valor sea la IP de tu servidor).*

## ⏳ 4. La Propagación (Paciencia)
¡Has guardado los cambios! Pero si intentas entrar a tu dominio en el navegador ahora mismo... probablemente dé error. 

¿Por qué? Porque internet es inmenso. El cambio que acabas de hacer en tu registrador tiene que copiarse (propagarse) por los servidores DNS de Telefónica, Vodafone, Google, etc., por todo el planeta. 

Esto se conoce como **Propagación DNS**.
*   Puede tardar desde **5 minutos hasta 24 horas**.
*   Para comprobar si el mundo ya conoce tu IP, puedes usar la herramienta web gratuita **[DNS Checker](https://dnschecker.org/)**. Escribe tu dominio, elige el registro "A" y verás un mapa mundial. Si ves cruces rojas, toca esperar. Si ves ticks verdes con la IP de tu servidor, ¡estás listo!

También puedes probarlo desde tu propia terminal local haciendo un ping a tu dominio:
```bash
ping tu-proyecto.com
```
Si el `ping` te responde con la IP de tu VPS, tu ordenador ya sabe el camino.

---

### 🛑 Siguiente parada: Seguridad
¡Perfecto! Ya tenemos un servidor encendido y un dominio apuntando hacia él. 

Pero antes de instalar nuestro código, Nginx o Docker... debemos recordar que este servidor está "desnudo" frente a internet. En el siguiente tema, ejecutaremos el **Checklist de Producción**, aplicando todo lo que aprendimos en el Módulo 11 para blindarlo antes de empezar a trabajar.

---
[<- Anterior: Alquiler y Acceso al VPS](../01-alquiler-y-acceso-al-vps/README.md) | [Volver al Módulo 12](../README.md) | [Siguiente: Checklist de Producción ->](../03-checklist-de-produccion/README.md)