# Evidencias de la unidad 5

## actividad 2

🧐🧪✍️ En tu bitácora responde a esta pregunta para cada una de las simulaciones: ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

Además te pediré que hagas los siguientes experimentos y los reportes en tu bitácora:

* Vas a modificar cada una de las simulaciones anteriores incluyen en cada una, al menos un concepto de las unidades anteriores, pero no repitas concepto, la idea es que repases al menos uno de cada unidad.
* Vas a gestionar la creación y la desaparición de las partículas y la memoria. Explica cómo lo hiciste (aunque es posible que la simulación ya lo haga, trata de identificarlo de nuevo y explicarlo con tus palabras).
* Explica qué concepto aplicaste, cómo lo aplicaste y por qué.
* Incluye un enlace a tu código en el editor de p5.js.
* Incluye el código fuente de cada una de las simulaciones.
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
1.

2. En este primer ejemplo las particulas se crean por medio de una matriz la cual lee la matriz de atras hacia delante, esto para que no cause error a la hora de iterar(recorrer la matriz), para modificar una matriz hay que tener encuanta la funcion splice y lo que hace cada uno de sus parametros `` array.splice(punto de partida del array, cantidad de elemtos que vas a eliminas, agregar item1,agregar item2, ...); ``.
3.codigo Fuente.

  ``js
  


  
  ``
4. [link del ejercicio modificado]()

 
Que con cada click las particulas cabien aleatoriamente (polimorfismo).

### Ejercicio 3
1.

2. En este primer ejemplo las particulas se crean por medio de una matriz la cual lee la matriz de atras hacia delante, esto para que no cause error a la hora de iterar(recorrer la matriz), para modificar una matriz hay que tener encuanta la funcion splice y lo que hace cada uno de sus parametros `` array.splice(punto de partida del array, cantidad de elemtos que vas a eliminas, agregar item1,agregar item2, ...); ``.
3.codigo Fuente.

  ``js
  


  
  ``
4. [link del ejercicio modificado]()
agregar nuevas formas.

### Ejercicio 4
1.

2. En este primer ejemplo las particulas se crean por medio de una matriz la cual lee la matriz de atras hacia delante, esto para que no cause error a la hora de iterar(recorrer la matriz), para modificar una matriz hay que tener encuanta la funcion splice y lo que hace cada uno de sus parametros `` array.splice(punto de partida del array, cantidad de elemtos que vas a eliminas, agregar item1,agregar item2, ...); ``.
3.codigo Fuente.

  ``js
  


  
  ``
4. [link del ejercicio modificado]()
Que exista una fuerza de viento que impulse las particulas hacia arriba.

### Ejercicio 5
1.

2. En este primer ejemplo las particulas se crean por medio de una matriz la cual lee la matriz de atras hacia delante, esto para que no cause error a la hora de iterar(recorrer la matriz), para modificar una matriz hay que tener encuanta la funcion splice y lo que hace cada uno de sus parametros `` array.splice(punto de partida del array, cantidad de elemtos que vas a eliminas, agregar item1,agregar item2, ...); ``.
3.codigo Fuente.

  ``js
  


  
  ``
4. [link del ejercicio modificado]()
que el suelo sea una superficie que perimita que todas la bolitas reboten y tengan colores aleatorios.

## actividad 3

Es hora de una nueva creación. Diseña e implementa una obra de arte generativa algorítmica interactiva en tiempo real en p5.js que cumpla con los siguientes requisitos:

Documenta el proceso de creación, incluyendo la idea inicial, bocetos, experimentación con el código y el resultado final.

Es unidad incluye una novedad: DISEÑO. Debes intencionar tu obra. Esta vez te pediré que DISEÑES antes de generar código. Define un concepto, haz bocetos, define la interacción, etc. ¿Cuál es el concepto de tu obra? ¿Qué quieres comunicar con ella?
* Debes utilizar los conceptos de herencia y polimorfismo que revisaste en la fase de investigación.
* Debes utilizar al menos un concepto de cada una de las unidades anteriores: 4 conceptos.
* Debes definir cómo vas a gestionar el tiempo de vida de las partículas y la memoria.
* La obra debe ser interactiva en tiempo real. Puedes usar teclado, mouse, música, el micrófono, video, sensor o cualquier otro dispositivo de entrada.
* Incluye un enlace a tu código en el editor de p5.js.
* Incluye el código fuente.
* Captura de pantallas de tu obra con las imágenes que más te gusten


