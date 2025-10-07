
# Evidencias de la unidad 6

## Actividad 1

Me gusta mucho que cree campos electromagnéticos para crear este tipo de obras, siento que son figuras o movimientos de la naturaleza que si uno domina hace que toda obra de arte se vea muy orgánica.
 
<img width="706" height="720" alt="image" src="https://github.com/user-attachments/assets/f6681cad-f264-4c5a-97a6-6ddf874afa9c" />

De esta imagen destaco el trazo me parece increíble la textura como a lápiz y el patrón de las líneas me hace pensar que tiene como un efecto de gliche.
<img width="739" height="737" alt="image" src="https://github.com/user-attachments/assets/0b5666ad-92df-459a-a75b-e33d46a42aed" />

•	¿Qué te inspira de su trabajo?

Que utiliza la programación para complementar su trabajo análogo al mismo tiempo también me gusta mucho que gracias a la generación por código es capaz de explorar y crear nuevas texturas.

## Actividad 2




* ¿Qué es una fuerza de dirección (steering force)?

Es una fuerza que guía hacia un objetivo, ajustando su trayectoria de manera controlada. No solo lo empuja, sino que le da dirección y suavidad al movimiento.

* ¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?

Las fuerzas como la gravedad y la fricción  son externas y afectan a todos por igual en cambio la steering forcé es independiente del canva y afecta a un objeto para crear efectos o movimientos como seguir, huir, miedo etc…

* ¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?
  
Craig Reynolds fue el que creó el modelo de los boids. Él introdujo las steering forces para que un objeto tomara decisiones simples generaran comportamientos colectivos realistas.


## Actividad 3

<img width="617" height="236" alt="image" src="https://github.com/user-attachments/assets/31730308-39a6-47fc-afb1-4dd63fcbd12e" />

Vamos a estudiar y a crear hipotesis de la clase FlowField para entender que pasa

```js
class FlowField {
  constructor(r) {
    this.resolution = r;
    //{!2} Determine the number of columns and rows.
    this.cols = width / this.resolution;
    this.rows = height / this.resolution;
    //{!4} A flow field is a two-dimensional array of vectors. The example includes as separate function to create that array
    this.field = new Array(this.cols);
    for (let i = 0; i < this.cols; i++) {
      this.field[i] = new Array(this.rows);
    }
    this.init();
  }

  // The init() function fills the 2D array with vectors
  init() {
    // Reseed noise for a new flow field each time
    noiseSeed(random(10000));
    let xoff = 0;
    for (let i = 0; i < this.cols; i++) {
      let yoff = 0;
      for (let j = 0; j < this.rows; j++) {
        //{.code-wide} In this example, use Perlin noise to create the vectors.
        let angle = map(noise(xoff, yoff), 0, 1, 0, TWO_PI);
        this.field[i][j] = p5.Vector.fromAngle(angle);
        yoff += 0.1;
      }
      xoff += 0.1;
    }
  }

  // Draw every vector
  show() {
    for (let i = 0; i < this.cols; i++) {
      for (let j = 0; j < this.rows; j++) {
        let w = width / this.cols;
        let h = height / this.rows;
        let v = this.field[i][j].copy();
        v.setMag(w * 0.5);
        let x = i * w + w / 2;
        let y = j * h + h / 2;
        strokeWeight(1);
        line(x, y, x + v.x, y + v.y);
      }
    }
  }

  //{.code-wide} A function to return a p5.Vector based on a position
  lookup(position) {
    let column = constrain(floor(position.x / this.resolution), 0, this.cols - 1);
    let row = constrain(floor(position.y / this.resolution), 0, this.rows - 1);
    return this.field[column][row].copy();
  }
}

```

Podemos observar en el código que se crean filas y columnas por medio del tamaño de canva y un parámetro r. Luego los organiza en un array para así poder centrarnos en cada celda de la malla de manera independiente.

En la función int() podemos ver como se crean vectores unitarios para cada celda con un ruido Perlin paraque su movimiento sea más natural.


Aquí analizaremos lo que sucede con el agente

