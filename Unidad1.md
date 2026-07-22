# Unidad 1: Aleatoriedad 🕷️

## Actividad 01

> La aleatoriedad en el arte generativo

Reflexiones importantes: 

- El arte siempre ha estado ligado de una manera u otra a la ciencia, en la era actual de una forma más evidente, sin embargo en la teoria de los principios básicos del arte se encuentran ligados a conceptos de la matematica, geometria, física, etc. Por ejemplo: la perspectiva, la composición, la luz, las proporciones, entre otros.
- El arte generativo sule ser muy abstracto, ya que busca como la mayoria del arte moderno espresar algo más allá de lo qiue ya es visible, en este caso la fusión de la tecnología con el arte.
- Algo interesante del arte generativo es que al juntarse con la aleatoriedad le abre la puerta a los artistas a facilitar su trabajo, ya que pueden usar la misma "semilla" o código base y aun así generar obras complatamente distintas 

## Actividad 02

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

## Actividad 03 

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

## Actividad 04

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

## Actividad 05

> Analicemos juntos y detenidamente el concepto de Lévy flight.

Por lo que comprendi el Levy flight es como un salto que se hace en los datos para que haya algo de variedad, en este caso se explicaba como una forma de recorrer menos vecxes el mismo punto.

> Ahora vas a:

> Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.

Hice una prueba con la caminata pero no vi en ningun momento el salto

