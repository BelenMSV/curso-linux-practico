# Módulo 5: Usuarios y Permisos (La Matriz de Seguridad)

En los sistemas operativos domésticos, solemos tener un único usuario que puede hacer y deshacer a su antojo. Si descargas un virus, el virus tiene el mismo poder que tú para destruir el sistema. **Linux no funciona así.** Linux nació en las universidades para ser usado por cientos de personas a la vez en la misma máquina. Por ello, su sistema de seguridad, basado en usuarios y permisos, es uno de los más robustos del mundo.

## 📝 Descripción del Módulo
En este bloque descubrirás por qué la mayor parte del tiempo eres un "invitado" en tu propio sistema. Aprenderás a gestionar quién entra en el equipo, a qué grupos pertenecen y, lo más importante, cómo leer y modificar los permisos de los archivos para asegurar que nadie toque lo que no debe.

* ⏱️ **Duración estimada del módulo:** 4 horas.

## 📚 Temas del Módulo
1. **01-el-usuario-root-y-sudo**: Entendiendo la jerarquía de poder. Quién es el superusuario y por qué usamos `sudo` en lugar de iniciar sesión como él.
2. **02-gestion-de-usuarios**: Cómo crear, modificar y eliminar cuentas de usuario desde la terminal (`adduser`, `deluser`, `passwd`).
3. **03-gestion-de-grupos**: Organizando a los usuarios por roles o departamentos (`groupadd`, `usermod`).
4. **04-la-matriz-de-permisos**: Comprendiendo la salida de `ls -l`. Qué significan las letras `rwx` (Lectura, Escritura, Ejecución) y cómo se aplican al dueño, al grupo y a los demás.
5. **05-modificando-permisos-y-propietarios**: Toma el control de la seguridad. Uso de `chmod` (en modo simbólico y numérico) y `chown` para cambiar dueños.
6. **06-practica-carpeta-compartida**: Un reto integrador donde crearemos usuarios y configuraremos una carpeta en la que solo un grupo específico pueda leer y escribir.

## 🎯 Resultado Esperado
Al finalizar este módulo, entenderás exactamente por qué ocurre un error de "Permiso denegado" (Access Denied). Sabrás cómo crear cuentas para otros usuarios (o para aplicaciones/servicios) y serás capaz de bloquear un archivo para que sea completamente invisible o inmodificable para el resto de la red.

---
[<- Volver al inicio](../README.md)