# 🐧 Linux Práctico: El Bootcamp Definitivo de Administración de Sistemas

Bienvenido al repositorio oficial de **Linux Práctico**. Este proyecto nace con el objetivo de ofrecer una guía paso a paso, estructurada y, sobre todo, práctica, para cualquier persona que quiera dominar el sistema operativo que mueve la infraestructura tecnológica del mundo.

Lo que empezó como un curso introductorio, ha evolucionado hasta convertirse en un **Bootcamp completo**. Aquí no solo encontrarás teoría; el entrenamiento está diseñado para que "aprendas haciendo", llevándote desde la creación de tu propio laboratorio virtual hasta el despliegue de servidores reales en la nube y la orquestación con contenedores.

---

## 🚀 Sobre este Bootcamp

Este programa está pensado para eliminar la barrera de entrada a Linux y formar perfiles preparados para el mundo laboral (SysAdmin, Junior DevOps o Backend Developer). A través de módulos progresivos y orientados a proyectos, dejarás de ser un simple usuario para convertirte en un administrador de sistemas.

### 📊 Detalles del programa
* **Dificultad:** Básico a Avanzado. Comenzamos desde cero absoluto.
* **Conocimientos previos:** No se requiere experiencia previa con Linux. Solo manejo básico de un ordenador (Windows o macOS), conexión a internet y ganas de aprender.
* **Tiempo total estimado:** ~55 horas (actualizado: **48.5 horas** de contenido ya disponible).

---

## 🗂️ Estructura del Bootcamp (Módulos)

El entrenamiento se divide en grandes bloques. Cada carpeta contiene su propio material y guías paso a paso.

### ✅ [Módulo 1: Introducción y Entorno](./01-introduccion-y-entorno/)
* **Descripción:** Fundamentos de Linux, historia, selección de distribuciones y preparación del entorno seguro con VirtualBox.
* **Estado:** Finalizado.
* **Duración estimada:** 3 horas.

### ✅ [Módulo 2: Instalación del Sistema](./02-instalacion-del-sistema/)
* **Descripción:** Proceso de instalación real, conceptos de particionado (Raíz, Home, Swap) y configuración post-instalación.
* **Estado:** Finalizado.
* **Duración estimada:** 4 horas.

### ✅ [Módulo 3: Supervivencia en la Terminal](./03-supervivencia-en-terminal/)
* **Descripción:** El corazón de Linux. Uso de la shell Bash, atajos de teclado, navegación por directorios, gestión de archivos y edición de texto con Nano.
* **Estado:** Finalizado.
* **Duración estimada:** 5 horas.

### ✅ [Módulo 4: Gestión de Paquetes y Software](./04-gestion-de-paquetes-y-software/)
* **Descripción:** Instalación de programas, uso de repositorios (`apt`), paquetes `.deb`, formatos universales (Snap, Flatpak, AppImage) y compilación básica.
* **Estado:** Finalizado.
* **Duración estimada:** 4.5 horas.

### ✅ [Módulo 5: Usuarios y Permisos](./05-usuarios-y-permisos/)
* **Descripción:** Seguridad del sistema, gestión de cuentas, grupos, matriz de permisos (rwx), comandos `chmod`/`chown` y uso de `sudo`.
* **Estado:** Finalizado.
* **Duración estimada:** 4 horas.

### ✅ [Módulo 6: Automatización y Bash Scripting](./06-automatizacion-y-bash-scripting/)
* **Descripción:** Creación de guiones (scripts) para automatizar tareas, uso de variables, operaciones, condicionales, bucles y funciones.
* **Estado:** Finalizado.
* **Duración estimada:** 5 horas.

### ✅ [Módulo 7: Redes y Servicios Básicos](./07-redes-y-servicios-basicos/)
* **Descripción:** Configuración de red, acceso remoto seguro con SSH, cortafuegos (UFW), escaneo de puertos y gestión de servicios con `systemd`.
* **Estado:** Finalizado.
* **Duración estimada:** 5 horas.

### ✅ [Módulo 8: Servidores Web y Bases de Datos](./08-servidores-web-y-bases-de-datos/)
* **Descripción:** Despliegue del Stack LEMP (Linux, Nginx, MariaDB, PHP). Configuración de Virtual Hosts y certificados SSL con Let's Encrypt.
* **Estado:** Finalizado.
* **Duración estimada:** 6 horas.

### ✅ [Módulo 9: Contenedores y Docker](./09-contenedores-y-docker/)
* **Descripción:** Introducción a la virtualización ligera. Uso de imágenes, contenedores, volúmenes, redes y orquestación con Docker Compose.
* **Estado:** Finalizado.
* **Duración estimada:** 6 horas.

### ✅ [Módulo 10: Monitorización, Logs y Troubleshooting](./10-monitorizacion-logs-y-troubleshooting/)
* **Descripción:** Diagnóstico avanzado. Gestión de Logs (`journalctl`), monitorización visual con Prometheus/Grafana y resolución de incidentes en vivo.
* **Estado:** Finalizado.
* **Duración estimada:** 6 horas.

### 🚧 Módulo 11: Seguridad Avanzada y Hardening
* **Descripción:** Auditoría de seguridad, protección de servidores expuestos a internet, Fail2ban y buenas prácticas para entornos productivos.
* **Estado:** Planificado (Siguiente paso).

### 🚧 Módulo 12: Proyecto Final (De Local a la Nube)
* **Descripción:** Alquiler de un VPS real, configuración de dominios y despliegue del proyecto final en internet.
* **Estado:** Planificado.

---

## 🛠️ ¿Cómo usar este repositorio?

Cada módulo está organizado de forma jerárquica para facilitar el aprendizaje autónomo:

1.  **Navegación:** Entra en la carpeta del módulo correspondiente (ej. `06-automatizacion-y-bash-scripting`).
2.  **Lectura:** Cada carpeta de módulo tiene su propio `README.md` que explica los objetivos y lista los temas.
3.  **Temas:** Dentro de cada módulo, los temas están numerados (ej. `01-mi-primer-script`). Entra en ellos y sigue el archivo `README.md` detallado.
4.  **Práctica:** No te limites a leer. Ten tu máquina virtual abierta y replica cada paso. **Linux se aprende escribiendo, no solo mirando.**

---
*Este proyecto es de código abierto y está vivo. Si encuentras algún error o quieres proponer una mejora, ¡los Pull Requests son bienvenidos!*