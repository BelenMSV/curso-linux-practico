# Módulo 11: Seguridad Avanzada y Hardening (Blindando el Servidor)

Bienvenido a la trinchera. En el momento en que conectas un servidor a internet, empieza a recibir ataques. Literalmente en cuestión de minutos, *bots* automatizados de todo el mundo empezarán a escanear tus puertos y a probar contraseñas al azar intentando entrar. 

En el mundo de la Administración de Sistemas, a la práctica de asegurar un sistema operativo reduciendo su superficie de ataque se le llama **Hardening** (Fortificación). En este módulo, vamos a convertir tu servidor Linux en una auténtica fortaleza.

## 📝 Descripción del Módulo
Aprenderemos a auditar nuestro sistema buscando puntos débiles, cambiaremos la forma en la que nos conectamos para hacer imposible el robo de contraseñas, e instalaremos sistemas de defensa activa que banearán automáticamente a los atacantes en tiempo real.

* ⏱️ **Duración estimada del módulo:** 4.5 horas.

## 📚 Temas del Módulo
1. **01-auditoria-y-hardening-basico**: La regla del menor privilegio. Cómo buscar usuarios huérfanos, permisos peligrosos y aplicar el sentido común antes de instalar herramientas complejas.
2. **02-fortificando-ssh-llaves-criptograficas**: El fin de las contraseñas. Generación de pares de llaves (Ed25519/RSA), deshabilitar el acceso al usuario `root` y bloquear los inicios de sesión tradicionales.
3. **03-defensa-activa-fail2ban**: Tu perro guardián. Instalación y configuración de un sistema de prevención de intrusos (IPS) que lee los logs en tiempo real y bloquea IPs maliciosas en el firewall automáticamente.
4. **04-firewall-avanzado-y-limites**: Más allá de abrir y cerrar puertos. Aprenderemos a configurar reglas de *rate limiting* (límites de conexión) en UFW para mitigar ataques de denegación de servicio (DDoS) básicos.
5. **05-seguridad-del-kernel-apparmor**: Introducción al Control de Acceso Obligatorio (MAC). ¿Qué pasa si un hacker logra entrar a través de una vulnerabilidad en Nginx? AppArmor lo encerrará en una jaula para que no pueda tocar el resto del sistema.

## 🎯 Resultado Esperado
Al terminar este módulo, tu servidor podrá sobrevivir en internet de forma autónoma. Entenderás que la seguridad no es un programa que se instala, sino **una mentalidad de capas (Defensa en Profundidad)**. Tu sistema estará protegido contra ataques de fuerza bruta, escaneos masivos y vulnerabilidades comunes de configuración.

---
[<- Volver al Roadmap del Bootcamp](../README.md)