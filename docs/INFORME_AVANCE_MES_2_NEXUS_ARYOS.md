# Informe de avance - Nexus + A.R.Y.O.S

## Proyecto de integración tecnológica escolar

**Período informado:** 06/08/2026 al 06/10/2026  
**Finalización prevista:** 26/11/2026  
**Institución:** EST UTN "Werner von Siemens"  
**Municipalidad:** Municipalidad de San Martín  
**Docente responsable:** Victor Javier Imoberdorff  
**Avance estimado defendible:** 65%  

### Integrantes

- Justin Terrel
- Tiziano Del Papa
- Juan Martin Orona Vizcaino
- Franco del Monte
- Santiago Naveira
- Ian Hugo Gonzalez
- Tiziano Arrieta, incorporado durante las últimas dos semanas del período informado

---

## 1. Resumen ejecutivo

Durante los primeros dos meses se avanzó en la construcción de una plataforma
escolar integrada, compuesta por dos partes principales:

- **Nexus:** central técnica que coordina el servidor, los dispositivos físicos,
  el lector RFID y las comunicaciones.
- **A.R.Y.O.S.:** campus web para la gestión cotidiana de la institución:
  usuarios, roles, comunicados, agenda, trabajos, calificaciones, asistencia,
  documentos y seguimiento de convivencia.

El proyecto ya cuenta con una arquitectura funcional, una interfaz web adaptada
a los distintos roles escolares, firmware para el sistema RFID y diseños de PCB
para ordenar las conexiones entre la STM32, la pantalla, el lector y las ESP32-C3.

El foco del trabajo fue crear una solución que pueda ser utilizada por una
escuela real: clara para cada usuario, ampliable, reparable y preparada para
funcionar incluso cuando algún componente de red o hardware tenga problemas.

---

## 2. Objetivos del proyecto

El objetivo general es desarrollar un ecosistema escolar que centralice la
información y reduzca tareas repetitivas, manteniendo una conexión directa entre
la gestión digital y los dispositivos físicos del establecimiento.

Los objetivos específicos son:

1. Crear un campus web con funciones diferenciadas por rol.
2. Registrar asistencia mediante RFID.
3. Comunicar el dispositivo del aula con el servidor de forma inalámbrica.
4. Organizar calificaciones por materia, trimestre y tipo de evaluación.
5. Facilitar la comunicación entre docentes, alumnos, tutores y personal escolar.
6. Diseñar una PCB que reemplace el protoboard y ordene el cableado.
7. Preparar protocolos de recuperación ante cortes de Wi-Fi, servidor o hardware.
8. Dejar documentación para que otro integrante pueda instalar, probar y mantener
   el sistema.

---

## 3. Avances realizados

### 3.1 Plataforma A.R.Y.O.S.

Se implementó una estructura de campus con vistas diferenciadas para los roles
principales de la institución:

- **Administración:** usuarios, cursos, reportes, documentos, configuraciones,
  Nexus y control general.
- **Docente o maestro:** trabajos, entregas, calificaciones, cursos y alumnos a
  cargo.
- **Preceptoría:** toma de lista, asistencia, tardanzas, retiros, convivencia,
  amonestaciones y reportes descargables.
- **Alumno:** trabajos, entregas, comunicados, documentos, agenda y notas por
  trimestre.
- **Tutor:** seguimiento de alumnos vinculados, comunicados y consulta de
  información habilitada.

La navegación se adaptó para mostrar a cada usuario únicamente las funciones
relacionadas con su rol. También se trabajó en la distribución visual de los
paneles, los iconos de navegación, los estados de carga y la adaptación a
pantallas con distinto tamaño.

### 3.2 Calificaciones

La sección de notas fue reorganizada para que cada trimestre se consulte de
forma independiente. La vista muestra las materias en filas y las evaluaciones
en casillas consecutivas, indicando el tipo de nota y su valor.

También se contempló:

- promedio automático de evaluaciones;
- carga manual de una nota final por parte del docente;
- edición posterior de calificaciones;
- estado aprobado o pendiente;
- materias aunque todavía no tengan calificaciones;
- generación de informe en PDF.

