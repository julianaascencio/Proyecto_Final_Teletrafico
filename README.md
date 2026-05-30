# Proyecto Final - Conmutación y Teletráfico

## Del Switch Catalyst a la Orquestación con Kubernetes

---

## 1. Información General

**Asignatura:** Conmutación y Teletráfico
**Proyecto:** Proyecto Integrador - Del Switch Catalyst a la Orquestación con Kubernetes
**Estudiante:** Juliana Ascencio
**Entorno de trabajo:** Windows 11
**Memoria RAM:** 16 GB
**Herramientas principales:** Docker Desktop, Kubernetes, Helm, Agones, SuperTuxKart, Flask, Prometheus, Grafana, Wireshark y Kali Linux.

---

## 2. Descripción del Proyecto

Este proyecto tiene como finalidad implementar una arquitectura moderna de telecomunicaciones basada en contenedores, orquestación, monitoreo y análisis de tráfico de red.

La práctica integra diferentes tecnologías utilizadas actualmente en entornos empresariales y de alta disponibilidad, tales como Docker, Kubernetes, Agones, Prometheus, Grafana y Wireshark.

El proyecto se desarrolló tomando como referencia una arquitectura donde diferentes servicios son desplegados y administrados mediante contenedores y orquestación. Dentro de la solución se implementó un chatbot web, servidores de juego SuperTuxKart administrados por Agones, monitoreo con Prometheus y Grafana, además de captura de tráfico HTTP mediante Wireshark.

---

## 3. Objetivo General

Implementar una arquitectura funcional basada en Docker y Kubernetes que permita desplegar, monitorear y analizar servicios de red, integrando herramientas de orquestación, visualización de métricas, análisis de tráfico y administración de servidores de videojuegos.

---

## 4. Objetivos Específicos

* Implementar un entorno de contenedores mediante Docker Desktop.
* Crear y ejecutar un chatbot web desarrollado con Python y Flask.
* Dockerizar el chatbot mediante un archivo Dockerfile.
* Activar y validar Kubernetes en Docker Desktop.
* Instalar Helm como gestor de paquetes para Kubernetes.
* Instalar Agones como plataforma de administración de servidores de videojuegos.
* Desplegar una Fleet de servidores SuperTuxKart mediante Agones.
* Verificar GameServers en estado Ready.
* Capturar tráfico HTTP con Wireshark.
* Crear un endpoint de métricas en formato Prometheus.
* Implementar Prometheus para recolectar métricas del chatbot.
* Implementar Grafana para visualizar métricas en tiempo real.
* Documentar las fallas encontradas durante el desarrollo.
* Consolidar evidencias técnicas para la entrega final.

---

## 5. Arquitectura General del Proyecto

La arquitectura implementada se compone de los siguientes elementos:

```text
Usuario
   |
   v
Chatbot Web Flask
   |
   v
Docker Container
   |
   v
Prometheus
   |
   v
Grafana Dashboard


Kubernetes Cluster
   |
   v
Agones
   |
   v
Fleet SuperTuxKart
   |
   v
GameServers Ready


Wireshark
   |
   v
Captura y análisis de tráfico HTTP
```

La solución permite demostrar el funcionamiento de una infraestructura moderna donde los servicios se ejecutan en contenedores, se administran mediante Kubernetes, se monitorean con Prometheus y Grafana, y se validan mediante análisis de tráfico de red.

(Evidencia requerida: imagen o diagrama de la arquitectura general del proyecto. Guardar como `evidencias/arquitectura-general.png`)

---

## 6. Tecnologías Utilizadas

| Tecnología     | Función dentro del proyecto                  |
| -------------- | -------------------------------------------- |
| Docker Desktop | Creación y ejecución de contenedores         |
| Python Flask   | Desarrollo del chatbot web                   |
| Kubernetes     | Orquestación de servicios y contenedores     |
| Helm           | Instalación de Agones sobre Kubernetes       |
| Agones         | Administración de servidores de videojuegos  |
| SuperTuxKart   | Servidor de juego usado para simular tráfico |
| Prometheus     | Recolección de métricas del chatbot          |
| Grafana        | Visualización de métricas en dashboard       |
| Wireshark      | Captura y análisis de tráfico HTTP           |
| Kali Linux     | Contenedor de auditoría para pruebas de red  |

