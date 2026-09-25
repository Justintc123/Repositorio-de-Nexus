# Nexus STM32 Hub R4 Clean Dupont

PCB de interconexion para usar cables Dupont sin protoboard.

Cada bloque tiene dos headers: `DESDE_NUCLEO` y `HACIA_MODULO`. Conectas la Nucleo al primer header y el sensor/módulo al segundo. La PCB une cada pin con pista corta y recta, sin buses largos cruzando la placa.

En esta revision, las alimentaciones y GND estan separados por bloque para que el ruteo quede limpio. La referencia comun se mantiene en la Nucleo al conectar todos los GND correspondientes.

Componentes cubiertos:

- RDM6300 UART 125 kHz.
- TFT ST7796 SPI con touch XPT2046.
- ESP32-C3 Super Mini para ESP-NOW.
- LED verde externo.
- LED rojo externo.
- Buzzer externo.

Abrir con KiCad 10: `nexus_stm32_hub_R4_clean_dupont.kicad_pro`.
