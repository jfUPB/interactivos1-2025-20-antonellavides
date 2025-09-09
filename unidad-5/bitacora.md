
# Evidencias de la unidad 5

### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

El micro:bit y el sketch se comunican a través del puerto serial (UART). El micro:bit envía constantemente información a 115200 baudios, y en el navegador el sketch usa la librería p5.webserial.js para conectarse al puerto, recibir esos datos en tiempo real y utilizarlos para dibujar en la pantalla.

El micro:bit envía cuatro valores separados por comas:

- El valor del acelerómetro en el eje X.

- El valor del acelerómetro en el eje Y.

- El estado del botón A (True o False).

- El estado del botón B (True o False).

### ¿Cómo es la estructura del protocolo ASCII usado?

X → número entero con el valor de aceleración en X.

Y → número entero con el valor de aceleración en Y.

A → palabra “True” o “False” indicando si el botón A está presionado.

B → palabra “True” o “False” indicando si el botón B está presionado.

\n → salto de línea que marca el final del mensaje.

### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.

```js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```

- Lee la línea completa del puerto serial.

- Divide los datos en 4 valores.

- Convierte los datos X y Y en coordenadas de la pantalla.

- Interpreta los estados de los botones A y B como true o false.

### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

El sketch compara el estado actual del botón con el estado anterior. Cuando el botón A pasa de false a true, se genera el evento “A pressed” y se cambian parámetros del dibujo y cuando el botón B pasa de true a false, se genera el evento “B released” y se cambia el color. Esto se controla con la función updateButtonStates(), que revisa si hubo cambios en los botones y ejecuta las acciones correspondientes.

### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.





