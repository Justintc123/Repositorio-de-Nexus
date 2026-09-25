# 02 - Franco: placa, pantalla y UI del hardware

Tu tarea es que la parte física se vea mas prolija y entendible.

## Archivos que tenes que abrir

Firmware STM32:

```text
Arduino/stm32prueb/stm32prueb.ino
```

PCB mas nueva:

```text
hardware/nexus_stm32_hub_R4_clean_dupont/
```

Guia de pines:

```text
hardware/nexus_stm32_hub_R4_clean_dupont/docs/PINOUT.md
```

## Tareas principales

1. Revisar que la placa/conexiones tengan sentido.
2. Mejorar la fuente de la pantalla.
3. Cambiar texto pixelado por letras mas prolijas.
4. Mejorar la UI de la pantalla para que cualquiera entienda que pasa.

## Pantalla: estados que tiene que mostrar

La pantalla deberia poder mostrar mensajes tipo:

```text
Esperando tarjeta
Leyendo...
Asistencia registrada
Tarjeta no encontrada
Sin conexión
Reintentando
```

No hace falta que quede perfecto de una. Tiene que ser claro y presentable.

## Cuidado con esto

- No cambiar pines sin avisar.
- Si cambias pines, anotarlo en `PINOUT.md`.
- No dejar textos cortados.
- Que se lea desde cierta distancia.

## Para presentar

Preparar una frase corta:

```text
La placa lee el RFID, la STM32 procesa la lectura y Nexus registra la asistencia.
La pantalla muestra el estado para que el alumno sepa si quedo registrado.
```