```js
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
    let c = [175, 20, random(100, 200)];
    fill(c);
    square(this.x, this.y,20);
  }

  step() {
    const choicex = floor(randomGaussian(1));
    const choicey = floor(random(2,4));
    if (choicex >0.1|| choicex <2) {
      this.x= random(330, 310);
    } else if (choicex < 0.1) {
      this.x= random(-100, 100);
    } else if (choicey == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

<img width="805" height="305" alt="image" src="https://github.com/user-attachments/assets/8c5a70ae-3df3-463a-87ca-9eb6e5f55fd9" />

Me imagino que es porque al final del dia sigue teniendo muy poca probabilidad, pero luego investigue y resulta que mis errores fueron dos: 
- en el código "floor(randomGaussian(1))" el floor lo que hace es redondear a números enteros, así que en ningun momento iba a obtener un número decimal como queria
- mi idea de Levy fly estaba equivocada, la idea era que cuando diera el gran paso luego siguiera dando pasos pequeños

Por ende le pregunte a una IA que podía hacer para ese cambio y me recomendo cambiar la función step de la siguiente manera: 

```js
  step() {
 // 90% de probabilidad: paso pequeño (difusión normal cerca del centro)
 // 10% de probabilidad: SALTO GRANDE a los extremos
 if (random(1) < 0.9) {
 // Paso pequeño con distribución normal (centrado en la posición actual)
 this.x += randomGaussian(0, 5); // media 0, desviación 5 -> pasos de ~1-10px
 } else {
 // ¡SALTO! a algún extremo, izquierda o derecha
 if (random(1) < 0.3) {
 this.x = random(0, 50); // salta a la izquierda
 } else {
 this.x = random(width - 50, width); // salta a la derecha
 }
 }
```

Básicamente es muy parecido al ejemplo inicial de la caminata pero ahora juega con las probabilidades para que sean más extremas, y como resultado visual obtuve lo siguiente (que según yo se parece más a lo que necesitaba) :

<img width="801" height="296" alt="image" src="https://github.com/user-attachments/assets/7f478425-6049-42c8-a9a5-537f50399b2b" />

> Explica por qué usaste esta técnica y qué resultados esperabas obtener.

Bueno, creo que en el punto anterior explique esto a gran profundidad, pero igual para aclara yo esperaba en realidad que saltara y regresara a la media original (el centro), pero luego de buscar más a fondo comprendi mucho mejor que se referia a que no importa donde vaya el salto grande, los pequeños pasos iran a su alrededor.

Y la tecnica que use para esto fue básicamente el desplazamiento horizontal en la caminata aleatoria, con un poquito de vertical para que sea vea mejor.

## Actividad 06

> Analicemos junto el concepto de ruido Perlin analizando la figura 0.4: “A graph of Perlin noise values over time (left) and of random noise values over time (right)”.

Según lo que entendí en estas figuras, el ruido de Perlin se trata de cambios más leves, en cambio el ruido random real es básicamente caos total. 

> Una vez has entendido el concepto de ruido Perlin, vas a pensar en una nueva manera de visualizarlo.

> Crea un nuevo sketch en p5.js donde los visualices.

Mi sketch:

```js
class Box {
constructor(x,y,z,scl,speed,noiseOffset){
  this.pos= createVector(x,y,z);
  this.noiseOffset = noiseOffset;
  this.scl=scl;
  this.speed= speed;
  this.t=0;
 }  

  update (){
  let n = noise(
 this.noiseOffset.x + this.t * this.speed,
 this.noiseOffset.y + this.t * this.speed,
 this.t * this.speed * 0.5
 ); 
    this.pos.z =map(n, 0, 1, -this.scl, this.scl);
    this.t += 0.05;
  }
  
  display() {
    noStroke();
    let r= map(this.pos.z, -this.scl, this.scl, 0, 255);
    fill(r,0,0);
    push();
    translate (this.pos.x,this.pos.y,this.pos.z);
    box(size);
    pop();
  }
}

let boxes= [];
let size = 10;let cols,rows;
let margin= 50; let scl=50;
let speed= 0.05;

function setup() {
  createCanvas(500, 500,WEBGL);
  frameRate(30);
  cols= (width-margin*2)/size;
  rows= (height-margin*2)/size;
   noiseSeed(random(1000));

  for (let i=0;i<cols;i++){
    boxes[i]=[];
    for ( let j=0; j< rows;j++){
      let x = -width/2+ margin +size/2+i*size;
      let y =-height/2+ margin+ size/2+ j*size;
      let z = 0;
      let noiseOffset = createVector(i * 0.1, j * 0.1, 0);
      boxes[i][j]= new Box(x, y, z, scl, speed, noiseOffset);
    }
  }
}

function draw() {
  background(0);
  orbitControl();

  for (let i=0; i<cols;i++){
    for(let j=0; j<rows; j++){
    //  boxes [i][j].angle= m;
      boxes[i][j].update();
     boxes [i][j].display(); 
    }
  }
  
}
```
Se ve de la siguiente manera:

<img width="622" height="617" alt="image" src="https://github.com/user-attachments/assets/d98060f4-314a-441a-843b-4c10706f32c3" />

<img width="556" height="610" alt="image" src="https://github.com/user-attachments/assets/408131a1-e942-408f-9ad8-b197411583a1" />


**En la imagen no se ve pero se mueve con ruido de Perlin**

> Explica por qué lo visualizaste de esa manera y qué resultados esperabas obtener.

Yo lo visualize de esta manera porque al ver la gráfica que se me presentó en la comparación pensé en la textura que me trasmitan los dos, senti que el ruido de Perlin era rugoso mientras que el ruido "normal" era puntudo, de alguna forma quería transmitir esa sensación y crei que sería más fácil demostrarla con 3D.

## Atividad 07

Para este trabajo busque temas de festivales del mundo que se relacionaran con tecnología pero no me gusto ninguno, entonces decidí ir por colombia Moda, el tema de este año es tejido infinito, que siento que se relaciona con la idea de "La incertidumbre no es ausencia de reglas" ya que a pesar de la incertidumbre del infinito de cierta forma se teje o forma con un conjunto de reglas y conceptos, además en el tema también se presenta la siguiente idea: Un hilo que se entrelaza con los demás para tejer historias, conectar mundos y transformar realidades. 

Mi idea entonces que el usuario controle o maneje el hilo que conecta  

let particles = [];
let levyAlpha = 1.5;

function setup() {
 createCanvas(windowWidth, windowHeight);
 background(10);
 strokeWeight(1.5);
}

function draw() {
 // Desvanecer ligeramente el fondo para efecto de "tejido infinito"
 background(10, 5);

 // Dejar una partícula nueva en la posición del mouse
 if (frameCount % 3 === 0) {
 particles.push(new Particle(mouseX, mouseY));
 }

 // Conectar y dibujar
 for (let p of particles) {
 p.connect(particles);
 p.show();
 }

 // Limitar cantidad para no colgar el navegador
 if (particles.length > 300) {
 particles.splice(0, 50);
 }
}

class Particle {
 constructor(x, y) {
 this.pos = createVector(x, y);
 this.connections = [];
 this.color = color(
 200 + random(55),
 150 + random(105),
 200 + random(55),
 80
 );
 }

 connect(others) {
 this.connections = []; // reiniciar cada frame

 // Conexiones cortas con vecinos cercanos (trama densa)
 for (let other of others) {
 if (other === this) continue;
 let d = dist(this.pos.x, this.pos.y, other.pos.x, other.pos.y);
 if (d < 80 && random() < 0.25) {
 this.connections.push(other);
 }
 }

 // Levy flight: salto largo ocasional
 if (random() < 0.015) {
 let target = random(others);
 if (target && target!== this) {
 // Dirección aleatoria con distancia Levy
 let step = pow(random(), -1 / levyAlpha) * 60;
 let angle = random(TWO_PI);
 let farX = this.pos.x + cos(angle) * step;
 let farY = this.pos.y + sin(angle) * step;

 // Encontrar la partícula más cercana a ese punto lejano
 let farTarget = null;
 let minDist = Infinity;
 for (let o of others) {
 if (o === this) continue;
 let d = dist(farX, farY, o.pos.x, o.pos.y);
 if (d < minDist) {
 minDist = d;
 farTarget = o;
 }
 }
 if (farTarget) {
 this.connections.push(farTarget);
 }
 }
 }
 }

 show() {
 stroke(this.color);
 for (let c of this.connections) {
 line(this.pos.x, this.pos.y, c.pos.x, c.pos.y);
 }
 }
}

function keyPressed() {
 // Tecla R para reiniciar
 if (key === 'r' || key === 'R') {
 particles = [];
 background(10);
 }

 // Flecha arriba/abajo para ajustar alpha del Levy
 if (keyCode === UP_ARROW) {
 levyAlpha = min(levyAlpha + 0.1, 2.5);
 print('Levy alpha:', levyAlpha);
 }
 if (keyCode === DOWN_ARROW) {
 levyAlpha = max(levyAlpha - 0.1, 1.1);
 print('Levy alpha:', levyAlpha);
 }
}
