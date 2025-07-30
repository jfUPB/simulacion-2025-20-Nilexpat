# Unidad 2

## 🔎 Fase: Set + Seek

##APUNTES

###Actividad 01

* ¿Cómo funciona la suma dos vectores en p5.js?

 ``` js
  position = createVector(100, 100); // se posiciona el vector en la posicion del canva
  velocity = createVector(2.5, 2);

  ```

como hacer para que un vector no se salga de los bordes, este ejemplo da una ilusion de rebote con los bordes.

``` js
  if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1; // la velocidad en el eje x se vuelve negativa 
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1; // la velocidad en el eje y se vuelve negativa 
  }
```
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


###Actividad 03

```js
let position;

function setup() {
    createCanvas(400, 400);
    position = createVector(6,9);
    console.log(position.toString());
    playingVector(position);
    console.log(position.toString());
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```

* ¿Qué resultado esperas obtener en el programa anterior?

que se imprima el resultado de la posicion del vector actual, luego se ejecute la funcion playing vector y se impriman los nuevos valores del vector position y luego el Only Once.
  
* ¿Qué resultado obtuviste?

Estos resultados arrojaron la consola:

```
p5.Vector Object : [6, 9, 0] 
p5.Vector Object : [20, 30, 0] 
Only once 
```


* Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.


segun la IA este es un paso por referencia el cual modifica el valor original dentro del setup, importante tener en cuenta que el programa solo puede hacer esto con un array o un objeto ( en este caso OBJETO), el paso por valor solo crea una copia de un `number`, `boolean`, `string`.

* ¿Qué tipo de paso se está realizando en el código?

Paso por referencia.

* ¿Qué aprendiste?

aprendi en que casos se usa caso por valor y caso por referencia.
