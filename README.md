# DDNS — APK v1.3

App Android **genérica** para actualizar un DNS dinámico que funcione por **URL de
actualización (web call)**, el sistema que usa cPanel y muchos paneles de hosting.

> **No lleva ninguna URL, dominio ni token dentro.** Cada usuario pega la suya la primera vez.

## Qué hace
- **Actualizar ahora**: llama a la URL y escribe el resultado en el registro de la app.
- **Automático cada 5 o 10 minutos**, a elegir en la pantalla, y sobrevive a reinicios.
- **Funciona igual con WiFi que con datos móviles.** No hay filtro de red ni permisos de
  ubicación: usa la conexión que haya en ese momento.
- Muestra **IP pública**, **lo que resuelve el DNS antes y después** (vía DNS-over-HTTPS, sin
  caché) y si coincide: `OK coincide` o `OJO: no coincide con X`.
- Registro con fecha y hora de cada intento, y botón para borrarlo.

## Cómo se usa (el resumen también está dentro de la app, en la pantalla principal)
1. Instala el APK (permitir "origen desconocido").
2. Consigue la **URL de actualización** de tu proveedor:
   - cPanel: busca **«DNS dinámico» / «Dynamic DNS»** y crea el enlace *web call*.
   - Otros paneles: suelen dar una URL tipo `https://midominio.com/ddns.php?host=...&ip=...`.
   - Si no aparece en el panel, pídesela a tu proveedor: es un enlace de actualización automática.
3. Pégala en el campo **URL** (si se te olvida `https://`, la app lo añade sola).
4. Opcional: **host a comprobar** (p. ej. `casa.midominio.com`) — solo para verificar.
5. Elige **cada 5 o 10 min**, activa **"Actualizar automáticamente"** y pulsa **"Actualizar ahora"** para la primera prueba.
6. La explicación completa está detrás del botón **"¿Ayuda?"** de la cabecera (ya no ocupa pantalla).

## Avisos
- La periodicidad usa `AlarmManager`, porque Android no permite JobScheduler por debajo de 15 min.
- En Doze (móvil mucho rato quieto) el sistema puede retrasar la alarma unos minutos.
- Doze puede retrasar la ejecución: Ajustes → Batería → **sin restricciones** para esta app.
- El enlace de actualización es **secreto**: quien lo tenga puede cambiar tu DNS.
- La actualización se hace **con la IP del dispositivo que llama**. Por eso, si actualizas
  desde el móvil en datos móviles, el dominio apuntará a la IP de la operadora (normalmente
  detrás de CGNAT, no accesible desde fuera). Para un DDNS de casa, ejecútalo desde la red de casa.

## Permisos
- **INTERNET** y **ACCESS_NETWORK_STATE**: lo mínimo para llamar a la URL.
- **RECEIVE_BOOT_COMPLETED**: reprogramar la tarea tras reiniciar el móvil.
- Sin ubicación, sin WiFi, sin almacenamiento. Nada más.
