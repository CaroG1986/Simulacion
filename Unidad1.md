# Unidad 1: Aleatoriedad 🕷️

## Actividad 1

La aleatoriedad en el arte generativo

Reflexiones importantes: 


## Actividad 2

Analicemos juntos el código del ejemplo Example 0.1: A Traditional Random Walk del texto guía.

<img width="641" height="241" alt="image" src="https://github.com/user-attachments/assets/c01c2575-70ae-458e-8e47-a6d903c44186" />

## Actividad 3 

Analicemos juntos y detenidamente este ejemplo.
En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(100);
  
}

function draw() {
  walker.step();
  walker.show();
}

function keyPressed() {
  // Code to run.
}
class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    noStroke();
    let c = [175, random(100, 200), 220];
    fill(c);
    square(this.x, this.y,20);
  }

  step() {
    const choicex = floor(randomGaussian(0));
    const choicey = floor(random(2,4));
    if (choicex == 0) {
      this.x++;
    } else if (choicex == 1) {
      this.x--;
    } else if (choicey == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

<img width="658" height="247" alt="image" src="https://github.com/user-attachments/assets/eba1a4fd-aac3-4354-a649-75bd630fbb9c" />

## Actividad 4

Analicemos juntos y detenidamente este ejemplo.
Crea un nuevo sketch en p5.js que represente una distribución normal, pero visualizándola de manera diferente a la del ejemplo.

## Actividad 5
