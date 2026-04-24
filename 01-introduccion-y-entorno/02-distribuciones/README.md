# Tema 2: Distribuciones Linux (Distros)

Si buscas "descargar Linux" en internet, te vas a encontrar con un pequeño problema: no hay un solo botón de descarga oficial de "Linux". En su lugar, encontrarás cientos de versiones diferentes con nombres extraños como Ubuntu, Fedora, Mint o Arch. 

En este tema vamos a entender por qué ocurre esto y cómo orientarnos en este inmenso ecosistema.

## 🧩 ¿Qué es exactamente una Distribución?
Como vimos en el tema anterior, Linux es solo el "motor" (el Kernel). Para tener un coche funcional que puedas conducir, necesitas añadirle ruedas, asientos, un volante y pintura.

Una **Distribución** (o "Distro" de forma cariñosa) es el paquete completo. Es el trabajo de una organización, empresa o comunidad de usuarios que se encarga de juntar:
1. El **Kernel** de Linux.
2. Las **herramientas** del sistema (generalmente del proyecto GNU).
3. Un **Entorno de Escritorio** (la interfaz gráfica, las ventanas, los iconos).
4. Un **Gestor de Paquetes** (el programa que instala y actualiza otras aplicaciones).
5. Un conjunto de **aplicaciones preinstaladas** (navegador web, suite ofimática, reproductor de música).

Cada grupo elige estas piezas según su visión y las empaqueta listas para que tú las instales. Por eso hay distros enfocadas en la seguridad, otras en la facilidad de uso para novatos, otras para servidores y otras para revivir ordenadores viejos.

## 🌳 Las tres grandes "familias" de Linux
Aunque existen cientos de distribuciones, la gran mayoría son "hijas" o derivan de tres grandes ramas principales. Conocer a la familia te ayuda a saber cómo funciona el sistema por debajo (sobre todo a la hora de instalar programas).

### 1. La Familia Debian 🔴
Es una de las ramas más antiguas, estables y populares. Su sistema para instalar programas usa comandos como `apt`.
* **Debian:** La madre de la familia. Extremadamente estable, pero puede requerir algo más de conocimiento para dejarla a punto.
* **Ubuntu:** Basada en Debian, creada por la empresa Canonical. Revolucionó Linux haciéndolo fácil para el usuario común. Es el estándar de la industria.
* **Linux Mint:** Basada en Ubuntu. Modificada para que la transición desde Windows sea lo más amigable, cómoda e intuitiva posible.

### 2. La Familia Red Hat 🔵
Enfocada históricamente en el mundo empresarial, servidores y nuevas tecnologías. Utilizan el gestor de programas `dnf` (o el clásico `yum`).
* **RHEL (Red Hat Enterprise Linux):** De pago y orientada a grandes servidores y empresas.
* **Fedora:** La versión comunitaria patrocinada por Red Hat. Trae siempre las últimas novedades tecnológicas antes que nadie. Ideal para desarrolladores.
* **Rocky Linux / AlmaLinux:** Clones gratuitos de RHEL, ideales para aprender a montar servidores empresariales sin pagar licencia.

### 3. La Familia Arch 🟣
Diseñada para usuarios avanzados que quieren control absoluto. Su gestor de programas es `pacman`.
* **Arch Linux:** Es un sistema "hazlo tú mismo". La instalación base te deja en una pantalla negra y tú debes construir el sistema pieza a pieza.
* **Manjaro:** Toma la base de Arch, pero le añade un instalador gráfico y lo configura por ti para que sea fácil de usar desde el minuto uno.

## 🎯 ¿Cuál elegir para este curso (y para empezar)?
Si es tu primera vez, la regla de oro es: **elige una distribución popular y amigable**. Al ser populares, si tienes un problema, buscar en Google te dará la solución en segundos porque miles de personas ya lo han resuelto.

Para seguir este curso sin frustraciones, te recomiendo encarecidamente que uses una de estas dos:
1. **Ubuntu:** Porque es el estándar. Casi cualquier tutorial en internet asume que usas Ubuntu.
2. **Linux Mint:** Porque su interfaz es muy similar a Windows y consume muy pocos recursos.

Durante el resto del curso, los comandos y ejemplos estarán enfocados principalmente en la familia Debian/Ubuntu, ya que es la puerta de entrada más lógica y demandada en el mundo laboral para principiantes.

---
[<- Anterior: ¿Qué es Linux?](../01-que-es-linux/README.md) | [Volver al Módulo 1](../README.md) | [Siguiente: Entornos de Escritorio ->](../03-entornos-de-escritorio/README.md)