---

## 7. Estructura de Repositorio

```text
proyecto-final-conmutacion-teletrafico/
│
├── README.md
│
├── chatbot/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
│
├── prometheus/
│   └── prometheus.yml
│
├── evidencias/
│   ├── 01-docker-ps.png
│   ├── 02-chatbot-interfaz.png
│   ├── 03-chatbot-metrics.png
│   ├── 04-kubernetes-node-ready.png
│   ├── 05-agones-pods-running.png
│   ├── 06-fleet-supertuxkart.png
│   ├── 07-gameservers-ready.png
│   ├── 08-wireshark-http.png
│   ├── 09-prometheus-query.png
│   ├── 10-grafana-dashboard.png
│   ├── 11-kali-error-dns.png
│   └── 12-arquitectura-general.png
│
└── docs/
    └── informe-final.pdf
```

---

## 8. Desarrollo Paso a Paso

---

# Fase 1: Verificación de Docker Desktop

Inicialmente se validó que Docker Desktop estuviera instalado y funcionando correctamente sobre Windows 11.

Se ejecutaron los siguientes comandos:

```powershell
docker --version
```

```powershell
docker ps
```
<img width="439" height="331" alt="DOCKER PS" src="https://github.com/user-attachments/assets/43e97160-c327-4ce2-8cd9-1c50869eb17f" />

Con estos comandos se verificó que Docker estuviera instalado y que el motor de contenedores estuviera activo.

![Uploading DOCKER PS.png…]()


---

# Fase 2: Desarrollo del Chatbot en Flask

Se creó un chatbot web utilizando Python y Flask. El chatbot permite consultar conceptos relacionados con el proyecto, tales como Docker, Kubernetes, Agones, SuperTuxKart, Wireshark, Grafana, Parrot OS, Nmap, QoS, ACL y la arquitectura general.

El chatbot fue diseñado con una interfaz visual moderna, botones por tecnología, área de conversación, respuesta escrita y respuesta por voz mediante el navegador.

El archivo principal del chatbot es:

```text
chatbot/app.py
```

El chatbot cuenta con las siguientes rutas:

| Ruta           | Función                                   |
| -------------- | ----------------------------------------- |
| `/`            | Interfaz web del chatbot                  |
| `/chat?q=tema` | Devuelve respuesta JSON según la pregunta |
| `/metrics`     | Expone métricas en formato Prometheus     |

(Evidencia requerida: captura de la interfaz visual del chatbot en `http://localhost:5000`. Guardar como `evidencias/02-chatbot-interfaz.png`)

---

# Fase 3: Dockerización del Chatbot

Para ejecutar el chatbot en un contenedor, se creó un archivo `Dockerfile`.

Contenido del Dockerfile:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app.py .

