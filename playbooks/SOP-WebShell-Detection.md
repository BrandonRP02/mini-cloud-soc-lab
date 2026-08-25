# Standard Operating Procedure (SOP): Detección y Respuesta a Web Shells

- **Código:** SOP-SOC-001
- **Rol:** Analista SOC Tier 1 / Tier 2
- **Técnica MITRE:** T1505.003 (Server Software Component: Web Shell)

---

### 1. Detección y Triaje
1. Revisar la alerta FIM en el SIEM (Rule ID `554` / `550`).
2. Identificar la ruta completa del archivo modificado (`syscheck.path`) y el hash SHA-256.
3. Consultar la reputación del hash en plataformas de Threat Intelligence (VirusTotal / AlienVault OTX).

### 2. Contención Inmediata
1. Desactivar permisos de ejecución para mitigar persistencia:
   `chmod 000 /ruta/del/archivo/sospechoso.php`
2. Verificar conexiones de red activas originadas por el proceso web:
   `ss -tunap | grep -E ':80|:443|:8443'`

### 3. Erradicación y Recuperación
1. Mover el archivo comprometido a cuarentena aislada:
   `mv /ruta/del/archivo/sospechoso.php /root/quarantine/`
2. Analizar registros web para ubicar la IP de origen y vectores de inyección.
3. Restablecer el archivo legítimo desde copias de respaldo verificadas.
