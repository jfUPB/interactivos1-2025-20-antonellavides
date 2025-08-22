# Unidad 3


## 🛠 Fase: Apply

### Actividad 06

```js
// Estados posibles
let estado = "esperando"; 
let tiempo = 0; 
let tiempoMax = 300; // duración de la cuenta regresiva

function setup() {
  createCanvas(400, 200);
  textAlign(CENTER, CENTER);
  textSize(20);
}

function draw() {
  background(220);

  if (estado === "esperando") {
    text("Presiona ESPACIO para iniciar", width/2, height/2);

  } else if (estado === "activada") {
    text("Bomba activada!", width/2, height/2 - 30);
    text("Tiempo: " + int((tiempoMax - tiempo) / 60), width/2, height/2 + 20);

    tiempo++;
    if (tiempo > tiempoMax) {
      estado = "exploto";
    }

  } else if (estado === "exploto") {
    text("BOOM ", width/2, height/2);
  }
}

function keyPressed() {
  if (estado === "esperando" && key === " ") {
    estado = "activada";
    tiempo = 0;
  }
}

```

### Actividad 06

```js
let estado = "esperando"; 
let tiempo = 0; 
let tiempoMax = 300; 

// Objeto para la comunicación serial
let serial;
let ultimoDato = "";

function setup() {
  createCanvas(400, 200);
  textAlign(CENTER, CENTER);
  textSize(20);

  // Configurar serial
  serial = new p5.SerialPort();
  serial.list();
  serial.open(" ");
  serial.on("data", recibirDatos);
}

function draw() {
  background(220);

  if (estado === "esperando") {
    text("Presiona ESPACIO o Botón A", width/2, height/2);

  } else if (estado === "activada") {
    text("Bomba activada!", width/2, height/2 - 30);
    text("Tiempo: " + int((tiempoMax - tiempo) / 60), width/2, height/2 + 20);

    tiempo++;
    if (tiempo > tiempoMax) {
      estado = "exploto";
    }

  } else if (estado === "exploto") {
    text("BOOM", width/2, height/2);
  } else if (estado === "desactivada") {
    text("Bomba desactivada", width/2, height/2);
  }
}

function keyPressed() {
  if (estado === "esperando" && key === " ") {
    estado = "activada";
    tiempo = 0;
  }
}

// Función para leer lo que envía el micro:bit
function recibirDatos() {
  let dato = serial.readLine().trim();
  if (dato.length > 0) {
    ultimoDato = dato;

    if (estado === "esperando" && dato === "A") {
      estado = "activada";
      tiempo = 0;
    } else if (estado === "activada" && dato === "B") {
      estado = "desactivada";
    }
  }
}

```

<iframe src="https://editor.p5js.org/antonellavides/full/8_96lB9w_"></iframe>

```python
from microbit import *

while True:
    if button_a.is_pressed():
        uart.write("A\n")
    if button_b.is_pressed():
        uart.write("B\n")
```