CMD ["python", "app.py"]
```

También se creó el archivo `requirements.txt` con la dependencia principal:

```text
flask
```

Luego se construyó la imagen Docker:

```powershell
docker build -t chatbot-proyecto .
```

Después se ejecutó el contenedor:

```powershell
docker run -d -p 5000:5000 --name chatbot-proyecto chatbot-proyecto
```

Para verificar que el contenedor estuviera activo se utilizó:

```powershell
docker ps
```

El servicio quedó disponible en:

```text
http://localhost:5000
```

<img width="879" height="149" alt="image" src="https://github.com/user-attachments/assets/77668d01-39ce-400d-a0b2-df8c89acf74b" />


<img width="870" height="592" alt="image" src="https://github.com/user-attachments/assets/3f398301-942c-462c-8fbc-4cbbbb8cfbcb" />


---

# Fase 4: Prueba del Chatbot

Se probaron diferentes consultas desde el navegador, por ejemplo:

```text
http://localhost:5000/chat?q=que es kubernetes
```

Respuesta esperada:

```json
{
  "pregunta": "que es kubernetes",
  "respuesta": "Kubernetes orquesta contenedores, administra pods, servicios, despliegues y permite escalar aplicaciones dentro de un clúster."
}
```

Además, la interfaz visual permite hacer clic en botones como:

* Docker
* Kubernetes
* Agones
* SuperTuxKart
* Wireshark
* Grafana
* Parrot OS
* Nmap
* QoS
* ACL
* Proyecto

Cada consulta aumenta los contadores internos del chatbot.

<img width="626" height="502" alt="CHATBOT" src="https://github.com/user-attachments/assets/c02497b7-0536-4c03-91c7-4ae23c0bafee" />


---

# Fase 5: Creación del Endpoint de Métricas

Para integrar el chatbot con Prometheus y Grafana, se agregó la ruta:

```text
/metrics
```

Esta ruta expone métricas en formato compatible con Prometheus.

Ejemplo de métricas expuestas:

```text
chatbot_total_preguntas 13
chatbot_uptime_seconds 2100
proyecto_docker_status 1
proyecto_kubernetes_status 1
proyecto_agones_status 1
proyecto_gameservers_ready 2
proyecto_wireshark_status 1
proyecto_grafana_status 1
chatbot_preguntas_por_tema{tema="docker"} 2
chatbot_preguntas_por_tema{tema="kubernetes"} 3
```

Se verificó el endpoint en:

```text
http://localhost:5000/metrics
```

<img width="453" height="473" alt="METRICS" src="https://github.com/user-attachments/assets/a86ae57f-fee5-41a0-9fa2-4b8b2debf818" />


---

# Fase 6: Activación y Validación de Kubernetes

Se activó Kubernetes desde Docker Desktop y se verificó su funcionamiento mediante el comando:

```powershell
kubectl get nodes
```

Resultado esperado:

```text
NAME                    STATUS   ROLES           VERSION
desktop-control-plane   Ready    control-plane   v1.34.3
```

Esto confirmó que el clúster Kubernetes estaba activo y disponible para desplegar servicios.

<img width="443" height="43" alt="EVIDENCIA 1" src="https://github.com/user-attachments/assets/a9967b2c-90ec-4351-9906-506be58125b3" />


También se validaron los pods internos del sistema:

```powershell
kubectl get pods -A
```

<img width="458" height="301" alt="EVIDENCIA 2" src="https://github.com/user-attachments/assets/524cd611-8ece-4742-9de5-90458fa87d45" />


---

# Fase 7: Instalación de Helm

Helm fue instalado para permitir la instalación de Agones sobre Kubernetes.

Primero se validó si Helm estaba instalado:

```powershell
helm version
```

Inicialmente se presentó el siguiente error:

```text
helm : El término 'helm' no se reconoce como nombre de un cmdlet
```

Para solucionarlo se instaló Helm con:

```powershell
winget install Helm.Helm
```

Luego se cerró y abrió nuevamente PowerShell, y se verificó:

```powershell
helm version
```

Resultado esperado:

```text
version.BuildInfo{Version:"v4.2.0"...}
```

<img width="873" height="119" alt="image" src="https://github.com/user-attachments/assets/664b8a6f-1749-4f46-89fd-77aace8a9490" />


---

# Fase 8: Instalación de Agones

Agones fue instalado utilizando Helm.

Se agregó el repositorio:

```powershell
helm repo add agones https://agones.dev/chart/stable
```

Se actualizaron los repositorios:

```powershell
helm repo update
```

Se instaló Agones:

```powershell
helm install agones agones/agones --namespace agones-system --create-namespace
```

Luego se verificaron los pods:

```powershell
kubectl get pods -n agones-system
```

Resultado esperado:

```text
agones-allocator     1/1 Running
agones-controller    1/1 Running
agones-extensions    1/1 Running
agones-ping          1/1 Running
```

<img width="870" height="510" alt="image" src="https://github.com/user-attachments/assets/96103942-4d03-4c2a-82b0-6c57054037b2" />


---

# Fase 9: Despliegue de SuperTuxKart con Agones

Se desplegó una Fleet de servidores de juego SuperTuxKart usando el manifiesto oficial de Agones:

```powershell
kubectl apply -f https://raw.githubusercontent.com/googleforgames/agones/release-1.57.0/examples/supertuxkart/fleet.yaml
```

Resultado esperado:

```text
fleet.agones.dev/supertuxkart created
```

Se verificó la Fleet:

```powershell
kubectl get fleet
```

Resultado obtenido:

```text
NAME           SCHEDULING   DESIRED   CURRENT   ALLOCATED   READY
supertuxkart   Packed       2         2         0           2
```

<img width="451" height="75" alt="EVIDENCIA 3" src="https://github.com/user-attachments/assets/6046c596-9f7e-4d1a-8c2c-45847d1b6070" />


---

# Fase 10: Verificación de GameServers

Se verificaron los GameServers con:

```powershell
kubectl get gameservers
```

Resultado obtenido:

```text
NAME                       STATE   ADDRESS      PORT   NODE
supertuxkart-75jcx-65cq7   Ready   172.19.0.4   7886   desktop-control-plane
supertuxkart-75jcx-xhj77   Ready   172.19.0.4   7057   desktop-control-plane
```

Esto confirmó que los servidores de juego estaban activos y listos para recibir conexiones.

<img width="448" height="104" alt="EVIDENCIA 4" src="https://github.com/user-attachments/assets/eb372fbf-47df-42a6-8b3c-7a54e9154a89" />


---

# Fase 11: Captura de Tráfico con Wireshark

Se utilizó Wireshark para capturar tráfico HTTP generado por el chatbot.

Como el servicio estaba publicado en `localhost:5000`, se seleccionó la interfaz:

```text
Adapter for loopback traffic capture
```

Se aplicó el filtro:

```text
tcp.port == 5000
```

Se generó tráfico accediendo a:

```text
http://localhost:5000/chat?q=kubernetes
```

En Wireshark se observó la solicitud:

```text
GET /chat?q=kubernetes HTTP/1.1
```

Y la respuesta:

```text
HTTP/1.1 200 OK
```

Esto permitió validar la comunicación cliente-servidor entre el navegador y el chatbot Flask.

<img width="1906" height="949" alt="Captura de pantalla 2026-05-29 192408" src="https://github.com/user-attachments/assets/b613ea30-b33d-4d21-8a71-c82f4560aa83" />


---

# Fase 12: Implementación de Prometheus

Se creó una carpeta para Prometheus:

```powershell
mkdir C:\Users\juli\proyecto-final\prometheus
cd C:\Users\juli\proyecto-final\prometheus
```

Se creó el archivo:

```text
prometheus.yml
```

Contenido del archivo:

```yaml
global:
  scrape_interval: 5s

