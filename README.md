📈 Google Cloud Monitoring — Lab

Documentación técnica de un laboratorio práctico de supervisión de infraestructura en Google Cloud Platform, con configuración de métricas, alertas, grupos de recursos y comprobaciones de disponibilidad sobre un clúster de VMs con Nginx.

📌 Resumen Ejecutivo

En este laboratorio se configuró un entorno de supervisión para recursos en Google Cloud Platform (GCP). Se desplegaron instancias de máquinas virtuales (VM), se instaló un servicio web Nginx, y se configuraron métricas, alertas, grupos de recursos y comprobaciones de disponibilidad (Uptime Checks) para monitorear la salud e infraestructura del sistema.

🎯 Objetivos Alcanzados
Exploración de Cloud Monitoring: configuración de paneles (dashboards) y visualización de métricas.
Alertamiento automático: creación de políticas de alertas para métricas críticas (uso de CPU superior al 20%).
Grupos de recursos: agrupación lógica de instancias para monitoreo conjunto.
Comprobación de disponibilidad (Uptime Check): configuración de peticiones HTTP automatizadas para validar el estado del servicio web.
Resolución de incidentes: identificación y solución de errores de conexión (Connection Error - Refused) mediante la instalación y activación de Nginx.
🛠️ Arquitectura y Componentes
Componente	Detalle
Servidores	3 instancias de Compute Engine (nginxstack-1, nginxstack-2, nginxstack-3)
Servicio web	Nginx HTTP Server (puerto 80)
Métrica monitoreada	VM Instance – CPU utilization
Herramientas de GCP	Compute Engine, Cloud Monitoring (Alerting, Dashboards, Uptime Checks)
📋 Guía Paso a Paso
1. Configuración de la política de alerta
Se accedió a Monitoring → Alerting → Create Policy.
Métrica seleccionada: VM Instance > Instance > CPU utilization.

Condición de activación:

Parámetro	Valor
Position	Above threshold (por encima del umbral)
Threshold Value	20%
Rolling window / Period	1 min
2. Configuración de la comprobación de disponibilidad

Se configuró un Uptime Check de tipo HTTP hacia las instancias en el puerto 80.

Diagnóstico y solución de fallo:

La prueba inicial arrojó el error Connection Error - Refused.
Causa: las instancias VM no tenían un servidor web activo escuchando en el puerto 80.
Solución: se accedió por SSH a cada instancia (nginxstack-1, 2, y 3) y se ejecutó:
bash
sudo apt-get update && sudo apt-get install -y nginx

Tras la instalación, la comprobación devolvió un estado 200 OK (exitoso).

3. Limpieza de recursos

Para evitar cargos adicionales y mantener el entorno limpio:

Se desactivaron y eliminaron las políticas de alertas.
Se eliminaron las comprobaciones de disponibilidad y los grupos de recursos.
Se eliminaron las instancias de VM mediante Cloud Shell:
bash
gcloud compute instances delete nginxstack-1 nginxstack-2 nginxstack-3 --quiet
🎓 Conceptos Aprendidos
Configuración de políticas de alertamiento basadas en umbrales de métricas
Diagnóstico de fallos de conectividad a nivel de servicio (puerto/HTTP)
Uso de Uptime Checks como validación activa de disponibilidad
Buenas prácticas de limpieza de infraestructura multi-instancia
📌 Notas

Este laboratorio forma parte de mi preparación continua para la certificación Google Associate Cloud Engineer (ACE), con enfoque práctico en observabilidad y monitoreo de infraestructura en GCP.

⬆ Español version above

📈 Google Cloud Monitoring — Lab

Technical documentation of a hands-on infrastructure monitoring lab on Google Cloud Platform, covering metrics, alerting, resource grouping, and uptime checks across a cluster of Nginx-backed VMs.

📌 Executive Summary

In this lab, a monitoring environment was configured for Google Cloud Platform (GCP) resources. Compute Engine Virtual Machine (VM) instances were deployed, an Nginx web service was installed, and metrics, alerting policies, resource groups, and Uptime Checks were implemented to ensure infrastructure health and availability.

🎯 Accomplished Objectives
Cloud Monitoring exploration: configured dashboards and metric visualizations.
Automated alerting: created alert policies for critical metrics (CPU utilization exceeding 20%).
Resource grouping: grouped instances logically for unified monitoring.
Uptime Checks: configured automated HTTP probes to validate web service availability.
Troubleshooting & remediation: diagnosed and resolved connection errors (Connection Error - Refused) by installing and starting the Nginx web service.
🛠️ Architecture & Components
Component	Detail
Servers	3 Compute Engine instances (nginxstack-1, nginxstack-2, nginxstack-3)
Web service	Nginx HTTP Server (port 80)
Monitored metric	VM Instance – CPU utilization
GCP services used	Compute Engine, Cloud Monitoring (Alerting, Dashboards, Uptime Checks)
📋 Step-by-Step Execution Guide
1. Alert policy configuration
Navigated to Monitoring → Alerting → Create Policy.
Selected metric: VM Instance > Instance > CPU utilization.

Trigger condition:

Parameter	Value
Threshold position	Above threshold
Threshold value	20%
Rolling window	1 min
2. Uptime Check configuration

Configured an HTTP Uptime Check targeting the VM instances on port 80.

Troubleshooting:

Initial test returned Connection Error - Refused.
Root cause: VMs lacked an active web server listening on port 80.
Resolution: connected via SSH to each VM (nginxstack-1, 2, and 3) and executed:
bash
sudo apt-get update && sudo apt-get install -y nginx

After installation, re-testing returned a 200 OK status.

3. Resource Cleanup

To prevent unnecessary billing and maintain account cleanliness:

Disabled and removed alerting policies.
Deleted Uptime Checks and resource groups.
Terminated VM instances via Cloud Shell:
bash
gcloud compute instances delete nginxstack-1 nginxstack-2 nginxstack-3 --quiet
🎓 Key Concepts Learned
Configuring threshold-based alerting policies
Diagnosing service-level connectivity failures (port/HTTP)
Using Uptime Checks as active availability validation
Multi-instance infrastructure cleanup best practices
📌 Notes

This lab is part of my ongoing preparation for the Google Associate Cloud Engineer (ACE) certification, with a hands-on focus on observability and infrastructure monitoring in GCP.
