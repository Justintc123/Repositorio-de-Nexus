# NEXUS + A.R.Y.O.S.

## Presentación del proyecto

NEXUS + A.R.Y.O.S. busca facilitar la organización de una institución educativa
mediante una plataforma común para asistencia, calificaciones, trabajos,
comunicados, documentos y seguimiento de estudiantes.

La propuesta combina el campus A.R.Y.O.S. con NEXUS, que coordina el servidor y la
conexión con los dispositivos RFID. El alcance contempla la implementación
institucional completa.

## Docentes titulares y adultos responsables

- **Leandro Boned**
- **Víctor Imobedorff**

## Equipo de trabajo

- **Justin Terrel:** coordinación general y desarrollo de NEXUS y A.R.Y.O.S.
- **Tiziano Del Papa:** programación y pruebas funcionales.
- **Juan Martín Orona Vizcaino:** diseño y ajustes de la carcasa.
- **Franco del Monte:** placa, pantalla e interfaz del dispositivo.
- **Santiago Naveira:** coordinación, documentación y presentación.
- **Ian Hugo Gonzalez:** PCB, cableado y pruebas de conexiones.
- **Tiziano Arrieta:** apoyo en PCB, pruebas y documentación.

## Usuarios y funcionamiento

El campus dispone de perfiles de alumno, docente, preceptor, tutor y administrador.
Cada uno accede a las funciones relacionadas con sus tareas.

El alumno consulta trabajos, notas y faltas. El docente publica actividades,
revisa entregas y carga calificaciones. Preceptoría registra asistencia y
convivencia. Los tutores consultan la información de los alumnos vinculados.
Administración gestiona usuarios, cursos, permisos y configuración.

Para la asistencia RFID, el recorrido previsto conecta la credencial, el módulo
lector, el servidor y el campus. La confirmación al usuario debe corresponder a
un registro efectivamente guardado.

## Estado al 12 de noviembre de 2026

El equipo estima un avance general de aproximadamente **90%**. Se levantó el
servidor y se informó acceso en red durante las pruebas. Se mejoró el campus,
se instaló el cliente Android en un teléfono y se probó la activación de cuentas
por correo.

La comunicación UART entre la STM32 y la emisora fue probada en ambos sentidos
según el equipo. El recorrido completo por ESP-NOW, USB, servidor y respuesta
continúa pendiente. La fabricación definitiva de la PCB, el montaje de la
carcasa y las pruebas de aceptación requieren confirmación.

[Ver la actualización técnica completa](ACTUALIZACION_AVANCES_2026-11-12.md).

## Financiamiento y cronograma

El proyecto obtuvo un bono de **$1.180.000 argentinos** mediante el **Fondo
Municipal de Innovación Educativa 2026**, para desarrollo, prototipado y pruebas.

El inicio documentado es el **06/08/2026** y la finalización prevista es el
**26/11/2026**. Los informes mensuales conservan la evolución y las dificultades
de cada etapa.

## Próximos pasos

- Completar la comunicación RFID de ida y vuelta y comprobar el registro en el campus.
- Validar credenciales desconocidas, duplicados y recuperación ante desconexiones.
- Consolidar la instalación, las copias de seguridad y las pruebas de los cinco perfiles.
- Confirmar la fabricación y el montaje definitivo de placa y carcasa.
- Incorporar fotografías y resultados de pruebas al registro de avances.

## Informes

- [Índice de informes mensuales](informes_avance/00_INDICE_INFORMES_AVANCE.md)
- [Informe del segundo mes](INFORME_AVANCE_MES_2_NEXUS_ARYOS.md)
- [Informe del tercer mes](INFORME_AVANCE_MES_3_NEXUS_ARYOS.md)
- [Informes semanales](informes_semanales/00_INDICE_INFORMES_SEMANALES.md)
