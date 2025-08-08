# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 1

**Describe detalladamente cómo funciona este ejemplo.**

El programa está hecho para ejecutarse en la micro:bit y hace que dos píxeles de la pantalla parpadeen con diferente velocidad, crea una clase llamada Pixel que se encarga de encender y apagar un LED específico, dependiendo del tiempo que haya pasado. Hay dos píxeles, uno en la esquina superior izquierda (0, 0) que cambia cada segundo y otro en la esquina inferior derecha (4, 4) que cambia cada medio segundo. El método update() se encarga de revisar si ya pasó el tiempo que le corresponde a cada píxel para cambiar de estado, y si si, lo prende o lo apaga

**¿Cuáles son los estados en el programa?**

Init: cuando el píxel se inicializa por primera vez, se guarda el tiempo actual y se muestra el LED con el brillo inicial

WaitTimeout: cuando ya está esperando que pase el tiempo para volver a cambiar su estado (prendido o apagado)

**¿Cuáles son los eventos/inputs en el programa?**

El único evento que hace que todo funcione es el paso del tiempo. No hay botones ni sensores, solo se usa el tiempo que ha pasado desde que se activó el LED para saber si ya debe cambiar de estado

**¿Cuáles son las acciones en el programa?**

Dependen del estado

Init: se guarda el tiempo actual y se muestra el LED

WaitTimeout: si ya pasó el intervalo definido, se cambia el estado del LED (de apagado a encendido o al revés), se actualiza el tiempo y se muestra el nuevo estado en la pantalla.

### Actividad 2

```python

from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.estado = "rojo"
        self.inicio = utime.ticks_ms()
        self.mostrar_estado()

    def mostrar_estado(self):
        display.clear()
        if self.estado == "rojo":
            display.set_pixel(2, 0, 9)
        elif self.estado == "amarillo":
            display.set_pixel(2, 2, 9)
        elif self.estado == "verde":
            display.set_pixel(2, 4, 9)

    def actualizar(self):
        ahora = utime.ticks_ms()
        tiempo = utime.ticks_diff(ahora, self.inicio)

        if self.estado == "rojo" and tiempo > 3000:
            self.estado = "verde"
            self.inicio = utime.ticks_ms()
            self.mostrar_estado()

        elif self.estado == "verde" and tiempo > 3000:
            self.estado = "amarillo"
            self.inicio = utime.ticks_ms()
            self.mostrar_estado()

        elif self.estado == "amarillo" and tiempo > 1000:
            self.estado = "rojo"
            self.inicio = utime.ticks_ms()
            self.mostrar_estado()

mi_semaforo = Semaforo()

while True:
    mi_semaforo.actualizar()

```

**Estados:**

Rojo -> el LED rojo está encendido

Verde -> el LED verde está encendido

Amarillo -> el LED amarillo está encendido 

**Eventos:**

Como no hay interaccion del usuario los eventos que causan el cambio de estado son el paso del tiempo

Después de 3 segundos en rojo -> pasa a verde

Después de 3 segundos en verde -> pasa a amarillo

Después de 1 segundo en amarillo -> vuelve a rojo

**Acciones:**

- Apago la pantalla (display.clear()) cada vez que cambia el estado

- Enciendo solo el LED que corresponde a cada color

- Vuelvo a contar el tiempo desde cero cada vez que cambio de estado

### Actividad 3

**Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas**

Aunque el micro:bit no puede hacer tareas al mismo tiempo como un computador, este programa hace pareceer que sí lo hace porque usa una máquina de estados junto con el tiempo (utime.ticks_ms()) para controlar cuándo cambiar de imagen, sin detener el programa. no usamos sleep porque nos tiramos la concurrencia y si hacemos los fps caen y los usuarios no juegan, etc etc.

**Identifica los estados, eventos y acciones en el programa.**

**Estados:**

STATE_INIT -> el estado inicial

STATE_HAPPY -> se muestra la cara feliz.

STATE_SMILE -> se muestra la cara sonriente

STATE_SAD -> se muestra la carita triste.

**Eventos:**

- El tiempo que ha pasado desde que se entró a un estado

- La pulsación del botón A, que puede interrumpir el ciclo y forzar un cambio de imagen dependiendo de cuál esté en pantalla.

**Acciones:**

- Se muestra una imagen en la pantalla

- Se cambia al estado siguiente dependiendo del evento (tiempo o botón).

- Se ajusta el tiempo que debe durar cada imagen (intervalo).

**Describe y aplica al menos 3 vectores de prueba para el programa**

**Vector de prueba 1:**

Estado inicial: STATE_HAPPY

Evento: Presionar botón A antes de que pasen los 1500 ms

Resultado esperado: Mostrar la cara triste y cambiar a STATE_SAD

Resultado real: El cambio ocurrió de inmediato.

**Vector de prueba 2:**

Estado inicial: STATE_SMILE

Evento: Presionar botón A antes de que pasen los 1000 ms

Resultado esperado: Mostrar la cara feliz y volver a STATE_HAPPY

Resultado real: Se mostró la cara feliz al instante.

**Vector de prueba 3**

Estado inicial: STATE_SAD

Evento: Presionar botón A antes de que pasen los 2000 ms

Resultado esperado: Mostrar la cara sonriente y pasar a STATE_SMILE

Resultado real: Cambió correctamente.









