# Tema 5: Observabilidad moderna (Prometheus y Grafana)

Leer logs y usar `htop` está muy bien cuando ya sabes que hay un problema. Pero la **observabilidad** va un paso más allá: consiste en recopilar métricas constantemente para poder ver tendencias a lo largo del tiempo, crear gráficas y configurar alertas automáticas antes de que el servidor explote.

Para lograr esto, vamos a usar el "Stack" líder de la industria, aprovechando todo lo que aprendimos en el Módulo de Docker.

## 🏛️ 1. La Santísima Trinidad de las Métricas



Nuestra infraestructura de vigilancia estará compuesta por 3 piezas clave que trabajarán en equipo:

1.  **Node Exporter (El Espía):** Es un pequeño programa que se instala en el servidor. Su única misión es recopilar información del sistema operativo (uso de CPU, RAM, red, temperatura) y exponerla en un puerto web.
2.  **Prometheus (El Recolector):** Es una base de datos temporal. Cada 15 segundos, Prometheus llama a la puerta de Node Exporter, recoge todas las métricas que tiene y las guarda en su disco duro.
3.  **Grafana (El Pintor):** Es un panel web de visualización. Se conecta a Prometheus, lee esos millones de datos incomprensibles y los transforma en gráficas espectaculares.

## 🚀 2. Despliegue con Docker Compose
En lugar de instalar esto a mano (lo cual llevaría horas), vamos a usar la magia de `docker-compose` para levantar toda la infraestructura en 3 minutos.

**Paso 1: Preparar el entorno**
Crea una carpeta en tu servidor para este proyecto:
```bash
cd ~
mkdir stack-monitorizacion
cd stack-monitorizacion
```

**Paso 2: Configurar Prometheus**
Prometheus necesita saber a quién tiene que vigilar. Crea un archivo de configuración llamado `prometheus.yml`:
```bash
nano prometheus.yml
```
Pega este contenido y guarda (Ctrl+O, Enter, Ctrl+X):
```yaml
global:
  scrape_interval: 15s # Recopilar datos cada 15 segundos

scrape_configs:
  - job_name: 'servidor_linux'
    static_configs:
      - targets: ['node-exporter:9100'] # El nombre del contenedor y su puerto
```

**Paso 3: El archivo Compose**
Ahora vamos a orquestar los 3 contenedores. Crea el archivo `docker-compose.yml`:
```bash
nano docker-compose.yml
```
Pega la receta de infraestructura:
```yaml
version: '3.8'

services:
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: always
    ports:
      - "9100:9100"

  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: always
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
```
Guarda y cierra.

**Paso 4: ¡Magia!**
Levanta la infraestructura en segundo plano:
```bash
docker compose up -d
```

## 🎨 3. Configurando tu Panel de Control (Dashboard)

¡Ya está funcionando! Ahora vamos a conectar las piezas desde el navegador.

1.  **Entra a Grafana:** Abre tu navegador y ve a `http://TU_IP:3000`.
2.  **Inicia sesión:** El usuario por defecto es `admin` y la contraseña es `admin` (te pedirá cambiarla en el primer inicio de sesión).
3.  **Conecta la base de datos (Prometheus):**
    *   Ve al menú izquierdo: `Connections` -> `Data sources`.
    *   Haz clic en `Add data source` y elige **Prometheus**.
    *   En la URL, escribe `http://prometheus:9090` (gracias a la red de Docker, Grafana puede hablar con Prometheus usando el nombre de su contenedor).
    *   Baja del todo y haz clic en `Save & test`. Si sale un tick verde, ¡están conectados!
4.  **Importa un Dashboard profesional:**
    *   La comunidad de Grafana ya ha creado paneles increíbles, no tienes que inventar la rueda.
    *   Ve al menú izquierdo (el signo de más `+` o `Dashboards`) y selecciona **Import**.
    *   Donde dice "Import via grafana.com", escribe el número **1860** (es el código del dashboard oficial y más famoso para Node Exporter) y pulsa "Load".
    *   Abajo del todo, selecciona "Prometheus" en el desplegable de base de datos y haz clic en "Import".

### 🏆 ¡Bienvenido al centro de mando!
De repente, verás decenas de gráficas en tiempo real de tu servidor: uso de CPU por núcleo, tráfico de red entrante/saliente, disco duro disponible, carga de memoria RAM... Todo con un diseño espectacular oscuro y profesional.

Acabas de desplegar la misma arquitectura de observabilidad que exigen las grandes empresas de tecnología en sus ofertas de empleo. 

---
[<- Anterior: Dominando journalctl](../04-dominando-journalctl/README.md) | [Volver al Módulo 10](../README.md) | [Siguiente: Troubleshooting Práctico (Simulacro) ->](../06-troubleshooting-practico/README.md)