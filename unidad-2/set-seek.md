# Unidad 2

## 🔎 Fase: Set + Seek

##APUNTES

###Actividad 01

* ¿Cómo funciona la suma dos vectores en p5.js?

 `` 
  position = createVector(100, 100); // se posiciona el vector en la posicion del canva
  velocity = createVector(2.5, 2);
  ``

como hacer para que un vector no se salga de los bordes, este ejemplo da una ilusion de rebote con los bordes.

``  if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1; // la velocidad en el eje x se vuelve negativa 
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1; // la velocidad en el eje y se vuelve negativa 
  }
``
* ¿Por qué esta línea position = position + velocity; no funciona?

 porque la sobre carga de la suma no esta implementada en esta biblioteca si lo queremos hacer debemos usar el metodo add.
ejemplo  ``position.add(velocity)``


###Actividad 02

* ¿Qué tuviste que hacer para hacer la conversión propuesta?

hacer apuntes
  
* Muestra el código que utilizaste para resolver el ejercicio. "https://editor.p5js.org/nicolasparra2024/sketches/11s4QYLCV" 

```js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    

    this. position = createVector(width/2 , height/2 );
  
  }

  show() {
    stroke(0);
    point(this.position.x , this.position.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.position.x++;
    } else if (choice == 1) {
      this.position.x--;
    } else if (choice == 2) {
      this.position.y++;
    } else {
      this.position.y--;
    }
  }
}


```
