# Evidencias de la unidad 5

## actividad 2

* Captura de pantallas de cada una de las simulaciones con las imágenes que más te gusten como resultado de la ejecución de cada una de las simulaciones.

### Ejercicio 1

1. las particulas se generan desde el mouse.

2. En este primer ejemplo las particulas se crean por medio de una matriz la cual lee la matriz de atras hacia delante, esto para que no cause error a la hora de iterar(recorrer la matriz), para modificar una matriz hay que tener encuanta la funcion splice y lo que hace cada uno de sus parametros `` array.splice(punto de partida del array, cantidad de elemtos que vas a eliminas, agregar item1,agregar item2, ...); ``.
3.codigo Fuente.

  ```js
 let particles = [];

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(255);

  // Agregar una partícula en la posición del mouse
  particles.push(new Particle(mouseX, mouseY));

  // Recorremos el array de partículas
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.run();
    if (p.isDead()) {
      particles.splice(i, 1); // eliminar partículas muertas
    }
  }
}
  ```
4. [link del ejercicio modificado](https://editor.p5js.org/natureofcode/sketches/-xTbGZMim)

### Ejercicio 2
1. Que con cada click las particulas cabien aleatoriamente (polimorfismo).

2. En este segundo ejemplo obsevamos que en la ventana o codigo de particulas el tiempo de vidad esta dictado por un contador llamado tiempo de vida el cual va disminuyendo con el paso del y cuando sea menor que 0 se borra la particula.

 ```js
  class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;

    // Forma aleatoria: "circle", "square" o "triangle"
    let r = int(random(3));
    if (r === 0) this.shape = "circle";
    else if (r === 1) this.shape = "square";
    else this.shape = "triangle";
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);

    if (this.shape === "circle") {
      circle(this.position.x, this.position.y, 12);
    } else if (this.shape === "square") {
      rectMode(CENTER);
      square(this.position.x, this.position.y, 12);
    } else if (this.shape === "triangle") {
      push();
      translate(this.position.x, this.position.y);
      rotate(PI / 6); // rotar un poco para que no quede plano
      triangle(-6, 6, 6, 6, 0, -6);
      pop();
    }
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

  ```
4. [link del ejercicio modificado](https://editor.p5js.org/nicolasparra2024/sketches/g6VA76FDC)


### Ejercicio 3
1.agregar nuevas formas.

2. Procederemos a desglosar el código para entender lo que hace, ya que visualmente se parece al ejercicio anterior, pero su forma de optimizar la memoria es diferente.
Primero vemos que existe una función llamada run, la cual recorre un arreglo de partículas. Al observar mejor el código, notamos que en el archivo particula.js ya se define un tiempo de vida para cada partícula. Sin embargo, no nos vamos a quedar con la duda de qué es lo que hace esta función y por qué recorre un arreglo para luego comprobar si la partícula está muerta o no.

   Este metodo recorre la lista de atras hacia delante y se encarga de eliminar de la lista las particulas que ya murieron ``this.particles.sdplice(i,1);``.

```js
  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```


3.codigo Fuente.

  ```js
 class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;

    this.col = color(random(255), random(255), random(255));
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);

    fill(red(this.col), green(this.col), blue(this.col), this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}
  ```
4. [link del ejercicio modificado](https://editor.p5js.org/natureofcode/sketches/2ZlNJp2EW)

### Ejercicio 4
1.Que exista una fuerza de viento que impulse las particulas hacia arriba.

2. Al observar el código, notamos que en el archivo particula.js ya se define un tiempo de vida para cada partícula. Tambien podemos observar que existe una función llamada run en el emitter.js, la cual recorre un arreglo de partículas de atras hacia delante y se encarga de eliminar de la lista las particulas que ya murieron ``this.particles.sdplice(i,1);``.
   
3.codigo Fuente.

  ```js
let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 50); // emisor en la parte de abajo
}

function draw() {
  background(255);
let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  emitter.addParticle();
  emitter.run();
  
  
  if (mouseIsPressed) {
    let wind = createVector(0, -0.1); // fuerza constante hacia arriba
    for (let p of emitter.particles) {
      p.applyForce(wind);
    }
  }

  emitter.run();
}

  ```
4. [link del ejercicio modificado](https://editor.p5js.org/nicolasparra2024/sketches/rj6gV5y9M)


### Ejercicio 5

1.Que el suelo sea una superficie que perimita que todas la bolitas reboten y tengan colores aleatorios...Se me dificulto hacer eso entonces la modificacion que agregue fue crear nuevos repellers en el canva con el click del mouse.

2.  Al observar el código, notamos que en el archivo particula.js ya se define un tiempo de vida para cada partícula. Tambien podemos observar que existe una función llamada run en el emitter.js, la cual recorre un arreglo de partículas de atras hacia delante y se encarga de eliminar de la lista las particulas que ya murieron ``this.particles.sdplice(i,1);``.
   
3.codigo Fuente.

  ```js
class Repeller {
  constructor(x, y) {
    this.position = createVector(x, y);
    //{!1} How strong is the repeller?
    this.power = 120;
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 32);
  }

  repel(particle) {
    //{!6 .code-wide} This is the same repel algorithm we used in Chapter 2: forces based on gravitational attraction.
    let force = p5.Vector.sub(this.position, particle.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 50);
    let strength = (-1 * this.power) / (distance * distance);
    force.setMag(strength);
    return force;
  }
}

  ```
4. [link del ejercicio modificado](https://editor.p5js.org/nicolasparra2024/sketches/olI_mW8kX)


## actividad 3

Es hora de una nueva creación. Diseña e implementa una obra de arte generativa algorítmica interactiva en tiempo real en p5.js que cumpla con los siguientes requisitos:

Documenta el proceso de creación, incluyendo la idea inicial, bocetos, experimentación con el código y el resultado final.

Es unidad incluye una novedad: DISEÑO. Debes intencionar tu obra. Esta vez te pediré que DISEÑES antes de generar código. Define un concepto, haz bocetos, define la interacción, etc. ¿Cuál es el concepto de tu obra? ¿Qué quieres comunicar con ella?

* **interpolacion de color**: aleatoriedad
* **Movimiento parabolico o gravedad**: fuerzas
* **Particulas**: no hay particulas
* **Optimizar Espacio**: no hay particulas

Es una applicacion que mide el sonido de una sala por medio de pendulos que detectan si un sonido es grave, medio o agudo. Me inspire en la arquitectura y lo facilque diferentes ondas de movimiento de las placas tectonicas pueden mover un edificio si su frecuencia coincide, dejare un link de un video experimental en el que me inspire (https://vt.tiktok.com/ZSUYxshbT/)

3.codigo Fuente.

  ```js
// ===================================
// 3 Péndulos reactivos al micrófono
// Grave - Medio - Agudo
// Con diferente sensibilidad
// ===================================

let mic, fft;
let pendulos = [];

function setup() {
  createCanvas(800, 500);

  // micrófono
  mic = new p5.AudioIn();
  mic.start();

  // análisis de frecuencias
  fft = new p5.FFT();
  fft.setInput(mic);

  // tres péndulos con diferentes largos y sensibilidad
// Péndulos con rangos personalizados de frecuencia
pendulos.push(new Pendulum(width/4, 50, 100, 100, 200, 0.2));     // grave
pendulos.push(new Pendulum(width/2, 50, 180, 250, 2000, 0.1));   // medio
pendulos.push(new Pendulum((3*width)/4, 50, 120, 2000, 8000, 0.2)); // agudo


  background(0);
}

function draw() {
  // efecto rastro
  fill(0, 25);
  noStroke();
  rect(0, 0, width, height);

  // espectro de frecuencias
  let spectrum = fft.analyze();

  // actualizar y mostrar cada péndulo
  for (let p of pendulos) {
    p.update(spectrum);
    p.show();
  }
}

// ===================================
// Clase Pendulum
// ===================================
class Pendulum {
  constructor(x, y, r, lowFreq, highFreq, sensibilidad) {
    this.pivot = createVector(x, y);
    this.bob = createVector();
    this.r = r;
    this.angle = PI / 4;
    this.angleVelocity = 0.0;
    this.angleAcceleration = 0.0;
    this.damping = 0.995;
    this.ballr = 20.0;

    this.currentColor = color(255, 0, 0);
    this.targetColor = color(0, 0, 255);

    // rango de frecuencias
    this.lowFreq = lowFreq;
    this.highFreq = highFreq;
    this.sensibilidad = sensibilidad;
  }

  update() {
    
    this.angleAcceleration = 0;
    let gravity = 0.94;
    this.angleAcceleration = ((-1 * gravity) / this.r) * sin(this.angle);

    // energía en rango específico
    let energia = fft.getEnergy(this.lowFreq, this.highFreq);

    let fuerza = map(energia, 0, 255, 0, 0.05) * this.sensibilidad;
    this.angleAcceleration += fuerza;

    this.angleVelocity += this.angleAcceleration;
    this.angle += this.angleVelocity;
    this.angleVelocity *= this.damping;

    if (frameCount % 30 === 0) {
      this.targetColor = color(random(255), random(255), random(255));
    }
    this.currentColor = lerpColor(this.currentColor, this.targetColor, 0.05);
  }

  show() {
    this.bob.set(this.r * sin(this.angle), this.r * cos(this.angle), 0);
    this.bob.add(this.pivot);

    stroke(255);
    strokeWeight(2);
    line(this.pivot.x, this.pivot.y, this.bob.x, this.bob.y);

    fill(this.currentColor);
    circle(this.bob.x, this.bob.y, this.ballr * 2);
  }
}

  ```
4. [link del ejercicio modificado](https://editor.p5js.org/nicolasparra2024/sketches/xcmCKql9C)

* Captura de pantallas de tu obra con las imágenes que más te gusten

<img width="785" height="483" alt="image" src="https://github.com/user-attachments/assets/f286a98f-a21f-4e29-b59c-ff3ce1cb1fcf" />

## Autoevalucion 

Nota: 3.6

1. Investigación y Experimentación (Evidencia en Actividad 2) = 5
2. Intención y Diseño (Proceso de Actividad 3) = 4 ; Es
3. Aplicación Técnica (Código de Actividad 3) = 2 ; Se me dificulto mucho creativamente crear algo, la verdad me sentia saturado de conceptos que perdi el horizonte y a la hora de volver a leer los parametros de la Actividad 3 no se muy bien que fue lo que desarrolle, tome como referencia algunos trabajos finales de mis compañeros( cuando presentaron para todos en el salon).

## Reflect: Consolidación y metacognición 🤔
Una vez termines esta unidad invierte en ti unos minutos para reflexionar sobre tu proceso de aprendizaje.

Realiza un diagrama conceptual donde incluyas todos los conceptos que has aprendido en las unidades 1 a 5.

* ¿Qué has venido haciendo bien en tu proceso durante el curso que debas mantener en la próxima unidad?

<img width="824" height="834" alt="image" src="https://github.com/user-attachments/assets/03410a48-53cb-453a-98c5-63433ab269f5" />


* ¿Qué has venido haciendo mal en tu proceso durante el curso que debas cambiar en la próxima unidad?

Profe me deje coger el tiempo pero ya con esto estoy al dia en simulacion, yo de verdad a cada trabjo trato de aprender y profundizar con la IA para entender los conceptos de raiz