scrape_configs:
  - job_name: 'chatbot'
    static_configs:
      - targets: ['host.docker.internal:5000']
```

Luego se ejecutó Prometheus en Docker:

```powershell
docker run -d --name prometheus-proyecto -p 9090:9090 -v "C:\Users\juli\proyecto-final\prometheus\prometheus.yml:/etc/prometheus/prometheus.yml" prom/prometheus
```

Se verificó que el contenedor estuviera activo:

```powershell
docker ps
```

Prometheus quedó disponible en:

```text
http://localhost:9090
```

<img width="878" height="661" alt="Captura de pantalla 2026-05-30 101041" src="https://github.com/user-attachments/assets/d9fe3784-7d57-4989-93b2-554a6d0fa6c5" />


---

# Fase 13: Validación de Métricas en Prometheus

Dentro de Prometheus se ejecutó la consulta:

```promql
chatbot_total_preguntas
```

El resultado mostró el número total de preguntas realizadas al chatbot.

También se validaron métricas como:

```promql
chatbot_uptime_seconds
```

```promql
proyecto_gameservers_ready
```

```promql
proyecto_kubernetes_status
```

```promql
chatbot_preguntas_por_tema
```

<img width="1207" height="718" alt="Captura de pantalla 2026-05-30 101309" src="https://github.com/user-attachments/assets/644b001d-e1d3-47b4-90bd-291b20288b91" />

---

# Fase 14: Implementación de Grafana

Se creó un contenedor independiente para Grafana:

```powershell
docker run -d --name grafana-proyecto -p 3001:3000 grafana/grafana
```

Se accedió a Grafana mediante:

```text
http://localhost:3001
```

Credenciales iniciales:

```text
Usuario: admin
Contraseña: admin
```

Posteriormente se configuró una nueva contraseña para la práctica.

---

# Fase 15: Conexión de Grafana con Prometheus

En Grafana se agregó Prometheus como fuente de datos.

Ruta:

```text
Connections > Data sources > Add data source > Prometheus
```

URL configurada:

```text
http://host.docker.internal:9090
```

Se presionó:

```text
Save & Test
```

Resultado esperado:

```text
Successfully queried Prometheus
```

<img width="1527" height="295" alt="image" src="https://github.com/user-attachments/assets/5d5c970d-3fd8-4a1c-8d33-775d3fee94f6" />


---

# Fase 16: Dashboard de Monitoreo en Grafana

Se creó un dashboard llamado:

```text
PROYECTO FINAL
```

El dashboard integra métricas recolectadas desde Prometheus.

Paneles implementados:

| Panel                     | Consulta PromQL              | Visualización           |
| ------------------------- | ---------------------------- | ----------------------- |
| Preguntas realizadas      | `chatbot_total_preguntas`    | Stat                    |
| Tiempo activo del chatbot | `chatbot_uptime_seconds`     | Stat                    |
| Docker Status             | `proyecto_docker_status`     | Gauge                   |
| Kubernetes Status         | `proyecto_kubernetes_status` | Gauge                   |
| Agones Status             | `proyecto_agones_status`     | Gauge                   |
| GameServers Ready         | `proyecto_gameservers_ready` | Gauge                   |
| Consultas por tecnología  | `chatbot_preguntas_por_tema` | Bar Chart / Time Series |
| Docker Engine             | `proyecto_docker_status`     | Gauge                   |
| Servidores SuperTuxKart   | `proyecto_gameservers_ready` | Stat                    |
| Agones Controller         | `proyecto_agones_status`     | Stat                    |

<img width="959" height="503" alt="GRAFANA" src="https://github.com/user-attachments/assets/5edfa434-71aa-4022-87b3-1b13dc4c9da9" />


---

## 9. Consultas PromQL Utilizadas

### Total de preguntas al chatbot

```promql
chatbot_total_preguntas
```

### Tiempo activo del chatbot

```promql
chatbot_uptime_seconds
```

### Estado Docker

```promql
proyecto_docker_status
```

### Estado Kubernetes

```promql
proyecto_kubernetes_status
```

### Estado Agones

```promql
proyecto_agones_status
```

### GameServers activos

```promql
proyecto_gameservers_ready
```

### Preguntas por tema

```promql
chatbot_preguntas_por_tema
```

### Disponibilidad general

```promql
(proyecto_docker_status + proyecto_kubernetes_status + proyecto_agones_status) / 3 * 100
```

---

## 10. Fallas y Errores Encontrados Durante el Desarrollo

Durante el desarrollo del proyecto se presentaron varias fallas técnicas que fueron solucionadas progresivamente.

---

### Error 1: Kubernetes no tenía contexto configurado

Al ejecutar:

```powershell
kubectl get nodes
```

Se obtuvo inicialmente el error:

```text
Unable to connect to the server: dial tcp [::1]:8080
```

También se observó:

```powershell
kubectl config current-context
```

Resultado:

```text
error: current-context is not set
```

Causa:

Kubernetes estaba habilitado en Docker Desktop, pero el clúster no había sido creado.

Solución:

Se ingresó a Docker Desktop y se utilizó la opción:

```text
Create cluster
```

Posteriormente se verificó:

```powershell
kubectl get nodes
```

Resultado final:

```text
desktop-control-plane   Ready
```

---

### Error 2: Helm no estaba instalado

Al ejecutar:

```powershell
helm version
```

Se obtuvo:

```text
helm : El término 'helm' no se reconoce como nombre de un cmdlet
```

Solución:

Se instaló Helm con:

```powershell
winget install Helm.Helm
```

Luego se verificó:

```powershell
helm version
```

---

### Error 3: Dockerfile guardado como Dockerfile.txt

Durante la creación del chatbot, el archivo Dockerfile fue guardado por error como:

```text
Dockerfile.txt
```

Al ejecutar:

```powershell
docker build -t chatbot-proyecto .
```

Se obtuvo:

```text
failed to read dockerfile: open Dockerfile: no such file or directory
```

Solución:

Se renombró el archivo:

```powershell
ren Dockerfile.txt Dockerfile
```

Luego se reconstruyó correctamente la imagen.

---

### Error 4: Contenedor chatbot detenido

El contenedor del chatbot apareció en estado:

```text
Exited (255)
```

Se revisaron los logs:

```powershell
docker logs chatbot-proyecto
```

Los logs mostraron que el servicio sí había respondido correctamente:

```text
GET / HTTP/1.1 200
GET /chat?q=que es kubernetes HTTP/1.1 200
GET /chat?q=que es docker HTTP/1.1 200
GET /chat?q=que es agones HTTP/1.1 200
```

Solución:

Se reinició el contenedor:

```powershell
docker start chatbot-proyecto
```

Posteriormente se reconstruyó el contenedor con una versión mejorada del chatbot.

---

### Error 5: Wireshark no capturaba tráfico en WiFi

Inicialmente se intentó capturar tráfico en la interfaz WiFi, pero no aparecían paquetes relacionados con el chatbot.

Causa:

El chatbot estaba publicado en:

```text
localhost:5000
```

Por lo tanto, el tráfico no salía por la tarjeta WiFi, sino que circulaba por la interfaz de loopback.

Solución:

Se seleccionó en Wireshark la interfaz:

```text
Adapter for loopback traffic capture
```

Luego se aplicó el filtro:

```text
tcp.port == 5000
```

Resultado:

Se capturó exitosamente la solicitud HTTP:

```text
GET /chat?q=kubernetes
```

y la respuesta:

```text
HTTP/1.1 200 OK
```

---

### Error 6: Imagen Parrot OS no descargaba correctamente

Se intentó descargar Parrot OS con:

```powershell
docker pull parrotsec/security
```

El proceso quedó detenido en:

```text
Pulling fs layer
```

Solución aplicada:

Se utilizó como alternativa Kali Linux:

```powershell
docker pull kalilinux/kali-rolling
```

La imagen de Kali sí se descargó correctamente.

---

### Error 7: Kali Linux no podía instalar Nmap por problema DNS

Dentro del contenedor Kali se intentó instalar Nmap:

```bash
apt update
apt install -y nmap
```

Se presentó el error:

```text
Could not resolve
```

y también:

```text
Unable to fetch some archives
```

Causa:

El contenedor Kali presentó problemas de resolución DNS hacia los repositorios.

Resultado:

Nmap no pudo instalarse dentro del contenedor. Esta incidencia se documentó como hallazgo técnico dentro de la auditoría.

(Evidencia requerida: captura del error DNS en Kali. Guardar como `evidencias/11-kali-error-dns.png`)

---

### Error 8: Comando Docker con saltos de línea mal interpretados en PowerShell

Al ejecutar algunos comandos de Docker en varias líneas con `^`, PowerShell interpretó incorrectamente los saltos de línea, generando errores como:

```text
docker: invalid reference format
```

y:

```text
Falta una expresión después del operador unario '--'
```

Solución:

Se ejecutaron los comandos en una sola línea. Ejemplo:

```powershell
docker run -d --name grafana-proyecto -p 3001:3000 grafana/grafana
```

---

### Error 9: Prometheus no iniciaba por error en el comando Docker

Inicialmente se intentó ejecutar Prometheus con saltos de línea y se generó:

```text
docker: invalid reference format
```

Solución:

Se ejecutó el comando en una sola línea:

```powershell
docker run -d --name prometheus-proyecto -p 9090:9090 -v "C:\Users\juli\proyecto-final\prometheus\prometheus.yml:/etc/prometheus/prometheus.yml" prom/prometheus
```

Resultado:

Prometheus quedó disponible en:

```text
http://localhost:9090
```

---

### Error 10: Métricas del chatbot salían en una sola línea

En el endpoint:

```text
http://localhost:5000/metrics
```

las métricas `chatbot_preguntas_por_tema` aparecían pegadas por error de salto de línea.

Causa:

Se estaba usando:

```python
\\n
```

en lugar de:

```python
\n
```

Solución:

Se corrigió el código del endpoint `/metrics` para que cada métrica apareciera en una línea independiente.

Resultado:

Prometheus pudo leer correctamente las métricas del chatbot.

---

## 11. Evidencias Requeridas para el Informe

| Número | Evidencia                       | Comando o ubicación                   |
| ------ | ------------------------------- | ------------------------------------- |
| 1      | Docker ejecutando contenedores  | `docker ps`                           |
| 2      | Chatbot visual funcionando      | `http://localhost:5000`               |
| 3      | Métricas del chatbot            | `http://localhost:5000/metrics`       |
| 4      | Kubernetes Ready                | `kubectl get nodes`                   |
| 5      | Agones Running                  | `kubectl get pods -n agones-system`   |
| 6      | Fleet SuperTuxKart              | `kubectl get fleet`                   |
| 7      | GameServers Ready               | `kubectl get gameservers`             |
| 8      | Wireshark HTTP                  | filtro `tcp.port == 5000`             |
| 9      | Prometheus consultando métricas | `http://localhost:9090`               |
| 10     | Grafana Dashboard               | `http://localhost:3001`               |
| 11     | Error Kali DNS                  | captura del error `Could not resolve` |
| 12     | Arquitectura general            | diagrama del proyecto                 |

