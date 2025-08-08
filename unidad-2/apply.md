# Unidad 2


## 🛠 Fase: Apply

### Actividad 08

1. Describe el concepto de tu obra generativa.

Estas controlando un coete lanzado por Elon el cual tiene la mision de llegar a marte, entonces necesitas esquivar todos los asteroides, el coete se contolara con mocion 101 en el eje y, los asteroides iran del derecha a izquierda con una aceleracion aleatoria mas en el eje x que en y para que no sea tan dificil de esquivar. 
  
2. ¿Cómo piensas aplicar el marco MOTION 101 y por qué?

   En los asteroides, para que puedan ser el obtaculo del cohete tipo loop infinito sin consumir tantos recursos de la memoria y tener mas control de ellos.
  
3. ¿Qué algoritmo de aceleración vas a utilizar? ¿Por qué?

 * aceleracion por mouse para que el piloto pueda controlar el cohete
 * aceleracion aleatoria para que los asteriodes no se muevan de forma aburrida.

  
4.  El contenido generado debe ser interactivo. Puedes utilizar mouse, teclado, cámara, micrófono, etc, para variar los parámetros del algoritmo en tiempo real.
5.  El código de la aplicación.

`sketch.js`
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com
let vidas = 3;
let cohete;
let movers = [];

function setup() {
  createCanvas(640, 240);
  
  cohete = new Cohete();
  
  for (let i = 0; i < 5; i++) {
    movers.push(new Mover());
  }
}

function draw() {
  background(10,10,100);

   for (let mover of movers) {
    mover.update();
    mover.checkEdges();
    mover.show();
  }
  
  cohete.update();
  cohete.show();
  
  for (let mover of movers) {
  let d = dist(cohete.position.x, cohete.position.y, mover.position.x, mover.position.y);
  if (d < 15 + 15) {
    vidas--;
    
    // Reposicionar el asteroide para que no reste varias vidas de una
    mover.position = createVector(random(width), random(height));
    
  }  
}
  
  fill(255);
textSize(24);
text("Vidas: " + vidas, 20, 30);
  
  if (vidas <= 0) {
  noLoop(); // Detiene draw()
  fill(255, 0, 0);
  textSize(32);
  text("¡Game Over!", width / 2 - 80, height / 2);
}
 }
```

`mover.js`
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

class Mover {
  constructor() {
    this.position = createVector( 640, random(height));
    this.velocity = createVector(random(-3,-5), 0);
  }

  update() {
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(1);
    fill(255,255,127);
    circle(this.position.x, this.position.y, 20);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.position.x = 0;
    } else if (this.position.x < 0) {
      this.position.x = width;
      this.position.y = random(height);
    }
  }
}

class Cohete {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector();
    this.acceleration = createVector();
    this.topspeed = 4;
  }

  update() {
    let mouse = createVector(80, mouseY);
    let dir = p5.Vector.sub(mouse, this.position);
    dir.setMag(0.1);
    this.acceleration = dir;

    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topspeed);
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(255);
    rect (100, this.position.y, 40,20);
  }
}

```
  
7.  Un enlace al proyecto en el editor de p5.js.

(https://editor.p5js.org/nicolasparra2024/sketches/sujBKMaeJ)
  
8.  Una captura de pantalla representativa de tu pieza de arte generativo.

<img width="630" height="231" alt="image" src="https://github.com/user-attachments/assets/d6d8a457-999d-4a0a-8f84-190c97594b55" />


