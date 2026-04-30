# Tema 1: ¿Qué es Docker? (La revolución de los contenedores)

Seguro que alguna vez has escuchado la excusa más famosa en el mundo del desarrollo de software: *"Pues en mi ordenador funcionaba"*. 

Esto ocurre porque un programa no funciona solo; depende de la versión del sistema operativo, de librerías específicas, de configuraciones de red y de versiones concretas de bases de datos. Cuando pasas ese programa del ordenador del programador al servidor de producción, las cosas se rompen.

Para solucionar este caos, nació **Docker**.

## 🏗️ 1. Máquinas Virtuales vs Contenedores
Para entender Docker, primero debemos compararlo con lo que ya conoces: las Máquinas Virtuales (como el VirtualBox que usamos en este curso).



*   **Máquina Virtual (La forma antigua):** Si tienes un servidor físico y quieres correr tres aplicaciones aisladas, levantas tres máquinas virtuales. Cada máquina virtual necesita **su propio Sistema Operativo completo** (Guest OS), al que le tienes que asignar memoria RAM y disco duro de forma fija. Es pesado, lento de arrancar y desperdicia muchísimos recursos.
*   **Contenedor (La forma moderna):** Docker elimina el "Guest OS". Un contenedor solo incluye tu aplicación y las librerías exactas que necesita para funcionar. Todos los contenedores **comparten el núcleo (Kernel) del sistema operativo principal** (tu Linux). Son ligeros, arrancan en milisegundos y consumen solo los megabytes estrictamente necesarios.

## 📖 2. El Glosario de Docker (La Santísima Trinidad)
Para hablar "Docker", necesitas dominar estos tres conceptos básicos. Son el núcleo de todo lo que haremos en este módulo:

1.  **Imagen (Image):** Es la receta o el plano de construcción. Es un archivo inerte, de solo lectura, que contiene el código, las librerías y las instrucciones. (Ejemplo: Una imagen de *Ubuntu con Nginx instalado*).
2.  **Contenedor (Container):** Es la imagen "cobrando vida". Cuando le dices a Docker que ejecute una Imagen, se crea un Contenedor. Es la aplicación real funcionando. Puedes lanzar 100 contenedores idénticos a partir de una sola imagen.
3.  **Registro (Registry):** Es la biblioteca en internet donde se guardan las imágenes. El más famoso es **Docker Hub** (es como el GitHub de Docker). De ahí descargaremos imágenes oficiales de MariaDB, WordPress, Nginx, etc.

## 🚀 3. ¿Por qué el mundo entero usa Docker?
*   **Portabilidad absoluta:** Si un contenedor funciona en tu portátil, funcionará exactamente igual en un servidor de Amazon Web Services, en un entorno de pruebas o en el servidor de producción. Garantizado.
*   **Despliegues relámpago:** Como no hay que arrancar un sistema operativo entero, levantar un servidor web con Docker tarda, literalmente, menos de un segundo.
*   **Aislamiento:** Si un contenedor falla o es hackeado, los demás contenedores y el sistema principal siguen a salvo.

---

### 🧪 Mini reto práctico: El chequeo de compatibilidad
Como hemos visto, la magia de Docker radica en que sus contenedores se comunican directamente con el **Kernel de Linux**. Aunque existe Docker para Windows o macOS, en esos sistemas hace "trampa" (crea una pequeña máquina virtual oculta). 

La forma nativa, profesional y de máximo rendimiento para correr Docker es sobre Linux. Vamos a comprobar la versión de tu núcleo para asegurarnos de que tu máquina está lista.

1. Abre tu terminal.
2. Ejecuta el comando para ver la información de tu sistema operativo y tu Kernel:
   ```bash
   uname -r
   ```
3. Verás una salida parecida a `5.15.0-76-generic` (o un número superior). Este es el motor de tu sistema, el núcleo con el que Docker va a hablar directamente a partir de la próxima lección.

---
[<- Volver al Módulo 9](../README.md) | [Siguiente: Instalación de Docker ->](../02-instalacion-de-docker/README.md)