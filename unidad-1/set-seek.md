# Unidad 1

## 🔎 Fase: Set + Seek

## Actividad 01

#### ¿Qué es un sistema físico interactivo?

Son sistemas que mezclan elementos fisicos y software para interactuar con estímulos del entorno o personas

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Expresar la creatividad de diferentes maneras a traves de las diferentes posibilidades que ofrecen los sistemas físicos interactivos es algo único que enriquece mucho un perfil profesional. Mi enfoque va mucho al arte y a poder expresarme libre y espontaneamente así que pienso que esta nueva forma que se nos presento hoy va muy de acuerdo en lo que espero en mi vida profesional y es una gran herramienta.

## Actividad 02

#### ¿Qué es el diseño/arte generativo?

se refiere a cualquier practica artistica en la que el artista utiliza un sistema (maquina programada, computador, seres humanos) el sistema se define con un conjunto de reglas y se utilizan sistemas con cierto grado de autonomía

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

La verdad no me llama la atención el arte generativo para lo que yo pienso de mi vida profesional pero reconozco que al automatizar y optimizar algunos procesos se pueden llegar a lograr resultados muy buenos y llevar a otro nivel el arte y la creatividad.

## Actividad 03

#### Identificar los inputs, outputs y el proceso.

En este sistema físico interactivo, usé un micro:bit y un programa en p5.js. Los inputs son cuando presiono el botón A, B o agito el micro:bit, y también cuando doy click en el botón “Send Love” en la pantalla. El proceso es que el micro:bit y el computador se comunican por puerto serial y envían letras según lo que hago. Los outputs son que en la pantalla cambia el color del círculo (según si se recibe una A, B o C), y el micro:bit muestra un corazón y una carita feliz cuando recibe la letra ‘h’.

## Actividad 04

Vamos a crear un programa en p5.js que genere patrones visuales aleatorios utilizando funciones matemáticas simples (ej. random(), sin(), cos()). Para esta actividade no es necesario usar el micro:bit, solo p5.js.

``` js
function setup() {
  createCanvas(400, 400);
  background(20);
  noLoop();
}

function draw() {
  translate(width / 2, height / 2);
  noStroke();
  for (let i = 0; i < 500; i++) {
    let angle = random(TWO_PI);
    let radius = random(20, 180);
    let x = cos(angle) * radius;
    let y = sin(angle) * radius;
    fill(random(100, 255), random(100, 255), random(100, 255), 150);
    ellipse(x, y, random(5, 15));
  }
}

```


<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/377fbb7b-9671-41f6-91f6-352cd6463057" />


### Paso a Paso no olv para racz

#### 1. setup()

- createCanvas(400, 400) -> Crea una pantalla de 400 x 400 píxeles

- background(20); -> Pone un fondo oscuro (20 es casi negro

- noLoop(); -> Hace que el dibujo solo se genere una vez

#### 2. draw()

- translate(width / 2, height / 2); -> Mueve el punto (0,0) al centro del canvas

- noStroke(); -> Quita los bordes de los círculos

#### 3. for (let i = 0; i < 500; i++) se repite 500 veces para crear muchos círculos

- let angle = random(TWO_PI); -> Escoge un ángulo aleatorio (de 0 a 2π, o sea 360 grados)

- let radius = random(20, 180); -> Escoge una distancia aleatoria desde el centro

- let x = cos(angle) * radius; -> Calcula la posición en X usando trigonometría

- let y = sin(angle) * radius; -> Calcula la posición en Y

fill(random(100, 255), random(100, 255), random(100, 255), 150); -> Color aleatorio con algo de transparencia

ellipse(x, y, random(5, 15)); -> Dibuja un círculo con posición y tamaño aleatorio









