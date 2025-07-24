# Unidad 1

## 🛠 Fase: Apply

### Actividad 08
Creación de obra generativa

Vas a crear una obra generativa interactiva en tiempo real utilizando los conceptos de aleatoriedad que has aprendido en esta unidad.
Tu obra debe:

Usar al menos tres conceptos estudiados en esta unidad COMBINADOS de manera creativa y coherente.
Tu obra de ser interactiva y generativa en tiempo real. Puedes usar el mouse, el teclado o cualquier otro sensor de entrada para interactuar con la obra.
📤 Bitácora

Reporta en tu bitácora lo siguiente:

1. Un texto donde expliques el concepto de obra generativa.

con esta unidad quiero poner a prueba  si puedo convinar el ruido de perlin con los colres, para que haga una tansiciones suaves, tambien sera el primer prototipo para crear un sistemas de particulas que se expanda hacia los bordes de la pantalla. usare un ramndom, en los colores de las particulas, un noise perlin en el fondo, y generare particulas al dar click con el raton.

*variables globales*
``` js
let noiseOffset = 0;
let particles = [];
```

*function setup()*
``` js
  createCanvas(600, 240);
  generateParticles(); // Genera partículas al inicio
  // Elegimos un color aleatorio al inicio, no lo coloque en la funcion draw porque hace que las particulas parpadeen y hace que se vea poco armonico
  particleColor = color(random(255), random(255), random(255), 255);
```

*funcion draw()  "agregar para el cambio de color del canvas"*
``` js
function draw() {

//se agregan variables para configurar el noise en cada color RGB.
  let r = noise(noiseOffset) * 255;
  let g = noise(noiseOffset + 10) * 255; 
  let b = noise(noiseOffset + 20) * 255;

 // se llaman esas variables al color del fondo. 
  background(r,g,b);
...
...
...
//esta parte es la que hace toda la magia del Perlin recomiendo dejarlo a lo ultimo de la funcion draw
  noiseOffset += 0.01;
}
```
*function generateParticles()* 
``` js
  particles = []; // Vacía el arreglo  
  for (let i = 0; i < 100; i++) {
    particles.push(new Particle()); //crea 100 particulas 
  }
```

*function mousePressed()* 
``` js
 generateParticles(); // acciona la funcion generar particulas
  particleColor = color(random(255), random(255), random(255), 255); // modifica los valores establecidos en el color de las particulas por otros valores aleatorios
  }
```
*update()* : ¿que hace update?  se encarga de actualizar la posición de un objeto (por ejemplo, una partícula) con base en su velocidad.
``` js
 this.pos.add(this.vel);
```
segun chat gpt `this.pos.add(this.vel);`

`this.pos` → es un vector que representa la posición del objeto (como un punto (x, y)).

`this.vel` → es otro vector, pero que representa la velocidad o dirección y magnitud del movimiento.

`.add()` → es una función de p5.js para sumar vectores.


*display()* : ¿que hace display? dislay manda la informacion que tiene dento a la funcion  DRAW, esta le indica las caracteristicas que deben tener las particulas 
``` js
    fill(particleColor);
    noStroke();
    ellipse(this.pos.x, this.pos.y, 8, 8);
```


2. Copia el código en tu bitácora.

``` js
let particles = [];
let noiseOffset = 0;

function setup() {
  createCanvas(600, 240);
  generateParticles(); // Genera partículas al inicio
  // Elegimos un color aleatorio al inicio
  particleColor = color(random(255), random(255), random(255), 255);
}

function draw() {
  
  let r = noise(noiseOffset) * 255;
  let g = noise(noiseOffset + 10) * 255; 
  let b = noise(noiseOffset + 20) * 255;

  
  background(r,g,b);

  for (let p of particles) {
    p.update();
    p.display();
  }
  noiseOffset += 0.01;
}

// Esta función genera 100 partículas desde el centro
function generateParticles() {
  particles = []; // Vacía el arreglo
  for (let i = 0; i < 100; i++) {
    particles.push(new Particle());
  }
}

// Al hacer clic, se reinician las partículas
function mousePressed() {
  generateParticles();
  particleColor = color(random(255), random(255), random(255), 255);
}

// Clase Partícula
class Particle {
  constructor() {
    this.pos = createVector(width / 2, height / 2);

    let angle = random(TWO_PI);
    let speed = random(1, 3);
    this.vel = p5.Vector.fromAngle(angle).mult(speed);
  }

  update() {
    this.pos.add(this.vel);
  }

  display() {
    fill(particleColor);
    noStroke();
    ellipse(this.pos.x, this.pos.y, 8, 8);
  }
}

```
Coloca en enlace a tu sketch en p5.js en tu bitácora.

[Enlace de la Apply](https://editor.p5js.org/nicolasparra2024/sketches/EacQ1BuK4)
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
