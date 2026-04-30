# Módulo 10: Monitorización, Logs y Troubleshooting (Los ojos del SysAdmin)

Bienvenido a la realidad de la infraestructura tecnológica: **las cosas se rompen.** 

Un servidor web se cae por un pico de tráfico, una base de datos se corrompe porque el disco duro se ha llenado al 100%, o un contenedor de Docker se reinicia en bucle y no sabes por qué. 

La diferencia entre un novato que entra en pánico y un profesional de Sistemas, es que el profesional no adivina; **el profesional lee el sistema**. En este módulo aprenderás a ser el "médico forense" y el "vigilante de seguridad" de tus servidores.

## 📝 Descripción del Módulo
Pasaremos de la monitorización clásica a la observabilidad moderna. Aprenderás a tomar las constantes vitales del servidor con herramientas de terminal, a bucear en los registros del sistema para encontrar errores ocultos, y a desplegar un panel de control profesional (Grafana) para visualizar métricas en tiempo real. Finalmente, haremos ingeniería inversa: romperemos nuestros propios servicios a propósito para aprender a diagnosticarlos y arreglarlos bajo presión.

* ⏱️ **Duración estimada del módulo:** 6 horas.

## 📚 Temas del Módulo
1. **01-monitorizacion-de-recursos**: Toma de constantes vitales. Uso avanzado de `top`, `htop`, `df` y `du` para controlar CPU, RAM y almacenamiento en tiempo real.
2. **02-gestion-de-memoria-y-swap**: ¿Qué pasa cuando te quedas sin RAM? Conceptos de paginación, creación y gestión de archivos Swap de emergencia.
3. **03-el-sistema-de-logs-var-log**: El historial del servidor. Exploración de `/var/log`, `syslog`, `auth.log` y los logs específicos de Nginx y MariaDB.
4. **04-dominando-journalctl**: La lupa moderna. Cómo filtrar, buscar por fechas y encontrar errores críticos en los servicios gestionados por `systemd`.
5. **05-observabilidad-prometheus-y-grafana**: El estándar de la industria. Despliegue rápido de un panel de métricas visuales utilizando Docker Compose.
6. **06-troubleshooting-practico**: El simulacro (Live Fire Drill). Romperemos nuestra base de datos y nuestro servidor web a propósito, analizaremos los síntomas y aplicaremos la cura.

## 🎯 Resultado Esperado
Al terminar este módulo, perderás el miedo a las pantallas de error y a las caídas del sistema. Sabrás cómo prever problemas antes de que ocurran (monitorización), cómo encontrar la aguja en el pajar cuando algo falla (logs), y tendrás tu propio panel de control visual al nivel de las grandes empresas tecnológicas.

---
[<- Volver al Roadmap del Bootcamp](../README.md)