---

## 12. Resultados Obtenidos

Se logró implementar una arquitectura funcional compuesta por:

* Un chatbot web desarrollado en Flask.
* Un contenedor Docker para el chatbot.
* Un clúster Kubernetes funcional en Docker Desktop.
* Agones instalado mediante Helm.
* Una Fleet de servidores SuperTuxKart.
* Dos GameServers en estado Ready.
* Captura de tráfico HTTP mediante Wireshark.
* Endpoint de métricas en formato Prometheus.
* Prometheus recolectando métricas del chatbot.
* Grafana visualizando métricas en tiempo real.
* Paneles dinámicos para estado de Docker, Kubernetes, Agones y GameServers.
* Gráfico de consultas por tecnología realizadas al chatbot.

---

## 13. Análisis Técnico

La solución implementada demuestra cómo una arquitectura basada en contenedores puede facilitar el despliegue y administración de servicios.

Docker permitió encapsular el chatbot y ejecutarlo de forma aislada. Kubernetes permitió crear un entorno de orquestación para desplegar servicios más complejos. Agones extendió las capacidades de Kubernetes para administrar servidores de videojuegos, permitiendo crear GameServers de SuperTuxKart.

Prometheus permitió recolectar métricas reales desde el chatbot mediante el endpoint `/metrics`, mientras que Grafana permitió visualizar estas métricas de forma clara mediante paneles dinámicos.

