# Tema 4: Dominando `journalctl` (La lupa moderna)

En el tema anterior vimos cómo leer archivos de texto plano dentro de `/var/log`. Pero, ¿recuerdas `systemd`? Ese gran "jefe" que aprendimos en el Módulo 7 y que se encarga de encender, apagar y vigilar todos los servicios del sistema (Nginx, Docker, SSH...).

Pues bien, `systemd` tiene su propio diario privado llamado **`journald`**. A diferencia de los logs tradicionales de texto, `journald` guarda los registros en un formato **binario**. Esto significa que no puedes abrir su base de datos con `nano` o `less`. Para leerla, necesitas usar su traductor oficial: el comando **`journalctl`**.

## 🚀 1. El poder de la centralización
Si ejecutas `journalctl` sin ningún argumento, te mostrará *absolutamente todo* lo que ha pasado en el sistema desde el primer día. Literalmente millones de líneas. 
```bash
journalctl
```
*(Puedes moverte con las flechas, buscar con `/` y salir con la letra `q`, ¡igual que en `less`!)*

El verdadero superpoder de `journalctl` no es mostrarlo todo, sino su capacidad de **filtrar la información** con una precisión quirúrgica.

## 🎯 2. Filtrando por Servicio (`-u`)
Imagina que Nginx se ha caído. No te importa lo que esté haciendo Docker o SSH; solo quieres ver los logs de Nginx. Usamos la bandera `-u` (Unit):
```bash
sudo journalctl -u nginx
```
Esto te mostrará única y exclusivamente el historial de vida del servicio web Nginx. Si quieres ver lo que está pasando con Docker:
```bash
sudo journalctl -u docker
```

## ⏱️ 3. Viajando en el tiempo (`--since` y `--until`)
Un cliente te llama y te dice: *"Oye, la web dio un error gravísimo ayer entre las 14:00 y las 14:15"*.

Con los logs tradicionales de `/var/log` tendrías que buscar a ojo o usar `grep` complejos. Con `journalctl`, es tan fácil como pedirle un viaje en el tiempo:
```bash
sudo journalctl -u nginx --since "2023-10-25 14:00:00" --until "2023-10-25 14:15:00"
```

También entiende lenguaje natural (en inglés). Puedes pedirle que te muestre los eventos de la última hora:
```bash
sudo journalctl --since "1 hour ago"
```
O simplemente lo que ha pasado hoy desde que empezó el día:
```bash
sudo journalctl --since "today"
```

## 🚨 4. Filtrando por gravedad (`-p`)
Los servicios hablan mucho. Dicen cosas como *"Me he encendido"*, *"He recibido una visita"*, *"Sigo vivo"*. Esto es información inútil cuando estás apagando un incendio.

Podemos decirle a `journalctl` que omita la charla y nos muestre **solo los errores graves**. Para ello usamos la bandera `-p` (Priority) seguida del nivel `err` (Error):

```bash
sudo journalctl -p err
```
O combinándolo con un servicio específico:
```bash
sudo journalctl -u nginx -p err
```
*(Los niveles de prioridad de Linux van del 0 al 7. Los más comunes son: `emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`).*

## 👁️ 5. El modo Vigilante (`-f` y `-n`)
Al igual que aprendimos a usar `tail -f` para los archivos de texto, `journalctl` tiene exactamente las mismas banderas para monitorizar en tiempo real.

Para ver las últimas 20 líneas de Docker y quedarte vigilando en directo:
```bash
sudo journalctl -u docker -n 20 -f
```
*(Recuerda: pulsa `Ctrl+C` para salir del modo vigilancia).*

## 🧹 6. Limpiando el diario
Como `journald` lo guarda todo, su base de datos binaria puede crecer hasta ocupar varios Gigabytes en servidores antiguos. Como buen SysAdmin, puedes ordenarle que haga limpieza de todo lo que tenga más de 2 semanas de antigüedad:
```bash
sudo journalctl --vacuum-time=2weeks
```
O puedes decirle que reduzca su tamaño hasta ocupar un máximo de 100 Megabytes:
```bash
sudo journalctl --vacuum-size=100M
```

---
[<- Anterior: El sistema de logs (/var/log)](../03-el-sistema-de-logs-var-log/README.md) | [Volver al Módulo 10](../README.md) | [Siguiente: Observabilidad moderna (Prometheus y Grafana) ->](../05-observabilidad-prometheus-y-grafana/README.md)