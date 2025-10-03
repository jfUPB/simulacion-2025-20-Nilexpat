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
