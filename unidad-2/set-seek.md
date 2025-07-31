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

Aprendi en que casos se usa caso por valor y caso por referencia.

###Actividad 04


* ¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

* **mag**

Calcula la magnitud (longitud) del vector.

mag() permite calcular la magnitud de un vector bidimensional usando sus componentes, como en mag(x, y).

* **magSq**

Calcula la magnitud (longitud) al cuadrado del vector.( En la operacion no saca la raiz cuadrada)

**¿Cuál es más eficiente?:** magSq ya que este No usa sqrt(), que es una operación costosa

* ¿Para qué sirve el método normalize()?

  normalize escala las componentes de un objeto p5.Vector para que su magnitud sea 1.

  la version estatica de normalize(), como en ``p5.Vector.normalize(v)``, devuelve un nuevo objeto p5.Vector sin cambiar el original.

  Usa normalize() cuando:

* Te importa solo la dirección de un vector.

* Quieres aplicar una velocidad, fuerza o desplazamiento constante en esa dirección.

* Estás generando patrones radiales o controlados visualmente.

* Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase? 

para calcular el producto punto de dos vectores.

* El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?

**Instancia:** multiplica unsando el producto punto dos vectores como se muestra en el ejemplo

```js
let v1 = createVector(1, 2);
let v2 = createVector(3, 4);
let resultado = v1.dot(v2);

```

**Estatica:** Calcula el producto punto entre v1 y v2 desde la clase p5.Vector, sin necesidad de usar un vector en particular.
```js
let v1 = createVector(1, 2);
let v2 = createVector(3, 4);
let resultado = p5.Vector.dot(v1, v2);

```

* Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

¿Para que te puede servir el método dist()?

Para calcular la distancia entre dos puntos representados como vectores.

Las coordenadas de un punto en el espacio pueden ser representadas por las componentes de un vector que se extiende del origen hasta el punto.

La versión estática de `dist()`, como en ``p5.Vector.dist(v1, v2)``, equivale a llamar ``v1.dist(v2)``.

dist() permite calcular la distancia entre dos puntos utilizando sus coordenadas, como en ``dist(x1, y1, x2, y2).``

* ¿Para qué sirven los métodos normalize() y limit()?

Como se habia dicho anterior mente el metodo normalize() cambia la magnitud del vector mas no la direccion, mientras que el metodo limit() limita la magnitud de un vector a el valor que yo diga esto sirve para controlar la fuerza y la velocidad de un vector.

###Actividad 5

``` js
function setup() {
    createCanvas(100, 100);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(30, 0);
    let v2 = createVector(0, 30);
    let v3 = p5.Vector.lerp(v1, v2, 0.5);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}

```

LINK del codigo que se modificara para hacer lo que se pide:
"https://editor.p5js.org/nicolasparra2024/sketches/Tpc_TRfOP"

El código que genera el resultado que te pedí.

* ¿Cómo funciona lerp() y lerpColor().

* ¿Cómo se dibuja una flecha usando drawArrow()?




