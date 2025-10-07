
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






