# Avances de NEXUS + A.R.Y.O.S. — 12 de noviembre de 2026

**Avance general estimado por el equipo: aproximadamente 90%.**

Este documento actualiza el estado del proyecto después del informe del segundo
mes. El 65% que figura en los informes anteriores corresponde a ese período;
el 90% es una estimación actual del equipo, no una medición de pruebas aprobadas
ni una certificación de disponibilidad para uso institucional.

## Resumen

NEXUS integra el servidor y la comunicación con los dispositivos de asistencia.
A.R.Y.O.S. es el campus que utilizan alumnos, docentes, tutores, preceptores y
administradores. El desarrollo es grupal, con la coordinación de Justin Terrel
y las responsabilidades que se detallan en la presentación institucional.

Se avanzó en el servidor escolar, la interfaz por roles, los clientes para
Android y Windows, el primer acceso por correo y la integración del receptor
USB con la base del campus. La etapa actual concentra el trabajo en validar el
recorrido completo de asistencia, consolidar la instalación y cerrar las pruebas.

El equipo ganó un bono de **$1.180.000 argentinos** mediante el **Fondo Municipal
de Innovación Educativa 2026**, destinado al desarrollo, prototipado y demás
etapas de NEXUS. Este importe corresponde al aporte otorgado; no representa
una rendición de gastos ni el saldo disponible.

## 1. Campus escolar y experiencia de uso

Se mejoró la presentación del campus para que cada perfil encuentre sus tareas
habituales con menos pasos. Entre los avances documentados están:

- separación de **Comunicados** y **Mensajes**;
- consulta de faltas para alumnos y tutores, y registro manual desde preceptoría;
- organización de la asistencia por curso y selección de estados;
- boletín más compacto, con materias y calificaciones organizadas en grilla;
- ajustes de proporciones del encabezado, tarjetas y formularios;
- revisión de la carga de trabajos y distribución de sus paneles;
- estados y animaciones de carga;
- sección informativa de permisos reservada al administrador;
- navegación y acciones adaptadas a las funciones de cada rol.

La revisión local más reciente utiliza recursos web **v70** (v69 de navegación y v70 de identidad visual). En teléfonos se
incorporó una barra con Inicio, Comunicados, Mensajes, Configuración y Más.
El menú de cuenta y el de secciones adicionales se abren dentro del área visible,
corrigiendo el panel que antes quedaba parcialmente fuera de pantalla.
Dentro de la aplicación Android se oculta el aviso redundante de instalar la app.

Se realizaron comprobaciones automatizadas de navegación, permisos y adaptación
a distintos anchos de pantalla. Estas comprobaciones complementan las pruebas
manuales; no sustituyen una evaluación institucional con usuarios reales.

## 2. Aplicaciones instalables e identidad visual

### Android

Se generó e instaló por USB una actualización **1.1.0** del cliente A.R.Y.O.S.
en un teléfono físico. Se verificaron la compilación, la firma, la instalación
y el inicio de la aplicación. Se incorporaron el logo elegido, una barra de
carga, mensajes de conexión y ajustes del encabezado.

La aplicación muestra el campus mediante Android WebView y se conecta al
servidor configurado. Los usuarios y datos escolares permanecen en el servidor.
La versión del APK y la versión de recursos web son independientes: actualizar
la interfaz del servidor no implica necesariamente generar otro APK.

El paquete actual usa firma de desarrollo. No se informa publicación en Google
Play ni se da por implementada una solución de notificaciones push nativas.

### Windows y otras plataformas

Se dispone de un cliente Windows empaquetado, basado en WebView2. Este cliente
permite abrir el campus y configurar la dirección del servidor; debe distinguirse
del instalador o lanzador **Nexus.exe**, que pertenece a la operación del servidor.

Android y Windows son las plataformas prioritarias. Linux e iOS continúan como
objetivos de ampliación: en esta revisión no se verificaron paquetes finales
ni instalaciones funcionales para esas plataformas.

### Identidad

Se seleccionó una versión del logo de A.R.Y.O.S. con azul más vivo, manteniendo
la figura educativa. NEXUS adopta el logo cuadrado azul y azul marino, con la N del primer diseño
seleccionado y el nombre debajo, preparado para redes. Ambos logos se incorporan
a la portada de esta documentación. La documentación y las
presentaciones deben distinguir ambos componentes del mismo proyecto.

## 3. Primer acceso y creación de contraseña

Se implementó un flujo para que el administrador dé de alta una cuenta con
correo y el usuario cree su propia contraseña mediante un enlace de activación.
La cuenta permanece pendiente hasta completar ese paso; no hay elección pública
de roles ni alta libre de alumnos desde el formulario de activación.

Los enlaces son temporales, de un solo uso, y la base conserva su hash. El flujo
incluye límites de solicitudes, bloqueo de cuentas suspendidas y respuestas
que evitan revelar si un correo existe. Al activar se invalidan enlaces y
sesiones anteriores de esa cuenta.

Se configuró envío de prueba con Gmail y se completó una activación real,
confirmada por el usuario. La clave de aplicación se guarda cifrada localmente
con la protección de Windows; no forma parte del repositorio ni del APK.

La prueba local usa un destinatario permitido y una dirección accesible mediante
el puente USB del teléfono. Para el colegio todavía corresponde configurar el
remitente definitivo, la dirección pública y HTTPS. La recuperación de una
contraseña olvidada y la migración masiva de cuentas anteriores son tareas
distintas de este primer acceso y no se presentan como finalizadas.