Wireshark permitió validar a nivel de red que el chatbot recibía solicitudes HTTP y respondía correctamente con código `200 OK`.

Aunque no se logró completar la instalación de Nmap dentro del contenedor Kali por problemas de DNS, el error fue documentado como parte del análisis técnico del proyecto.

---

## 14. Conclusiones

1. Docker permitió desplegar el chatbot de forma portable, aislada y reproducible, facilitando la ejecución del servicio sin depender directamente del sistema operativo anfitrión.

2. Kubernetes permitió implementar una arquitectura de orquestación real, donde se pudo validar el estado del nodo, los pods del sistema y los recursos desplegados.

3. Helm simplificó la instalación de Agones, evitando una configuración manual compleja de manifiestos Kubernetes.

4. Agones permitió desplegar servidores de juego SuperTuxKart mediante una Fleet, demostrando cómo Kubernetes puede extenderse para administrar cargas especializadas como videojuegos multijugador.

5. Los GameServers en estado Ready evidencian que la arquitectura de Agones funcionó correctamente y que los servidores fueron creados exitosamente.

6. El chatbot cumplió una doble función: por un lado, sirvió como aplicación web dockerizada; por otro, funcionó como fuente de métricas para Prometheus y Grafana.

7. La implementación del endpoint `/metrics` permitió convertir el chatbot en una aplicación monitoreable, generando información real como total de preguntas, tiempo activo, estado de componentes y consultas por tema.

