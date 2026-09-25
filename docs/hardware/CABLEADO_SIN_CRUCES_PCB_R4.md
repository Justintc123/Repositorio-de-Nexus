# Cableado sin cruces - Nexus STM32 Hub R4

Esta revision esta pensada para conectar con Dupont sin volver a armar una protoboard.

## Regla de montaje

Cada bloque tiene dos headers paralelos:

| Lado | Uso |
| --- | --- |
| DESDE_NUCLEO | Entran los cables que vienen desde la STM32 Nucleo-F401RE |
| HACIA_MODULO | Salen los cables hacia TFT, RDM6300, ESP32-C3, LEDs o buzzer |

La idea es conectar pin 1 con pin 1, pin 2 con pin 2, etc. dentro de cada bloque. Si se usan cables Dupont del mismo largo por bloque, los cables quedan paralelos y no hace falta cruzarlos.

## Orden sugerido físico

Colocar la PCB a la derecha de la Nucleo, con el texto de la placa mirando hacia arriba.

1. Conectar primero GND y alimentación.
2. Conectar el bloque TFT completo en orden vertical.
3. Conectar RDM6300 P1 completo en orden vertical.
4. Conectar ESP32-C3 completo en orden vertical.
5. Conectar LEDs y buzzer al final.

## Bloque TFT

| Orden | Nucleo | Modulo TFT |
| --- | --- | --- |
| 1 | 5V | VCC |
| 2 | GND | GND |
| 3 | PA5 | SCK |
| 4 | PA7 | MOSI |
| 5 | PA6 | MISO |
| 6 | PB5 | DC |
| 7 | PB6 | CS |
| 8 | PB4 | RST |
| 9 | PB10 | TOUCH_CS |
| 10 | 5V o control backlight | LED |

## Bloque RDM6300

| Orden | Nucleo | RDM6300 P1 |
| --- | --- | --- |
| 1 | PA10 RX | TX |
| 2 | PA9 TX | RX |
| 3 | NC | NC |
| 4 | GND | GND |
| 5 | 5V | 5V |

## Bloque ESP32-C3

| Orden | Nucleo | ESP32-C3 Super Mini |
| --- | --- | --- |
| 1 | 3V3 | 3V3 |
| 2 | GND | GND |
| 3 | PA2 TX | GPIO4 RX |
| 4 | PA3 RX | GPIO5 TX |

## Bloque LEDs y buzzer

| Orden | Nucleo | Salida |
| --- | --- | --- |
| 1 | PB8 | LED verde + resistor |
| 2 | GND | LED verde GND |
| 3 | PB9 | LED rojo + resistor |
| 4 | GND | LED rojo GND |
| 5 | PA8 | Buzzer + |
| 6 | GND | Buzzer - |

## Nota importante

La PCB no corrige automáticamente un módulo con pinout distinto. Antes de fabricar, comprobar el orden real de pines de la pantalla TFT, porque algunos módulos ST7796/XPT2046 cambian el orden del header.
