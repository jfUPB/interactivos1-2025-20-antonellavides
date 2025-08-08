# Unidad 2


## 🛠 Fase: Apply

### Actividad 04

<img width="600" height="600" alt="Screenshot 2025-08-08 092313" src="https://github.com/user-attachments/assets/b7bde889-2b6f-4cb1-b605-0569972d1457" />


### Actividad 05

```phyton
from microbit import *
import utime

TIEMPO_MIN = 10
TIEMPO_MAX = 60
TIEMPO_INICIAL = 20

estado = "CONFIG"  # Estados: CONFIG, ARMADA, EXPLOSION
tiempo = TIEMPO_INICIAL
ultimo_tick = utime.ticks_ms()

def mostrar_tiempo():
    # Mostrar solo la última cifra (para simplificar en micro:bit)
    display.show(str(tiempo % 10))

def aumentar_tiempo():
    global tiempo
    if tiempo < TIEMPO_MAX:
        tiempo += 1
    mostrar_tiempo()

def disminuir_tiempo():
    global tiempo
    if tiempo > TIEMPO_MIN:
        tiempo -= 1
    mostrar_tiempo()

def iniciar_cuenta_regresiva():
    global ultimo_tick
    ultimo_tick = utime.ticks_ms()

def explosion():
    display.show(Image.SKULL)
    pin0.write_digital(1)
    utime.sleep_ms(200)
    pin0.write_digital(0)

def reiniciar():
    global tiempo, estado
    tiempo = TIEMPO_INICIAL
    estado = "CONFIG"
    mostrar_tiempo()

mostrar_tiempo()

while True:
    if estado == "CONFIG":
        if button_a.was_pressed():
            aumentar_tiempo()
        if button_b.was_pressed():
            disminuir_tiempo()
        if accelerometer.was_gesture("shake"):
            estado = "ARMADA"
            iniciar_cuenta_regresiva()

    elif estado == "ARMADA":
        ahora = utime.ticks_ms()
        if utime.ticks_diff(ahora, ultimo_tick) >= 1000:
            ultimo_tick = ahora
            tiempo -= 1
            mostrar_tiempo()

        if tiempo <= 0:
            estado = "EXPLOSION"
            explosion()

        if pin_logo.is_touched():
            reiniciar()

    elif estado == "EXPLOSION":
        if pin_logo.is_touched():
            reiniciar()
```
