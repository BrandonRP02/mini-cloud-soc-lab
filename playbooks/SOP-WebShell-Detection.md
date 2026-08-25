# Standard Operating Procedure (SOP): Deteccion y Respuesta a Web Shells

- **Codigo:** SOP-SOC-001
- **Rol:** Analista SOC Tier 1 / Tier 2
- **Tecnica MITRE:** T1505.003 (Server Software Component: Web Shell)

---

### 1. Deteccion y Triaje
1. Revisar la alerta FIM en el SIEM (Rule ID 554 / 550).
2. Identificar la ruta completa del archivo modificado (\syscheck.path\) y el hash SHA-256.
3. Consultar la reputacion del hash en VirusTotal / AlienVault OTX.

### 2. Contencion Inmediata
1. Desactivar permisos de ejecucion para mitigar persistencia:
   \\\ash
   chmod 000 /ruta/del/archivo/sospechoso.php
   \\\`n2. Verificar conexiones de red activas originadas por el servicio web:
   \\\ash
   ss -tunap | grep -E ':80|:443|:8443'
   \\\`n
### 3. Erradicacion y Recuperacion
1. Mover el archivo comprometido a un directorio de cuarentena aislado:
   \\\ash
   mv /ruta/del/archivo/sospechoso.php /root/quarantine/
   \\\`n2. Analizar registros web para ubicar la IP de origen y vectores de inyeccion.
3. Restablecer el archivo legitimo desde copias de respaldo verificadas.