La carga y actualización de calificaciones se vincula con la base de datos de
A.R.Y.O.S. y debe continuar validándose con datos reales antes de una puesta en
producción.

### 3.3 Mensajería y comunicaciones

Se incorporó una vista de contactos que prioriza las personas con las que ya
existe una conversación. Incluye búsqueda por nombre de usuario y muestra la
última conexión conocida.

Para los mensajes se prepararon acciones habituales: responder, reenviar,
editar, reaccionar y eliminar para el usuario o para todos, según el estado del
mensaje y los permisos correspondientes.

### 3.4 Asistencia y convivencia

La preceptoría dispone de una vista agrupada por curso, con selección de curso y
un área desplazable para evitar listados excesivamente largos.

Se contemplaron acciones por alumno:

- presente;
- ausente;
- tardanza;
- retiro;
- consulta del promedio y faltas;
- registro de medidas de convivencia;
- descarga de asistencia en CSV o PDF.

También se documentaron protocolos para conservar la operación cuando el
servidor, la red o el dispositivo RFID no estén disponibles temporalmente.

### 3.5 Hardware y RFID

El flujo técnico definido es:

```text
RDM6300 -> STM32 Nucleo-F401RE -> ESP32-C3 del aula
        -> ESP-NOW -> ESP32-C3 receptora -> USB -> Nexus/A.R.Y.O.S
```

El firmware de la STM32 contempla:

- lectura serial del RDM6300 a 9600 baudios;
- pantalla TFT por SPI;
- touch XPT2046 por SPI compartido;
- LEDs verde y rojo;
- buzzer;
- botón de operación;
- comunicación NDJSON con Nexus;
- respuesta visual ante lectura válida, inválida o sin conexión.

Se prepararon dos firmwares para las ESP32-C3 Super Mini:

- `nexus_espnow_aula_sender`: recibe los eventos desde la STM32 y los transmite
  por ESP-NOW;
- `nexus_espnow_server_receiver`: recibe los eventos inalámbricos y los entrega
  a la computadora por USB.

### 3.6 PCB de interconexión

Se diseñaron varias revisiones de una PCB de interconexión para reemplazar el
protoboard y ordenar los cables Dupont:

- R1: primera distribución;
- R2: organización de pares;
- R3: revisión con recorridos sin cruces;
- R4: revisión limpia para fabricación y conectores Dupont.

La revisión R4 contiene bloques separados para pantalla/touch, RFID, ESP32-C3,
LED verde, LED rojo y buzzer. La idea es conectar la Nucleo a un lado del bloque
y el módulo al otro, usando cables cortos y claramente identificados.

La documentación de hardware incluye el pinout, la lista de materiales, las
notas de fabricación y el cableado sin cruces. Antes de fabricar se debe
confirmar el modelo exacto de la pantalla y sus tensiones de alimentación.

### 3.7 Protocolos de recuperación

Se documentaron pasos para detectar y recuperar fallas en:

- servidor de Nexus;
- servicio web de A.R.Y.O.S.;
- conexión USB;
- Wi-Fi;
- ESP32-C3 del aula;
- ESP32-C3 receptora;
- STM32;
- lector RDM6300;
- pantalla o touch.

El principio de recuperación es conservar el registro local o manual de la
asistencia y sincronizarlo cuando vuelva la conexión, evitando que una falla
puntual detenga toda la operación.

---

## 4. Estado actual por área

| Área | Estado observado en el repositorio | Próximo paso |
|---|---|---|
| Campus A.R.Y.O.S. | Funcional en entorno de prueba | Validar con usuarios reales por rol |
| Roles y permisos | Implementados para pruebas | Revisar casos límite y cuentas definitivas |
| Calificaciones | Vista trimestral y carga preparadas | Probar edición, promedios y PDF |
| Mensajería | Funciones principales preparadas | Validar acciones sobre mensajes |
| Preceptoría | Asistencia por curso y reportes preparados | Prueba completa con un curso real |
| STM32 + RFID | Firmware y protocolo definidos | Prueba física completa |
| ESP32-C3 | Las cinco placas fueron probadas correctamente; se seleccionarán dos para el sistema final | Definir la placa emisora y la receptora, registrar MAC y realizar la prueba final |
| PCB | Revisiones R1 a R4 diseñadas | Revisar DRC, fabricar y probar continuidad |
| Carcasa | Trabajo asignado | Integrar dimensiones reales de PCB y pantalla |
| Documentación | Guías técnicas y de trabajo disponibles | Completar fechas, evidencias y responsables |

