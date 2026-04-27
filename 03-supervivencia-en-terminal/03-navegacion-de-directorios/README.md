# Tema 3: Navegación de Directorios (El mapa del tesoro)

En el entorno gráfico, hacer doble clic en una carpeta es muy fácil. En la terminal, como no vemos los iconos, necesitamos una forma de saber **dónde estamos**, **qué hay a nuestro alrededor** y **cómo movernos**.

Para eso, Linux nos da tres comandos fundamentales y un concepto clave: las rutas.

## 📍 1. ¿Dónde estoy? (`pwd`)
Cuando abres la terminal, a veces el *prompt* solo te muestra una `~` (tu carpeta personal), pero no la ruta completa. Si en algún momento te sientes perdido dentro del sistema de archivos, solo tienes que escribir:

```bash
pwd
```
*(Proviene del inglés "Print Working Directory" o Imprimir Directorio de Trabajo).*

El sistema te devolverá tu ubicación exacta, por ejemplo: `/home/tu_usuario/Descargas/musica`.

## 👁️ 2. ¿Qué hay aquí? (`ls`)
Ahora que sabes dónde estás, necesitas "ver" qué archivos y carpetas tienes a tu alrededor. Para eso usamos el comando de listar:

```bash
ls
```
*(Proviene de "List").*

Si lo escribes solo, te mostrará los nombres de los archivos. Pero el verdadero poder de `ls` viene cuando usamos sus "modificadores" o "banderas" (opciones que le pasamos al comando usando un guion):

* `ls -l`: Muestra una lista detallada (tamaño, fecha de creación, permisos).
* `ls -a`: Muestra los **archivos ocultos**. (En Linux, cualquier archivo o carpeta que empiece por un punto, como `.config`, está oculto por defecto).
* `ls -la`: **El combo definitivo.** Te muestra todo, en formato de lista, incluyendo los ocultos. ¡Acostúmbrate a usar este!

## 🚶‍♂️ 3. Moviéndonos de carpeta (`cd`)
Ya sabes dónde estás y qué hay. Ahora vamos a movernos. Para entrar o salir de carpetas usamos:

```bash
cd nombre_de_la_carpeta
```
*(Proviene de "Change Directory").*

**Atajos vitales para moverse:**
* `cd ..` (con dos puntos): Te saca de la carpeta actual y te lleva un nivel hacia atrás (a la carpeta "padre").
* `cd ~` (o simplemente escribir `cd` y pulsar Enter): Es un botón de pánico. Estés donde estés, te teletransportará de vuelta a tu carpeta personal (`/home/tu_usuario`).
* `cd -` (con un guion): Te lleva a la última carpeta en la que estuviste (como el botón "Atrás" del navegador).

## 🗺️ El Gran Secreto: Rutas Absolutas vs. Relativas
Este es el concepto en el que todo el mundo tropieza la primera vez. Cuando usas comandos como `cd` o `ls`, puedes decirle a Linux a dónde ir usando dos tipos de direcciones:

### Rutas Absolutas (La dirección postal completa)
* **Siempre empiezan con la barra `/` (la Raíz).**
* Es como dar una dirección completa: "País, Ciudad, Calle, Número".
* Funcionan sin importar en qué parte del ordenador estés.
* *Ejemplo:* Si estás en `/var/log` y quieres ir a tus documentos, puedes escribir la ruta absoluta completa: `cd /home/tu_usuario/Documentos`

### Rutas Relativas (Indicaciones de giro a giro)
* **Nunca empiezan con `/`.**
* Es como decir: "Gira a la derecha en la próxima esquina". Las indicaciones dependen totalmente de **dónde estés parado ahora mismo**.
* *Ejemplo:* Si ya estás dentro de `/home/tu_usuario` y haces un `ls` y ves que existe la carpeta `Documentos`, no necesitas escribir toda la ruta. Solo escribes la ruta relativa: `cd Documentos`

> ❌ **El error de novato más común:** Estar dentro de tu carpeta personal y escribir `cd /Documentos`. Linux buscará una carpeta llamada "Documentos" colgada directamente de la raíz del disco duro, no la encontrará y te dará error. Lo correcto es `cd Documentos` (ruta relativa).

---
### 🧪 Mini reto práctico
Abre tu terminal y realiza esta secuencia sin usar el ratón:
1. Asegúrate de estar en tu casa tecleando: `cd`
2. Ve qué hay a tu alrededor (incluyendo lo oculto): `ls -la`
3. Entra en la carpeta de descargas: `cd Descargas` (¡Recuerda usar la tecla TAB para autocompletar!)
4. Comprueba tu ubicación exacta: `pwd`
5. Vuelve un paso hacia atrás: `cd ..`

---
[<- Anterior: Atajos y Autocompletado](../02-atajos-y-autocompletado/README.md) | [Volver al Módulo 3](../README.md) | [Siguiente: Gestión de Archivos ->](../04-gestion-de-archivos/README.md)