## 4. Servidor y preparación para el colegio

Se preparó material de instalación y actualización para trasladar NEXUS a una
PC con Windows destinada al servidor escolar. Se obtuvo respuesta del servidor
y el usuario confirmó acceso desde la red local durante las pruebas.

En paralelo se conserva una copia de desarrollo del campus que escucha en
`127.0.0.1:8011`. Esa dirección es local a la PC; no equivale a una dirección
pública ni demuestra acceso desde otros equipos. La prueba Android por USB
utiliza un puente específico y tampoco prueba el despliegue por Internet.

En la prueba más reciente el equipo informó una instalación mediante
**Nexus.exe**, con configuración en `C:\ProgramData\Nexus\server.json` y una
tarea programada llamada **Nexus School**. Su configuración efectiva, el inicio
automático y el puente de esa instalación todavía deben verificarse. No se
debe asumir que comparte configuración o base de datos con la copia de desarrollo.

No se da por finalizado el dominio institucional, HTTPS ni la actualización del
servidor escolar a todas las revisiones locales más recientes.

## 5. Hardware y prueba de asistencia

El montaje actual comunicado por el equipo utiliza una **STM32F446RE** con
firmware normal y dos **ESP32-C3 SuperMini**, una emisora y una receptora.
El canal de ESP-NOW es **6**. La comunicación UART y la conexión USB del puente
trabajan a **115200 baudios**.

```text
Lector RFID → STM32F446RE → ESP32-C3 emisora
                               ↓ ESP-NOW, canal 6
PC con NEXUS/ARYOS ← USB ← ESP32-C3 receptora
           respuesta ← recorrido inverso → STM32
```

La conexión UART actual es:

| Señal STM32 | Conexión con la emisora |
|---|---|
| A0 / PA0, TX | GPIO4, RX |
| A1 / PA1, RX | GPIO5, TX |

Según la prueba física informada por el equipo, la emisora recibe la solicitud
completa y devuelve `ESP-NOW TIMEOUT`; se comprobó comunicación UART en ambos
sentidos. Esto deja pendiente confirmar la comunicación por radio, la entrega
USB al servidor y la respuesta de vuelta. Un timeout por sí solo no identifica
cuál de esos tramos falló.

En la PC de desarrollo se identificó la receptora en **COM4**, con rol
`SERVER_RECEIVER`, radio lista y canal 6. Se preparó y abrió un puente local a
115200, conservando el firmware de la placa. COM4 es el puerto observado en esa
PC: debe volver a comprobarse en otra instalación.

El botón USER envía la credencial sintética **DEMO-BOTON-001**. Se la dio de alta
en la copia local y se la vinculó a un alumno ficticio de prueba. Esto no implica
que esté dada de alta en la base utilizada por Nexus.exe.

El adaptador local ya contempla rechazo de tarjetas desconocidas, comprobación
de alumno activo, prevención de duplicados diarios y conservación de registros
manuales de preceptoría. Su lógica se probó con una base temporal. En el último
estado observado, el puente local todavía no había recibido solicitudes reales.

## 6. Estado de validación

| Área | Evidencia disponible | Qué falta cerrar |
|---|---|---|
| Campus | Copia local v69 y pruebas de interfaz por roles | Revisión completa en la instalación escolar |
| Android | APK 1.1.0 instalado e iniciado en teléfono | Validación final en la red y servidor definitivos |
| Windows | Cliente empaquetado | Validación de distribución e instalación definitiva |
| Activación por correo | Envío y activación reales confirmados en prueba local | Configuración institucional con HTTPS |
| Servidor escolar | Arranque y acceso de red informados | Consolidar versión, respaldo y arranque automático |
| UART | Comunicación en ambos sentidos informada por el equipo | Conservar evidencia de la prueba |
| Puente USB local | COM4 abierto a 115200 y credencial demo asociada | Recepción real y respuesta completa |
| ESP-NOW | Canal 6 configurado; timeout observado en emisora | Cerrar el recorrido de ida y vuelta |
| PCB y carcasa | Diseños y documentación anteriores | Confirmar fabricación, montaje y pruebas finales |
| Documentación | Actualización pública de avances | Adjuntar evidencias finales autorizadas |

## 7. Trabajo restante

1. Verificar el COM y el puente que usa la instalación de Nexus.exe, evitando
   que un monitor serie u otro puente ocupe el puerto.
2. Registrar una solicitud real al pulsar USER y devolver una respuesta con el
   mismo identificador. Un rechazo de credencial también demuestra comunicación
   si llega de vuelta a la STM32.
3. Repetir con tarjeta física asociada y comprobar que una lectura confirmada
   aparezca en el campus correcto, sin duplicar ni sobrescribir registros manuales.
4. Probar desconexión USB, reinicio de servidor y recuperación sin pérdida de datos.
5. Consolidar el paquete definitivo, las copias de seguridad y el acceso de red.
6. Completar validación de roles, fabricación/montaje pendiente y evidencias finales.

Estos pendientes corresponden a integración y cierre. La estimación del 90%
no elimina la necesidad de completar estas pruebas antes de usar datos reales
y operar el sistema de forma habitual en el colegio.

## Alcance de esta actualización pública

Se publican avances y explicaciones del funcionamiento. El código, firmwares,
instaladores, bases de alumnos, credenciales, claves de firma y configuraciones
privadas se conservan fuera de este repositorio documental.
