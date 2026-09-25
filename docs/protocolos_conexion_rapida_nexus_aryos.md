# Protocolos de conexión rapida Nexus + ARYOS

Objetivo: que preceptoría o soporte pueda recuperar asistencia y comunicaciones rapido ante fallas de servidor, WiFi, ESP32-C3, STM32, RFID RDM6300, pantalla TFT o perdida de conexión con ARYOS.

## Regla general de primeros 60 segundos

1. Confirmar si ARYOS abre localmente en el servidor: `http://127.0.0.1:8010/api/health`.
2. Si abre local pero no desde otros equipos, el problema es red/WiFi/IP.
3. Si no abre local, reiniciar servicio o arrancar ARYOS manualmente.
4. Si ARYOS abre pero no hay lecturas, revisar Nexus/RFID/ESP32.
5. Si hay alumnos esperando, tomar asistencia manual en Preceptoria y luego conciliar RFID.

## Matriz de accidentes posibles

| Accidente | Sintoma visible | Causa probable | Accion rapida |
|---|---|---|---|
| Servidor apagado | Nadie entra a ARYOS | Corte de energia, PC apagada | Encender servidor, revisar servicio, probar `/api/health` |
| Backend caido | Pantalla carga pero API falla | Proceso uvicorn detenido | Reiniciar ARYOS o servicio systemd/watchdog |
| Base bloqueada | Login funciona lento o falla al guardar | SQLite ocupado/disco lento | Esperar unos segundos, cerrar procesos duplicados, revisar backup |
| WiFi caido | Celulares/PC no abren ARYOS | Router/AP apagado o saturado | Probar cable/LAN, reiniciar AP, verificar IP del servidor |
| Cambio de IP | Antes entraba, ahora no | DHCP cambio IP local | Consultar IP del servidor y actualizar acceso local |
| Tunel externo caido | Fuera del colegio no abre | Cloudflare/tunel detenido | Reiniciar `aryos-tunnel.service` y revisar URL/DNS |
| ESP32-C3 sin señal | Nexus indica sin dispositivos | Sin 3V3, firmware detenido, WiFi/ESP-NOW caido | Reset ESP32, revisar 3V3/GND, cargar firmware |
| STM32 sin respuesta | TFT/LED/buzzer no reaccionan | Alimentacion o firmware STM32 | Reset Nucleo, revisar USB/5V, reflashear si persiste |
| RDM6300 sin lecturas | Tarjeta no registra | 5V/GND, TX/RX invertidos, antena suelta | Revisar 5V, PA10<-TX, PA9->RX, ANT1/ANT2 |
| Tarjeta desconocida | Lectura llega pero sin alumno | UID no asociado | Registrar UID o reasignar tarjeta |
| Doble lectura | Aparecen registros repetidos | Rebote de tarjeta o reintentos | Mantener deduplicacion por DNI/fecha, revisar intervalo de firmware |
| TFT apagada | Sistema funciona pero no muestra | Backlight sin VCC, SPI mal conectado | Revisar LED/backlight, 5V/3V3 y pines SPI |
| Buzzer/LED no responde | Lee pero no avisa localmente | Pin o GND suelto | Revisar PB8, PB9, PA8 y retorno GND |
| Navegador viejo | Cambios no aparecen | Service worker cacheado | Ctrl+F5 o limpiar datos locales en Ajustes |

## Protocolo A: ARYOS no abre

1. En el servidor, abrir `http://127.0.0.1:8010/api/health`.
2. Si no responde, iniciar ARYOS desde el script o servicio instalado.
3. Revisar que el puerto `8010` no este ocupado por otro proceso.
4. Si la base falla, ejecutar recuperacion desde backup.
5. Registrar asistencia manual mientras vuelve el sistema.

## Protocolo B: ARYOS abre en servidor pero no en otros equipos

1. Revisar WiFi/LAN del servidor.
2. Confirmar IP local del servidor.
3. Probar desde otro equipo con `http://IP_DEL_SERVIDOR:8010`.
4. Revisar firewall del servidor.
5. Si usa acceso externo, revisar tunel y DNS.

## Protocolo C: Nexus no recibe ESP32-C3

1. Verificar alimentación 3V3 y GND comun.
2. Resetear ESP32-C3 receptora.
3. Revisar firmware, SSID/red o canal ESP-NOW.
4. Confirmar UART: STM32 PA2 TX hacia GPIO4 RX ESP32 y STM32 PA3 RX hacia GPIO5 TX ESP32.
5. Si no vuelve, pasar a asistencia manual y dejar incidencia técnica.

## Protocolo D: RFID RDM6300 no lee

1. Verificar 5V y GND del RDM6300.
2. Confirmar P1: TX RFID a PA10 de Nucleo y RX RFID a PA9.
3. Revisar antena ANT1/ANT2.
4. Probar con tarjeta conocida y otra tarjeta alternativa.
5. Si lee UID pero no alumno, asociar tarjeta en ARYOS.

## Protocolo E: pantalla, LEDs o buzzer fallan

1. Si ARYOS registra asistencia, el problema es solo indicador local.
2. Revisar TFT ST7796: VCC, GND, PA5 SCK, PA7 MOSI, PA6 MISO, PB5 DC, PB6 CS, PB4 RESET, PB10 T_CS.
3. Revisar LED verde PB8, LED rojo PB9, buzzer PA8 y GND.
4. Si pantalla no prende, revisar backlight LED a 5V o 3V3 segun módulo.

## Protocolo F: recuperacion sin perder clase

1. Preceptor registra asistencia manual desde ARYOS si el servidor funciona.
2. Si ARYOS no funciona, usar planilla papel/CSV temporal con curso, DNI, hora y estado.
3. Cuando vuelva el sistema, cargar ausentes/tardanzas manualmente.
4. Mantener RFID como evidencia adicional, no como unica fuente ante falla.
5. Cerrar el incidente con hora de inicio, hora de recuperacion y causa probable.

## Indicadores recomendados

- Verde: API, WiFi/ESP32 y RFID con lectura reciente.
- Ambar: sistema responde pero sin lectura reciente.
- Rojo: sin dispositivos, sin RFID o archivo Nexus no disponible.

## Umbrales

- RFID sin lectura por mas de 10 minutos: advertencia.
- ESP32 sin señal por mas de 5 minutos: advertencia.
- Sin dispositivos registrados: incidente critico de configuracion.

