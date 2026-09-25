# 01 - Santi: coordinacion y sistema

Tu tarea es ordenar el trabajo y asegurarte de que Nexus/A.R.Y.O.S quede andando
en la computadora vieja.

## Primera media hora

1. Abrir `00_LEER_PRIMERO_JUEVES.md`.
2. Repartir los readmes.
3. Ubicar la carpeta del Nexus viejo.
4. Hacer backup antes de copiar nada.

El backup puede llamarse:

```text
Nexus_BACKUP_2026-09-10
```

## Pasar cambios

Abrir esta guia:

```text
nexus_core/docs/PASAR_CAMBIOS_A_PC_NEXUS_ANTIGUO.md
```

Si estan en Linux:

```bash
cd nexus_core
bash scripts/instalar_actualizacion_aryos_linux.sh /ruta/al/NexusViejo/nexus_core
```

Si estan en Windows:

```powershell
cd nexus_core
.\scripts\windows\instalar_actualizacion_aryos_windows.ps1 -Destino "C:\Nexus\nexus_core"
```

## Probar que abre

Desde la carpeta:

```text
nexus_core/System-ARYOS
```

Ejecutar:

```bash
python3 -m uvicorn backend.app:app --host 127.0.0.1 --port 8010
```

Abrir:

```text
http://127.0.0.1:8010
```

Si se ve viejo o raro, apretar:

```text
Ctrl + F5
```

## Checklist de Santi

Probar rapido:

- Admin entra.
- Alumno ve inicio, trabajos y boletin.
- Docente/Maestro ve notas y trabajos.
- Preceptor ve toma de lista/preceptoría.
- Mensajes permite buscar contacto.
- Nexus muestra diagnóstico rapido.

## Dominio/acceso externo

Si queda tiempo, mirar:

```text
nexus_core/docs/aryos_acceso_externo.md
nexus_core/docs/aryos_produccion_colegio.md
```

No te quedes trabado con el dominio si la demo local todavia no funciona. La
prioridad es que la presentación salga.

## Al final

Juntar a todos y preparar la demo con el archivo:

```text
05_CONTROL_PRESENTACION.md
```

