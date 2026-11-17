# Informe de avance del tercer mes — NEXUS + A.R.Y.O.S.

**Período del tercer mes:** 07/10/2026 al 06/11/2026.  
**Actualización complementaria:** avances documentados hasta el 12/11/2026.  
**Inicio del proyecto:** 06/08/2026.  
**Finalización prevista:** 26/11/2026.  
**Avance general estimado por el equipo al 12/11/2026:** aproximadamente 90%.

## 1. Resumen y alcance

Durante esta etapa se continuó la preparación de NEXUS + A.R.Y.O.S. para su implementación directamente en una institución educativa. El alcance comprende el servidor, el campus y las funciones de estudiantes, docentes, tutores, preceptores y administradores, junto con los dispositivos de asistencia RFID.

Se avanzó en la plataforma, la preparación del servidor, los clientes instalables y la integración física. Las pruebas de un dispositivo permiten verificar una parte del sistema dentro del despliegue institucional. La institución destinataria no se identifica en esta copia pública.

El informe distingue el período mensual de los avances posteriores conocidos al 12 de noviembre. Los hitos que no tienen una fecha individual respaldada se presentan como estado acumulado al corte. El 90% es una estimación del equipo y la integración RFID completa sigue pendiente de validación.

## 2. Plataforma y servidor

Se consolidaron las vistas por rol y las funciones de asistencia, calificaciones, trabajos, documentos, comunicados y mensajería. Se mejoraron la consulta de faltas para alumnos y tutores, la asistencia manual por curso, la distribución de paneles y el funcionamiento en pantallas de distintos tamaños.

Se prepararon materiales de instalación y actualización para Windows. Se obtuvo respuesta del servidor y el equipo informó acceso desde la red local. Las copias de desarrollo y la instalación institucional deben cotejarse para confirmar que utilicen la versión, la configuración y las bases previstas.

## 3. Avances complementarios hasta el 12 de noviembre

El campus alcanzó recursos web v70, con revisión de identidad visual y navegación móvil. Se separaron Comunicados y Mensajes, se ajustó el boletín y se corrigieron menús que quedaban fuera del área visible.

El cliente Android 1.1.0 fue compilado, firmado con clave de desarrollo, instalado por USB e iniciado en un teléfono físico. También se dispone de un cliente Windows basado en WebView2 para abrir el campus y configurar la dirección del servidor. La instalación definitiva de estos clientes requiere validación en la red destino.

Se implementó el primer acceso por correo: el administrador crea la cuenta y el usuario genera su contraseña mediante un enlace temporal de un solo uso. Se completaron un envío y una activación reales en una prueba local. Continúan pendientes el remitente definitivo, la dirección pública y HTTPS. La recuperación de contraseñas y la migración masiva de cuentas son tareas diferentes.

## 4. Hardware e integración RFID

El montaje actual informado utiliza STM32F446RE y dos ESP32-C3 SuperMini, una emisora y una receptora, con ESP-NOW en canal 6. La comunicación UART entre STM32 y emisora fue probada en ambos sentidos según el equipo.

La emisora recibe la solicitud y devuelve ESP-NOW TIMEOUT. Por lo tanto, falta localizar y resolver el tramo que impide completar el recorrido por radio, USB y servidor, y devolver la respuesta al dispositivo.

En la PC de desarrollo se identificó la receptora en COM4 y se abrió un puente local a 115200 baudios. Se vinculó la credencial ficticia DEMO-BOTON-001 a un alumno de prueba. Ese puerto y esa asociación corresponden a esa copia local y deben comprobarse en la instalación destinataria.

La lógica del adaptador se ensayó con una base temporal para rechazar credenciales desconocidas, comprobar alumnos activos, evitar duplicados diarios y conservar los registros manuales. El puente local todavía no había recibido solicitudes reales en el último estado documentado.

## 5. Placa, carcasa y documentación

Se conservaron y revisaron los diseños de la PCB de interconexión y el montaje de la carcasa. La fabricación definitiva, la revisión del cableado y las pruebas del conjunto deben confirmarse.

La documentación histórica R4 describe conexiones de una revisión anterior. Antes de reutilizarla se debe cotejar con el montaje STM32F446RE y su UART PA0/PA1. La documentación pública incluye explicaciones, lista de materiales y protocolos, mientras los editables, firmwares y archivos de fabricación se conservan por separado.

Se consolidaron informes mensuales y semanales, responsabilidades del equipo y procedimientos de recuperación ante problemas de servidor, red, USB y dispositivos.

## 6. Organización y financiamiento

El equipo distribuyó tareas de coordinación y programación, pruebas funcionales, placa y pantalla, carcasa, cableado y documentación. Las decisiones de integración se revisaron entre las áreas para mantener la continuidad del trabajo.

NEXUS obtuvo un bono de $1.180.000 argentinos mediante el Fondo Municipal de Innovación Educativa 2026, destinado al desarrollo, prototipado y pruebas. El monto corresponde al aporte otorgado; la ejecución de gastos y el saldo requieren su rendición específica.

## 7. Grado de cumplimiento al corte

- Campus y perfiles: desarrollados y probados en el entorno de desarrollo; falta completar la revisión institucional.
- Servidor: arranque y acceso de red informados; se debe consolidar versión, configuración, respaldos e inicio automático.
- Android: instalación e inicio en teléfono comprobados; falta validación final con el servidor destino.
- Windows: cliente empaquetado; queda verificar su distribución e instalación definitiva.
- Activación por correo: prueba local completada; pendiente configuración para el despliegue definitivo.
- RFID: UART informada como funcional; recorrido ESP-NOW, USB, servidor y respuesta pendiente.
- PCB y carcasa: diseños documentados; fabricación, montaje y validación final pendientes de confirmación.

## 8. Próximos pasos

1. Confirmar el puerto USB y el puente activos en la instalación mediante Nexus.exe.
2. Recibir una solicitud real y devolver una respuesta con el mismo identificador hasta la STM32.
3. Repetir con una tarjeta física asociada y verificar el registro en el campus correcto.
4. Probar duplicados, credencial desconocida, desconexión USB, reinicio y recuperación.
5. Consolidar instalación, copias de seguridad, versión y acceso de red.
6. Completar la revisión de los cinco perfiles y confirmar placa, carcasa y montaje.
7. Incorporar fotos, capturas, videos y resultados verificables para el cierre previsto.

## 9. Fuentes y criterio de elaboración

Informe retrospectivo basado en la actualización de avances del 12/11/2026, las mejoras de NEXUS + A.R.Y.O.S., los protocolos de conexión y los informes previos del repositorio. La actualización del 12 de noviembre tiene precedencia sobre las referencias técnicas históricas.

No se asignan fechas de ejecución ni resultados adicionales a tareas sin evidencia individual. Los avances posteriores a ese corte deberán agregarse con sus pruebas. Este informe sirve para preparar el cierre previsto y no constituye una certificación de finalización.
