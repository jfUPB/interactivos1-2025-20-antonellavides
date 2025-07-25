# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

En este ejercicio conecté el micro:bit con p5.js para que al presionar el botón A, un cuadrado cambie de color. El micro:bit está enviando por serial una "A" si el botón A está presionado, y una "N" si no y lo hace cada 100 milisegundos.

En p5.js, creamos una ventana con un botón que sirve para conectar el micro:bit al navegador. en la función draw(), el programa revisa si llegó algún mensaje por el puerto serial, si llega una "A", pinta el cuadrado de rojo y si llega una "N" lo pinta de verde.

**Input:** Presionar o soltar el botón A del micro:bit.

**Proceso:** El micro:bit detecta el estado del botón y envía "A" o "N" por el puerto serial, p5.js recibe ese mensaje y cambia el color del cuadrado.

**Output:** El cuadrado cambia de color según el botón esté presionado (rojo) o no (verde)