```js
class Vehicle {
  constructor(x, y, ms, mf) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(0, 0);
    this.r = 4;
    this.maxspeed = ms;
    this.maxforce = mf;
  }

  run() {
    this.update();
    this.borders();
    this.show();
  }

  // Implementing Reynolds' flow field following algorithm
  // http://www.red3d.com/cwr/steer/FlowFollow.html
  follow(flow) {
    // What is the vector at that spot in the flow field?
    let desired = flow.lookup(this.position);
    // Scale it up by maxspeed
    desired.mult(this.maxspeed);
    // Steering is desired minus velocity
    let steer = p5.Vector.sub(desired, this.velocity);
    steer.limit(this.maxforce); // Limit to maximum steering force
    this.applyForce(steer);
  }

  applyForce(force) {
    // We could add mass here if we want A = F / M
    this.acceleration.add(force);
  }

  // Method to update location
  update() {
    // Update velocity
    this.velocity.add(this.acceleration);
    // Limit speed
    this.velocity.limit(this.maxspeed);
    this.position.add(this.velocity);
    // Reset accelerationelertion to 0 each cycle
    this.acceleration.mult(0);
  }

  // Wraparound
  borders() {
    if (this.position.x < -this.r) this.position.x = width + this.r;
    if (this.position.y < -this.r) this.position.y = height + this.r;
    if (this.position.x > width + this.r) this.position.x = -this.r;
    if (this.position.y > height + this.r) this.position.y = -this.r;
  }

  show() {
    // Draw a triangle rotated in the direction of velocity
    let theta = this.velocity.heading();
    fill(127);
    stroke(0);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(theta);
    beginShape();
    vertex(this.r * 2, 0);
    vertex(-this.r * 2, -this.r);
    vertex(-this.r * 2, this.r);
    endShape(CLOSE);
    pop();
  }
}
```
Para entender como funcionan los agentes en este tipo de códigos los veremos como una pelusa cayendo sobre el viento, sabemos que cuando va cayendo también va cambiando su movimiento ya que al ser muy ligera cada viento débil puede afectar la trayectoria esta pelusa.

Así podemos decir que los agentes son las pelusas y las celdas en la dirección del viento el cual guiara la pelusa a la siguiente rendija y así indeterminadamente. 

## Apply
<img width="649" height="553" alt="image" src="https://github.com/user-attachments/assets/6bc7f367-e99f-48cb-bb4e-22635defe2ac" />


Esta aplicación de DJ me gustó mucho. Algunas veces trabajo para un violinista, y esta es una de las canciones favoritas del público. Por lo ligera y frenética que es, me inspiré en crear un baile de partículas o de notas musicales que saltan y gozan al ritmo de la música.

Para simular esta partitura me dejé llevar por el ritmo; iba escuchando la canción mientras me imaginaba qué podía hacer. Mi primera decisión fue un piano que sonaba de fondo, pero que no pasaba desapercibido, así que debía hacer algo con él. Por ello agregué unas partículas individuales que me hacían pensar en gotas de agua cayendo en un manantial.

La segunda idea surgió al oprimir la tecla “E”. Desde el principio sabía que estas partículas necesitaban un instante de frenesí, pero como despegaban muy rápido, pensé que primero debía preparar al espectador, para que diera esa impresión de un cohete al despegar.

## AutoEvaluacion 

Nota: 4
Razon: desarrolle la actividad 1, 2 y 3 que cuenta como un punto cada una y luego desarrolle el apply que tambien vale un punto y realice la auto evaluacion.

## Reflect: Consolidación y metacognición 🤔

Explica en tus propias propias palabras qué es un agente autónomo y cómo puede contribuir al arte generativo.

Un agente autonomo es un individuo o particula en el codigo que es capas de tomar sus propias desiciones 

¿Qué es el comportamiento emergente y cómo se manifiesta en los algoritmos de flow fields y flocking?

podemos ver como las flow fiels como mallas o rejillas que tienen diferentes comportamientos o una fuerza parecida a la del viento pero con distinta magnitud los vehiculos que pasan por cada rendija se mueven hacia la posicion señalada.






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

Nota: 3.5

1. Investigación y Experimentación (Evidencia en Actividad 2) = 5
2. Intención y Diseño (Proceso de Actividad 3) = 4 ; Es
3. Aplicación Técnica (Código de Actividad 3) = 2 ; Se me dificulto mucho creativamente crear algo, la verdad me sentia saturado de conceptos que perdi el horizonte y a la hora de volver a leer los parametros de la Actividad 3 no se muy bien que fue lo que desarrolle, tome como referencia algunos trabajos finales de mis compañeros( cuando presentaron para todos en el salon).

## Reflect: Consolidación y metacognición 🤔
Una vez termines esta unidad invierte en ti unos minutos para reflexionar sobre tu proceso de aprendizaje.

Realiza un diagrama conceptual donde incluyas todos los conceptos que has aprendido en las unidades 1 a 5.
* ¿Qué has venido haciendo bien en tu proceso durante el curso que debas mantener en la próxima unidad?

* ¿Qué has venido haciendo mal en tu proceso durante el curso que debas cambiar en la próxima unidad?

* 
# Evidencias de la unidad 7


