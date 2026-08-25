# Cloud SOC Lab: Wazuh SIEM & Detection Engineering

Entorno de Security Operations Center (SOC) desplegado en la nube sobre un servidor Linux (Ubuntu 22.04 LTS) optimizado para coexistencia segura y bajo consumo de recursos (6 GB RAM).

---

## ?? Arquitectura y Tecnologías
* **SIEM / XDR:** Wazuh v4.8 (Despliegue multi-contenedor optimizado con heap de Java a 2 GB).
* **Telemetría:** Agente Wazuh + File Integrity Monitoring (FIM) en tiempo real.
* **Ingeniería de Detección:** Reglas XML personalizadas mapeadas al marco **MITRE ATT&CK**.
* **Hardening y Coexistencia:** Aislamiento en puerto alternativo (`8443`) y sandbox de pruebas para garantizar cero impacto en servicios web preexistentes.

---

## ?? Escenarios de Detección Implementados

### 1. Detección de Web Shells vía FIM (MITRE ATT&CK T1505.003)
* **Monitoreo:** Vigilancia en tiempo real sobre el directorio web (`/opt/mini-soc-lab/lab_web_test/`).
* **Resultado:** Detección instantánea de adición de scripts maliciosos con cálculo automático de hash SHA-256.

![FIM Detection](docs/evidence-fim-webshell.png)

---

### 2. Detección de Comandos Ofuscados en Base64 (MITRE ATT&CK T1027 / T1059)
* **Ingeniería de Detección:** Regla XML personalizada (Rule ID: `100002`, Severidad 10) para identificar ejecución de payloads decodificados en memoria.
* **Resultado:** Alerta disparada e indexada en Threat Hunting tras detectar la ejecución.

![MITRE T1027 Alert](docs/evidence-mitre-t1027.png)

---

## ?? Estructura del Repositorio
```text
mini-cloud-soc-lab/
+-- README.md                          # Documentación principal del laboratorio
+-- docs/                              # Evidencias visuales del SIEM
¦   +-- evidence-fim-webshell.png
¦   +-- evidence-mitre-t1027.png
+-- configs/                           # Configuraciones de agentes y entorno
¦   +-- ossec-agent.conf
+-- custom-rules/                      # Reglas de detección personalizadas
¦   +-- local_rules.xml
+-- playbooks/                         # Procedimientos Operativos Estándar (SOP)
¦   +-- SOP-WebShell-Detection.md
+-- reports/                           # Informes técnicos de incidentes
    +-- INC-2026-08-001-Base64-Exec.md
