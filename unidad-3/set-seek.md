# Unidad 3

## 🔎 Fase: Set + Seek

## Actividad 09
Inventa tres obras generativas interactivas, uno para cada una de las siguientes fuerzas:




* Fricción.
* Resistencia del aire y de fluidos.

<img width="606" height="411" alt="image" src="https://github.com/user-attachments/assets/a53d0ddc-bde3-41e4-ac25-c68235d5033a" />

mover.js
```js
class Mover {
  constructor() {
    this.mass = 1;
    this.position = createVector(width / 2, 30);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    stroke(0);
    strokeWeight(2);
    fill(127, 127);
    ellipse(this.position.x, this.position.y, 48, 48);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.position.x = width;
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1;
      this.position.x = 0;
    }
    if (this.position.y > height) {
      this.velocity.y *= -1;
      this.position.y = height;
    }
  }
}


function drawHoops() {
  fill(255, 100, 100);
  noStroke();

  // Canasta izquierda (mitad vertical)
  rect(0, height / 2 - 40, 90, 20);

  // Canasta derecha (mitad vertical)
  rect(width - 90, height / 2 - 40, 100, 20);
}

```

sketch.js
```js
let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover();
}

function draw() {
  background(220);

  // Aplicar gravedad constante
  let gravity = createVector(0, 0.2);
  mover.applyForce(gravity);

  // Si el mouse está presionado, aplicar viento
  if (mouseIsPressed) {
    let wind;
    if (mouseX > mover.position.x) {
      wind = createVector(-0.5, 0); // empuja a la izquierda
    } else {
      wind = createVector(0.5, 0); // empuja a la derecha
    }
    mover.applyForce(wind);
  }

  mover.update();
  mover.checkEdges();
  mover.display();
  drawHoops();
}

```
link del experimento: (https://editor.p5js.org/nicolasparra2024/sketches/jwADJu0qE)

* Explica cómo modelaste cada fuerza.

  Se aplico 101 y tambien una funcion de MouseIspressed que rastrea la posicion del mouse y aplica una fuerza contraria en el balon.
  
* Atracción gravitacional.
<img width="504" height="228" alt="image" src="https://github.com/user-attachments/assets/a4a595cf-240d-4e70-a741-07dbff254d97" />

mover.js
```js

class Body {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 10;
    this.r = sqrt(this.mass) * 2;
  }
  
  attract(body) {
    let force = p5.Vector.sub(this.position, body.position);
    let d = constrain(force.mag(), 25, 25);

    // Si el mouse está presionado aumentamos la gravedad
    let G = mouseIsPressed ? 5 : 1;  // <-- aquí cambiamos la fuerza (5x más fuerte al hacer click)

    let strength = (G * (this.mass * body.mass)) / (d * d);
    force.setMag(strength);
    body.applyForce(force);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.set(0, 0);
  }

  show() {
    stroke(250);
    strokeWeight(2);
    fill(250, 500);
    circle(this.position.x, this.position.y, this.r * 4);
  }
}

```
sketch.js
```js

let bodyA;
let bodyB;

let G = 1;

function setup() {
  createCanvas(640, 250);
  bodyA = new Body(320, 40);
  bodyB = new Body(320, 200);
  bodyA.velocity = createVector(1, 0);
  bodyB.velocity = createVector(-1, 0);
}

function draw() {
  background(25,0,0,5);

  bodyA.attract(bodyB);
  bodyB.attract(bodyA);

  bodyA.update();
  bodyA.show();
  bodyB.update();
  bodyB.show();
}
```
link: (https://editor.p5js.org/nicolasparra2024/sketches/CNrxCSMM1)
* Explica cómo modelaste cada fuerza.

  
* Conceptualmente cómo se relaciona la fuerza con la obra generativa.
* Copia el enlace a tu ejemplo en p5.js.


  
* Copia el código.
* Captura una imagen representativa de tu ejemplo.



