# Auditoría Forense: Detección de Rootkits y Análisis de Persistencia

## 🛡️ Descripción del Proyecto
Este repositorio documenta la metodología y ejecución de una auditoría técnica orientada al **Threat Hunting** (Caza de Amenazas) en sistemas Linux. El objetivo principal es la detección de **Rootkits**, puertas traseras (Backdoors) y mecanismos de persistencia que operan a nivel de Kernel o mediante la alteración de binarios esenciales.

## 🛠️ Stack Tecnológico
* **Herramienta de Auditoría:** Chkrootkit v0.58
* **Sistema Operativo:** Kali Linux
* **Áreas Auditadas:** * Integridad de comandos de administración (`ls`, `ps`, `netstat`, `login`).
    * Análisis de módulos cargables del Kernel (LKM).
    * Detección de interfaces en modo promiscuo (Sniffing).
    * Análisis de archivos ocultos en rutas de librerías.

## 📊 Hallazgos y Análisis Técnico

Durante la auditoría del **Día 15**, se identificaron diversos eventos que requirieron un análisis forense detallado para diferenciar entre actividad legítima y amenazas reales:

### 1. Detección de Procesos de Red (Sniffer Detection)
Se identificó una alerta de "Packet Sniffer" en la interfaz `eth0`.
* **Evidencia:** `eth0: PACKET SNIFFER(/usr/sbin/NetworkManager[686])`
* **Análisis:** Mediante el rastreo del PID 686, se confirmó que la actividad proviene del servicio **NetworkManager**. 
* **Estatus:** **Falso Positivo Validado.** Comportamiento normal del sistema operativo.

### 2. Auditoría de Archivos Ocultos (Aliens)
El escaneo reportó múltiples archivos sospechosos en `/usr/lib/`.
* **Evidencia:** Archivos ocultos en herramientas como `hashcat`, `gophish` y `llvm`.
* **Análisis:** Se verificó el origen de los archivos con los paquetes oficiales del repositorio. Se determinó que son componentes necesarios para el funcionamiento de herramientas de seguridad preinstaladas.
* **Estatus:** **Archivos Legítimos.**

## 📸 Evidencias de la Auditoría


*Figura 1: Verificación de interfaces y detección de actividad de red.*

*Figura 2: Auditoría de archivos sospechosos y validación de integridad en librerías.*

## 🏁 Conclusión
Tras el análisis exhaustivo, se certifica que el sistema se encuentra **libre de Rootkits conocidos** y no presenta signos de compromiso en sus binarios esenciales. Los hallazgos marcados como "Warning" han sido analizados y clasificados como actividad legítima del sistema.
