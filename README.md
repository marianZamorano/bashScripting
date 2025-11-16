# Práctica de Bash Scripting

## Nivel 1: Fundamentos del scripting en Bash

**Objetivo:**  
Aprender a crear y ejecutar scripts, usar variables, condicionales, loops y parámetros.

**Escenario:**  
Tu empresa necesita un script para verificar la salud de un servicio en Linux (por ejemplo, Nginx o Apache).

**Laboratorio:**  
Crea un script `check_service.sh` que:

- Reciba el nombre del servicio como parámetro.  
  Ejemplo: `./check_service.sh nginx`

1. Verifique si el servicio está activo (`systemctl is-active`).
2. Si el servicio no está activo, muestre un mensaje de alerta.
3. Guarde el resultado (activo/inactivo) en un archivo `service_status.log`.

**Bonus:**
- Agrega timestamp a los logs.
- Envía una notificación por correo (puedes usar `mail` o `sendmail`).

## Nivel 2: Automatización de tareas de mantenimiento

**Objetivo:**  
Aprender a manipular archivos, redirigir salidas y usar tareas programadas.

**Escenario:**  
Necesitas limpiar los logs antiguos del sistema para liberar espacio en disco.

**Laboratorio:**  
Crea un script `cleanup_logs.sh` que:

1. Busque en `/var/log` todos los archivos con más de 7 días.
2. Los comprima (`tar.gz`) y mueva a una carpeta `/backup/logs/`.
3. Elimine los archivos originales luego de confirmar la compresión.
4. Genere un log con las acciones realizadas.

**Bonus:**  
Configura este script en cron para que se ejecute cada noche a las 2 AM.  
Ejemplo:  
```
0 2 * * * /home/devops/scripts/cleanup_logs.sh
```

**Creación de archivos de logs falsos**  
Ejecuta este bloque de comandos en tu terminal Bash:

```bash
# Crear varios archivos de logs
touch app.log error.log access.log nginx.log system.log old_app.log old_error.log

# Agregar contenido simulado
echo "INFO - Application started successfully" > app.log
echo "ERROR - Database connection failed" > error.log
echo "GET /index.html 200 OK" > access.log
echo "nginx: worker process started" > nginx.log
echo "System check OK" > system.log
echo "Old app log entry" > old_app.log
echo "Old error log entry" > old_error.log

# Modificar las fechas de algunos archivos para simular antigüedad
# Archivos antiguos (10 días)
touch -d "10 days ago" old_app.log old_error.log
# Archivos recientes (2 días)
touch -d "2 days ago" app.log error.log access.log
# Archivos de hoy
touch nginx.log system.log
```

## Nivel 3: Despliegue automatizado (mini-CI/CD)

**Objetivo:**  
Practicar la integración continua y automatización de despliegues simples con Bash.

**Escenario:**  
Cada vez que un desarrollador actualiza el repositorio de Git, se debe desplegar el nuevo código en un servidor web.

**Laboratorio:**  
Crea un script `deploy_app.sh` que:

1. Clone o actualice el repositorio desde GitHub  
   (https://github.com/rayner-villalba-coderoad-com/clash-of-clan)
2. Reinicie el servicio (por ejemplo, `systemctl restart nginx` o `pm2 restart app`).
3. Guarde el resultado del despliegue en un archivo `deploy.log`.

**Bonus:**
- Envía una notificación al Slack o Discord del equipo usando un webhook.
- Agrega control de errores (por ejemplo, si falla `git pull`, abortar el despliegue).

## Nivel 4: Monitoreo y Alertas

**Objetivo:**  
Aprender a recopilar métricas y generar alertas con Bash.

**Escenario:**  
Quieres monitorear el uso de CPU, RAM y espacio en disco, y enviar alertas si se superan ciertos límites.

**Laboratorio:**  
Crea un script `monitor_system.sh` que:

1. Mida:
   - Porcentaje de CPU (`top` o `mpstat`)
   - Uso de RAM (`free -m`)
   - Uso de disco (`df -h`)
2. Si alguno de estos supera los límites definidos (por ejemplo, 80%), guarde una alerta en `alerts.log`.
3. Envíe una alerta por correo o webhook.

**Bonus:**
- Agrega colores a la salida del terminal (verde = OK, rojo = alerta).
- Guarda un histórico diario de métricas (`metrics_YYYYMMDD.log`).

## Requisitos técnicos

- **Sistema operativo:** Ubuntu o cualquier distribución Linux o MacOS.
- **Herramientas:** bash, cron, git, curl, mailutils.
- **Editor:** vim, nano, neovim o VS Code con terminal integrado.