8. Prometheus permitió recolectar métricas automáticamente, evitando que el dashboard dependiera únicamente de datos manuales o simulados.

9. Grafana permitió construir un tablero visual profesional, con indicadores de estado, medidores, contadores y gráficos dinámicos.

10. Wireshark permitió validar el tráfico HTTP generado por el chatbot, demostrando la comunicación cliente-servidor mediante paquetes TCP y respuestas HTTP exitosas.

11. El problema de DNS presentado en Kali Linux demuestra la importancia de validar conectividad, resolución de nombres y acceso a repositorios cuando se trabaja con contenedores de auditoría.

12. El proyecto permitió integrar conceptos de redes, contenedores, orquestación, monitoreo, análisis de tráfico y servicios distribuidos en una sola arquitectura funcional.

13. La práctica permitió comprender que una infraestructura moderna no solo debe desplegar servicios, sino también permitir su monitoreo, análisis y diagnóstico ante fallas.

14. La arquitectura implementada se acerca a un entorno real de DevOps y telecomunicaciones, donde los servicios son desplegados, monitoreados y validados mediante herramientas especializadas.

---

## 15. Recomendaciones

* Integrar Prometheus directamente con Kubernetes para recolectar métricas reales de pods, nodos y recursos del clúster.
* Implementar Node Exporter o cAdvisor para monitorear CPU, memoria y red.
* Corregir el problema DNS del contenedor Kali para instalar Nmap correctamente.
* Implementar un dashboard adicional con métricas específicas de Kubernetes.
* Probar conexión real al servidor SuperTuxKart desde el cliente del juego.
* Agregar un diagrama visual de arquitectura en el repositorio.
* Exportar el dashboard de Grafana en formato JSON para respaldo.
* Documentar todas las evidencias con capturas numeradas.

