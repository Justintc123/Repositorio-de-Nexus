# Pinout Nexus STM32 Hub R4

## TFT ST7796 + touch XPT2046

| Nucleo | Modulo TFT/touch |
|---|---|
| 5V | VCC |
| GND | GND |
| PA5 | SCK / T_CLK |
| PA7 | MOSI / SDI / T_DIN |
| PA6 | MISO / SDO / T_DO |
| PB5 | DC |
| PB6 | CS |
| PB4 | RESET |
| PB10 | T_CS |
| 5V o 3V3 puenteado | LED/backlight |

## RDM6300 P1

| Nucleo | RDM6300 |
|---|---|
| PA10 | TX |
| PA9 | RX |
| NC | NC |
| GND | GND |
| 5V | 5V |

## ESP32-C3 Super Mini

| Nucleo | ESP32-C3 |
|---|---|
| 3V3 | 3V3 |
| GND | GND |
| PA2 TX | GPIO4 RX |
| PA3 RX | GPIO5 TX |

## LEDs y buzzer

| Nucleo | Salida |
|---|---|
| PB8 | LED verde + resistencia externa |
| PB9 | LED rojo + resistencia externa |
| PA8 | Buzzer + |
| GND | retorno de cada salida |

Importante: la ESP32-C3 va a 3V3. El RDM6300 va a 5V.
