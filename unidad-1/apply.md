# Unidad 1

## 🛠 Fase: Apply

## Actividad 05

En este ejercicio conecté el micro:bit con p5.js para que al presionar el botón A, un cuadrado cambie de color. El micro:bit está enviando por serial una A si el botón A está presionado, y una N si no y lo hace cada 100 milisegundos.

En p5.js, creamos una ventana con un botón que sirve para conectar el micro:bit al navegador. en la función draw(), el programa revisa si llegó algún mensaje por el puerto serial, si llega una A, pinta el cuadrado de rojo y si llega una N lo pinta de verde.

**Input:** Presionar o soltar el botón A del micro:bit.

**Proceso:** El micro:bit detecta el estado del botón y envía A o N por el puerto serial, p5.js recibe ese mensaje y cambia el color del cuadrado.

**Output:** El cuadrado cambia de color según el botón esté presionado (rojo) o no (verde)

## Actividad 06

https://editor.p5js.org/antonellavides/sketches/asvYrOsLE

***p5js**

``` js
let port;
let connectBtn;
let x = 200;

function setup() {
  createCanvas(400, 400);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 350);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.availableBytes() > 0) {
    let data = port.read(1);
    if (data === "A") {
      x -= 10;
    } else if (data === "B") {
      x += 10;
    }
  }

  x = constrain(x, 25, width - 25);
  fill("blue");
  ellipse(x, height / 2, 50, 50);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}
```

**microbit**

``` python
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.was_pressed():
        uart.write('A')
    if button_b.was_pressed():
        uart.write('B')
```

#### Paso a paso

- Crear la variable del puerto (port) para comunicarme con el micro:bit y también una variable x para guardar la posición horizontal del círculo
- createCanvas dibuja el espacio donde va el círculo
- createSerial() crea el objeto para la conexión serial
- Hago un botón que me deja conectar y desconectar el micro:bit
- draw() se repite muchas veces por segundo para que la pagina se vaya actualizando para redibujar los fotogramas del circulo
- Si es A muevo el círculo a la izquierda y si es B lo muevo a la derecha

**uart:** es el módulo que permite al micro:bit comunicarse por puerto serial USB

**.init():** inicializa la comunicación

**baudrate=115200:** define la velocidad a la que se envían los datos en bits por segundo