---

## 5. Incidente técnico registrado

Durante las pruebas se dañó la bobina del lector RFID debido a una conexión
incorrecta. El incidente sirvió para revisar el procedimiento de conexión,
separar las pruebas de alimentación de las pruebas de señal y reforzar la
documentación del cableado antes de volver a conectar los módulos.

No se registraron otros errores críticos durante la integración general. El
equipo informó que la STM32, la pantalla, el RFID, los indicadores y las ESP32
fueron probados conectados en conjunto. La PCB continúa en etapa de diseño y
todavía no fue fabricada.

## 6. Plan para los meses 3 y 4

### Mes 3: integración y validación

- cerrar el diseño mecánico de la carcasa;
- confirmar el modelo de pantalla;
- revisar la PCB y realizar la prueba de continuidad;
- seleccionar las dos ESP32-C3 que quedarán en el sistema final y registrar sus
  identificadores;
- conectar STM32, RFID, pantalla, LEDs y buzzer;
- validar el flujo completo de asistencia;
- probar los perfiles de administración, docente, preceptoría, alumno y tutor;
- corregir errores de interfaz, permisos y generación de PDF;
- medir tiempos de respuesta y recuperación ante desconexiones.

### Mes 4: demostración y preparación final

- completar pruebas de aceptación;
- preparar una demostración reproducible;
- documentar instalación y recuperación;
- generar capturas, videos y evidencias técnicas;
- preparar la presentación institucional;
- registrar riesgos pendientes y decisiones futuras;
- entregar una versión estable acompañada por su documentación.

---

## 7. Riesgos y puntos pendientes

Los puntos que todavía deben confirmarse antes de presentar el proyecto como
completamente terminado son:

- compatibilidad exacta entre la pantalla recibida y el controlador configurado;
- tensiones de VCC y backlight de la pantalla;
- adaptación de nivel del TX del RDM6300 hacia la STM32;
- alimentación estable de las ESP32-C3;
- estado final de la PCB después de la fabricación;
- prueba completa del enlace ESP-NOW en el aula;
- validación de datos y permisos con usuarios institucionales;
- política definitiva de contraseñas y eliminación de cuentas de prueba;
- fecha real de cada avance y responsables que lo realizaron.

Estos puntos no significan que el proyecto esté detenido: indican qué debe
validarse para pasar de una versión avanzada de demostración a una versión lista
para uso institucional.

---

## 8. Evidencias disponibles en el repositorio

- `docs/MEJORAS_NEXUS_ARYOS.md`
- `docs/protocolos_conexion_rapida_nexus_aryos.md`
- `docs/hardware/PINOUT_PCB_R4.md`
- `docs/hardware/BOM_PCB_R4.md`
- `docs/hardware/CABLEADO_SIN_CRUCES_PCB_R4.md`
- documentación de integración, pruebas y presentación del proyecto.

---

## 9. Evidencias a incorporar posteriormente

El equipo incorporará posteriormente capturas de pantalla, fotografías, videos
de las pruebas y cualquier medición que pueda respaldar el avance informado.
Estas evidencias se adjuntarán antes de entregar la versión definitiva a la
institución o a la Municipalidad de San Martín.

## 10. Datos que debe completar el equipo

Para convertir este borrador en el informe oficial necesito que confirmen:

1. Nombre oficial del proyecto y, si existe, número de expediente.
2. Tareas específicas de cada integrante.
3. Cantidad de tarjetas RFID leídas durante las pruebas.
4. Capturas, videos, mediciones o demostraciones que se adjuntarán.

Con los datos actuales, el documento puede presentarse como un informe de avance
técnico del 65%. La versión final deberá incorporar las evidencias visuales y,
si corresponde, el número de expediente o la denominación oficial del proyecto.