---

## 16. Comandos Principales Utilizados

### Docker

```powershell
docker --version
docker ps
docker build -t chatbot-proyecto .
docker run -d -p 5000:5000 --name chatbot-proyecto chatbot-proyecto
docker logs chatbot-proyecto
docker rm -f chatbot-proyecto
```

### Kubernetes

```powershell
kubectl get nodes
kubectl get pods -A
kubectl get fleet
kubectl get gameservers
kubectl get pods -n agones-system
```

### Helm

```powershell
helm version
helm repo add agones https://agones.dev/chart/stable
helm repo update
helm install agones agones/agones --namespace agones-system --create-namespace
```

### Agones / SuperTuxKart

```powershell
kubectl apply -f https://raw.githubusercontent.com/googleforgames/agones/release-1.57.0/examples/supertuxkart/fleet.yaml
kubectl get fleet
kubectl get gameservers
```

### Prometheus

```powershell
docker run -d --name prometheus-proyecto -p 9090:9090 -v "C:\Users\juli\proyecto-final\prometheus\prometheus.yml:/etc/prometheus/prometheus.yml" prom/prometheus
```

### Grafana

```powershell
docker run -d --name grafana-proyecto -p 3001:3000 grafana/grafana
```

### Wireshark

```text
Interfaz: Adapter for loopback traffic capture
Filtro: tcp.port == 5000
Solicitud: GET /chat?q=kubernetes
Respuesta: HTTP/1.1 200 OK
```

---

## 17. Estado Final del Proyecto

| Componente                  | Estado                      |
| --------------------------- | --------------------------- |
| Docker Desktop              | Implementado                |
| Chatbot Flask               | Implementado                |
| Interfaz visual del chatbot | Implementada                |
| Endpoint `/metrics`         | Implementado                |
| Kubernetes                  | Implementado                |
| Helm                        | Implementado                |
| Agones                      | Implementado                |
| SuperTuxKart Fleet          | Implementada                |
| GameServers                 | Implementados               |
| Wireshark                   | Implementado                |
| Prometheus                  | Implementado                |
| Grafana                     | Implementado                |
| Kali Linux                  | Parcial                     |
| Nmap                        | No completado por error DNS |
| QoS / ACL                   | Documentado conceptualmente |

---

## 18. Referencias

* Docker: https://www.docker.com/
* Kubernetes: https://kubernetes.io/
* Agones: https://agones.dev/
* SuperTuxKart: https://supertuxkart.net/
* Prometheus: https://prometheus.io/
* Grafana: https://grafana.com/
* Wireshark: https://www.wireshark.org/
* Flask: https://flask.palletsprojects.com/
* Kali Linux: https://www.kali.org/

---

## 19. Anexos

En la carpeta `evidencias/` se deben almacenar las capturas correspondientes al desarrollo del proyecto.

Cada imagen debe nombrarse de forma clara y organizada para facilitar su revisión.

Ejemplo:

```text
evidencias/01-docker-ps.png
evidencias/02-chatbot-interfaz.png
evidencias/03-chatbot-metrics.png
evidencias/04-kubernetes-node-ready.png
evidencias/05-agones-pods-running.png
evidencias/06-fleet-supertuxkart.png
evidencias/07-gameservers-ready.png
evidencias/08-wireshark-http.png
evidencias/09-prometheus-query.png
evidencias/10-grafana-dashboard.png
evidencias/11-kali-error-dns.png
evidencias/12-arquitectura-general.png
```
