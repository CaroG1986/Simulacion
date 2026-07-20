# Unidad 1: Aleatoriedad 🕷️

## Actividad 1

> La aleatoriedad en el arte generativo

Reflexiones importantes: 

- El arte siempre ha estado ligado de una manera u otra a la ciencia, en la era actual de una forma más evidente, sin embargo en la teoria de los principios básicos del arte se encuentran ligados a conceptos de la matematica, geometria, física, etc. Por ejemplo: la perspectiva, la composición, la luz, las proporciones, entre otros.
- El arte generativo sule ser muy abstracto, ya que busca como la mayoria del arte moderno espresar algo más allá de lo qiue ya es visible, en este caso la fusión de la tecnología con el arte.
- Algo interesante del arte generativo es que al juntarse con la aleatoriedad le abre la puerta a los artistas a facilitar su trabajo, ya que pueden usar la misma "semilla" o código base y aun así generar obras complatamente distintas 

## Actividad 2

> Analicemos juntos el código del ejemplo Example 0.1: A Traditional Random Walk del texto guía.

El ejemplo que se muestra de la caminata aleatoria usa la aleatoriedad (valga la redundancia) para que el punto se dibuje en distintas direcciones, para desglodarlo más funciona así:

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;
```

Aqui en primer lugar se instancia al objeto Walker como una variable global para poder utilizarla durante todo el código.

```js

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}
```

Esta es la primera función que se implementa en el código, todo lo que esta aquí solo ocurre una vez. 

En este caso se crea un canvas, se crea un objeto tipo walker y finalmente se pinta el canvas de un color

```js 
function draw() {
  walker.step();
  walker.show();
}
```

Esta función si se repite varias veces y en esta se llama el método step y show del walker, que podrían no hacerse como método de una clase pero este sistema permite una mejor adaptavilidad y trabajo en equipo
```js

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }
```

La clase walker con sus atributos, aqui se indica que debe iniciar en el centro del canvas

```js

  show() {
    stroke(0);
    point(this.x, this.y);
  }
```

Este es el método encargado de lo que visualizamos, en este caso el punto que se mueve.

```js

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

Para finalizar vemos el método de step que es el encargado de la caminata aleatoria y de lo "matematico" donde se escoge un número random entre 0 y 4 y segúin la elección será la dirección.

<img width="806" height="362" alt="image" src="https://github.com/user-attachments/assets/3d6a235f-8f47-4b5f-b696-a5abbb4e35b2" />

> Foto de como se ve el ejemplo

<img width="641" height="241" alt="image" src="https://github.com/user-attachments/assets/c01c2575-70ae-458e-8e47-a6d903c44186" />

> Ejemplo con modificaciones propias en la apariencia

## Actividad 3 

> Analicemos juntos y detenidamente este ejemplo.

Ya esta analizado en el punto anterior.

>En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.

Una distribución uniforme es cuando se tiene la misma probabilidad para cualquier evento o resultado, en cambio la distribución no uniforme es cuando la distibución se concentra alrededor de una media.

>Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.

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

Para esto use randomGaussian que toma valores más parecidos al de la derecha

<img width="658" height="247" alt="image" src="https://github.com/user-attachments/assets/eba1a4fd-aac3-4354-a649-75bd630fbb9c" />

## Actividad 4

Analicemos juntos y detenidamente este ejemplo.
Crea un nuevo sketch en p5.js que represente una distribución normal, pero visualizándola de manera diferente a la del ejemplo.

Yo lo hice como un "abanico de luz" por así decirlo, donde se puede ver la mayor concentración en el centro el abanico usando la distibución normal

```js
function setup() {
  createCanvas(640, 400);
  background(0);
}

function draw() {
  let x = randomGaussian(360, 180);
   let y = 0;
  let c = [random(0,175), random(0, 200), random(100,220),100];
  stroke (c);
  strokeWeight(3);
  line (width/2,height,x,y);  
}
```

> El código es muy simple pero cumple la función de mostrar gráficamente esta distribución y se ve algo así: 

<img width="831" height="540" alt="image" src="https://github.com/user-attachments/assets/0463da61-682f-4cba-9ba7-1a60dd63d5c5" />

## Actividad 5
