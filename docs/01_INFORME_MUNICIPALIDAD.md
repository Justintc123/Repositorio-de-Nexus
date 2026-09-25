# Nexus + A.R.Y.O.S

## Presentación institucional

**Institución:** EST UTN “Werner von Siemens”  
**Municipalidad:** Municipalidad de San Martín  
**Docente responsable:** Victor Javier Imoberdorff  
**Equipo:** estudiantes de la institución  
**Inicio del proyecto:** 06/08/2026  
**Finalización prevista:** 26/11/2026  
**Avance informado:** 65%

## Resumen

Nexus + A.R.Y.O.S es un proyecto escolar que busca mejorar la forma en que se
organiza la información de una institución educativa.

La propuesta reúne en un mismo sistema tareas que normalmente se hacen por
separado: asistencia, notas, trabajos, comunicados, documentos y seguimiento de
los alumnos. También incorpora un dispositivo físico para registrar asistencia
mediante tarjetas RFID.

El proyecto combina programación, electrónica, diseño, organización de datos y
trabajo en equipo. Durante los primeros dos meses se desarrolló una versión
avanzada del sistema y se realizaron pruebas con los componentes principales.

## El problema que queremos resolver

En una escuela la información suele estar repartida entre planillas, mensajes,
carpetas y anotaciones. Esto puede provocar pérdida de tiempo, datos repetidos,
dificultad para encontrar información y errores al momento de comunicar algo.

El proyecto propone una plataforma común, con diferentes accesos según la
función de cada persona. Así, cada usuario encuentra las herramientas que
necesita sin tener que recorrer todo el sistema.

## Cómo funciona la propuesta

### A.R.Y.O.S

A.R.Y.O.S es la parte que utilizan las personas. Permite organizar:

- asistencia y novedades;
- comunicados;
- agenda escolar;
- trabajos prácticos y entregas;
- calificaciones por trimestre;
- documentos;
- mensajes;
- seguimiento de convivencia;
- reportes.

### Nexus

Nexus es la parte central que coordina la información y las conexiones. Su
función es unir el campus web con el dispositivo físico de asistencia y ayudar a
detectar problemas de comunicación.

### Sistema RFID

El lector RFID identifica una tarjeta de prueba. La lectura pasa por una placa
STM32, luego se transmite mediante dos módulos ESP32-C3 y finalmente llega al
sistema central. A.R.Y.O.S recibe el evento y puede registrar la asistencia.

## Usuarios contemplados

El sistema fue organizado para cuatro perfiles principales:

### Alumno

Puede consultar sus trabajos, entregas, comunicados, documentos y notas de cada
trimestre.

### Profesor o maestro

Puede publicar trabajos, revisar entregas, cargar calificaciones, calcular
promedios y establecer una nota final.

### Preceptor

Puede trabajar por curso, tomar asistencia, registrar ausencias, tardanzas,
retiros y situaciones de convivencia, además de descargar reportes.

### Tutor

Puede consultar la información habilitada del alumno vinculado, como
comunicados, agenda, trabajos y calificaciones.

También existe un perfil de administración para gestionar usuarios, cursos,
documentos, reportes y la configuración general.

## Avances alcanzados

Durante los primeros dos meses se logró:

1. Diseñar la estructura general de Nexus y A.R.Y.O.S.
2. Organizar la plataforma según perfiles de usuario.
3. Preparar la sección de notas por trimestre y materia.
4. Incorporar asistencia, convivencia y reportes para preceptoría.
5. Preparar mensajería, trabajos, entregas y documentos.
6. Definir el recorrido técnico del sistema RFID.
7. Probar las cinco ESP32-C3 Super Mini disponibles.
8. Seleccionar dos placas para el montaje final: una emisora y una receptora.
9. Diseñar varias revisiones de una PCB de interconexión.
10. Probar conectados la STM32, el RFID, la pantalla, los indicadores y las
    ESP32.
11. Documentar procedimientos de recuperación ante fallas.
12. Preparar informes, material de presentación y un plan de trabajo para las
    etapas restantes.

## Estado actual

La plataforma web se encuentra avanzada y cuenta con los perfiles principales.
El sistema físico fue probado como conjunto de prototipo. Las cinco ESP32-C3
funcionaron correctamente.

La PCB fue diseñada, pero todavía no fue fabricada. También quedan tareas de
ajuste de la carcasa, validación final del cableado y pruebas más extensas con
el montaje definitivo.

El porcentaje de avance informado es del 65%, porque la parte de software y la
arquitectura están más avanzadas que la fabricación y el cierre físico del
dispositivo.

## Dificultades y aprendizajes

Durante las pruebas se dañó la bobina del lector RFID por una conexión
incorrecta. El equipo revisó el procedimiento y decidió reforzar la identificación
de cables, verificar la alimentación antes de encender los módulos y documentar
las conexiones antes de continuar.

Esta situación permitió entender que un proyecto tecnológico no depende solo de
que el código funcione. También es necesario probar la alimentación, ordenar los
cables, proteger los componentes y dejar instrucciones claras para futuras
reparaciones.

## Próximas etapas

Durante los meses restantes se prevé:

- fabricar y probar la PCB;
- terminar la carcasa;
- validar las conexiones definitivas;
- confirmar la pantalla y su alimentación;
- realizar una prueba completa de asistencia;
- revisar la experiencia de los distintos perfiles;
- completar capturas, videos y evidencias;
- preparar una demostración estable;
- documentar el cierre del proyecto.

## Equipo de trabajo

- Justin Terrel: coordinación general, Nexus y A.R.Y.O.S.
- Tiziano Del Papa: programación y pruebas funcionales.
- Juan Martin Orona Vizcaino: diseño y correcciones de la carcasa.
- Franco del Monte: placa, pantalla e interfaz del dispositivo.
- Santiago Naveira: coordinación, documentación y presentación.
- Ian Hugo Gonzalez: PCB, cableado y pruebas de conexiones.
- Tiziano Arrieta: apoyo en PCB, pruebas y documentación; se incorporó durante
  las últimas dos semanas del período informado.

## Cierre

Nexus + A.R.Y.O.S representa una experiencia de aprendizaje integral. El equipo
trabaja sobre una necesidad concreta de la escuela y la aborda combinando una
plataforma digital con un dispositivo físico.

El proyecto todavía se encuentra en etapa de prototipo, pero ya cuenta con una
base funcional, pruebas realizadas y una planificación clara para completar la
integración antes del 26/11/2026.
