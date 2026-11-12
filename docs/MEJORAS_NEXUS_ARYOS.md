# Mejoras de Nexus + A.R.Y.O.S

**Actualizado al 12/11/2026.** La descripción general siguiente se complementa
con el [informe de avances actuales](ACTUALIZACION_AVANCES_2026-11-12.md).

## Incorporaciones recientes

- Interfaz local v69, navegación móvil con Configuración y Más, y menús que se
  mantienen dentro de la pantalla.
- Separación de comunicados y mensajes, boletín compacto y ajustes de formularios.
- Consulta de faltas y asistencia manual de respaldo desde preceptoría.
- APK Android 1.1.0 instalado por USB, nuevo logo y estados de carga/conexión.
- Cliente Windows empaquetado; Linux e iOS permanecen como ampliaciones pendientes.
- Primer acceso mediante correo, creación de contraseña y activación real probada.
- Preparación y arranque del servidor escolar, con acceso de red confirmado por
  el usuario durante las pruebas.
- Puente USB local a 115200, conectado a la base del campus actual, y credencial
  ficticia DEMO-BOTON-001 preparada para el botón USER.
- UART STM32–emisora probada en ambos sentidos según el equipo. Falta validar
  el recorrido completo ESP-NOW–USB–servidor–respuesta.

## Resumen

Durante el desarrollo se trabajó para convertir una idea inicial en un sistema
escolar integrado, claro para cada usuario y preparado para crecer.

Nexus cumple el papel de central de coordinación. A.R.Y.O.S es el campus que
utilizan las personas para consultar y registrar información escolar.

## Mejoras de la plataforma

Se organizó el campus en módulos de uso cotidiano:

- inicio;
- comunicados;
- agenda;
- trabajos prácticos;
- entregas;
- asistencia;
- calificaciones;
- documentos;
- mensajería;
- convivencia;
- reportes;
- configuración.

La navegación fue adaptada para que cada perfil encuentre sus funciones sin
recorrer pantallas que no necesita.

## Perfiles de usuario

### Administración

Puede organizar usuarios, cursos, documentos, reportes, calendario y la
configuración general del sistema.

### Profesor o maestro

Puede crear trabajos, indicar cursos destinatarios, revisar entregas y cargar o
editar calificaciones. También puede elegir entre un promedio automático o una
nota final escrita manualmente.

### Preceptoría

Puede seleccionar un curso, tomar asistencia, registrar presentes, ausentes,
tardanzas y retiros, además de registrar situaciones de convivencia y descargar
reportes.

### Alumno

Puede consultar sus trabajos, entregas, comunicados, agenda, documentos y notas
separadas por trimestre.

### Tutor

Puede consultar la información habilitada del alumno vinculado y recibir los
comunicados correspondientes.

## Calificaciones

La vista de notas se reorganizó para mostrar cada materia de forma horizontal,
con casillas para las evaluaciones y una casilla final. Esto permite distinguir
el tipo de evaluación y ver rápidamente si una materia tiene notas, promedio o
un resultado pendiente.

Se contemplaron:

- notas individuales;
- promedio automático;
- nota final manual;
- edición posterior por parte del docente;
- separación por trimestre;
- materias sin calificaciones cargadas;
- informe imprimible.

## Asistencia y convivencia

Las listas extensas se dividieron por curso y se incorporó un área desplazable.
Así, el personal puede trabajar con un grupo concreto sin tener que recorrer a
todos los alumnos al mismo tiempo.

También se prepararon acciones para registrar tardanzas, retiros, observaciones,
amonestaciones y otras medidas de convivencia.

## Comunicación

La mensajería permite buscar contactos por nombre de usuario y prioriza las
personas con las que ya existe una conversación. También muestra el estado o la
última conexión conocida.

Los mensajes contemplan acciones habituales como responder, reenviar, editar,
reaccionar y eliminar, de acuerdo con el tipo de mensaje y los permisos.

## Integración física

El sistema físico está compuesto por un lector RFID, una placa STM32, dos
ESP32-C3, una pantalla, indicadores luminosos y un buzzer.

El lector identifica una tarjeta de prueba. La STM32 procesa el evento y las
ESP32 lo transmiten hasta la central. La pantalla muestra estados simples como
esperando, leyendo, registrado, error o sin conexión.

## PCB de interconexión

Se diseñó una placa de interconexión para reemplazar el protoboard y ordenar los
cables Dupont. La propuesta separa los grupos de pantalla, RFID, ESP32, LEDs y
buzzer.

La placa todavía debe fabricarse y probarse. La documentación pública conserva
el pinout y la explicación del cableado, pero no publica los archivos editables
ni los archivos de fabricación.

## Continuidad ante fallas

Se documentaron procedimientos para revisar qué ocurre si falla:

- el servidor;
- la red Wi-Fi;
- la conexión USB;
- una ESP32;
- la STM32;
- el lector RFID;
- la pantalla;
- la comunicación con el campus.

La idea es que una falla puntual no borre la información ni detenga toda la
actividad escolar. Cuando vuelve la conexión, los registros pueden revisarse y
sincronizarse según el procedimiento definido.

## Estado del proyecto

El sistema web y la arquitectura general se encuentran avanzados. Las cinco
ESP32-C3 disponibles fueron probadas correctamente y se seleccionaron dos para
el montaje final.

La PCB está diseñada, pero aún no fabricada. La carcasa y la validación final
del montaje físico continúan en desarrollo. El avance general informado es del
aproximadamente 90% según la estimación del equipo al 12/11/2026. Las pruebas de
integración, fabricación y cierre pendientes se detallan en la actualización;
no se consideran completadas por el solo hecho de alcanzar esa estimación.
