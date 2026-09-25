# 04 - Tizi/Ian: PCB de conexiones

Tu tarea es trabajar la PCB que reemplaza el protoboard.

## Que placa abrir

Usar la versión mas nueva:

```text
hardware/nexus_stm32_hub_R4_clean_dupont/
```

Archivo de KiCad:

```text
hardware/nexus_stm32_hub_R4_clean_dupont/nexus_stm32_hub_R4_clean_dupont.kicad_pro
```

## Objetivo

La PCB no es para reemplazar todos los módulos. Es para ordenar conexiones.

Se conecta por cables Dupont a:

- STM32 Nucleo;
- RDM6300 RFID;
- TFT;
- ESP32-C3 Super Mini;
- LED rojo;
- LED verde;
- buzzer.

## Tareas

1. Abrir KiCad.
2. Revisar que los conectores esten claros.
3. Separar bien bloques:
   - Nucleo;
   - TFT;
   - RFID;
   - ESP32;
   - LEDs;
   - buzzer.
4. Revisar que no haya pistas cruzadas raras.
5. Correr DRC.
6. Si queda bien, exportar Gerbers.

## Archivos utiles

```text
hardware/nexus_stm32_hub_R4_clean_dupont/docs/PINOUT.md
hardware/nexus_stm32_hub_R4_clean_dupont/docs/CABLEADO_SIN_CRUCES.md
hardware/nexus_stm32_hub_R4_clean_dupont/docs/BOM.md
```

## Para presentar

Si pueden, abrir la vista 3D de KiCad y mostrarla.

Frase corta:

```text
Esta PCB ordena el cableado y evita usar protoboard. Los módulos siguen
conectados por Dupont, pero cada pin queda identificado y limpio.
```

