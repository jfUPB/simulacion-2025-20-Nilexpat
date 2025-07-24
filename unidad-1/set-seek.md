# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.

Un conjunto de eventos distopicos que trazan una huella en el tiempo.

### Actividad 02

Luego de ver el trabajo de Sofía piensa y escribe en TUS PROPIAS palabras:

- Cuál es el papel de la aleatoriedad en su obra.

Crea una textura en la obra y tambien determina el movim iento de las raices
  
- Según tu perfil profesional, cómo se aplica el concepto de aleatoriedad en el tipo de proyectos que desarrollas. Ilustra tu respuesta con ejemplos concretos.

En estos momentos mes esta llamando mucho la atencion las experiencias interactivas con sonidos o gestos en vivo, me gustaria utilizarlo para crear puestas en escenas.

### Actividad 03
#### CAMINATAS ALEATORIAS

Realiza el siguiente experimento y reporta los resultados en tu bitácora:

* Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.

``` js
  
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
}

function draw() {
  background(random(255), random(255), random(255), 150);
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

**Modifico:** Se agrego un Random en los colores del background 
  
* Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
que cambiara el color del fondo pero el trazo se mantuviera, aunque no fue asi, se arreglo un poco agregandole un alpha.

* Ejecuta el código y escribe en tu bitácora qué sucedió realmente.

Cambio el fondo de varios colores y solo se vio como se movia un punto

* Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?

no, no porque queria que le punto manduviera su rastro pero se perdio.

### Actividad 04

* En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.

**RTA:** La distribucion uniforme guia al walker a pintar areas del background de manera uniforme, como se muestra en el ejemplo (una linea recta) con limites, y de manera no uniforme aumenta la probabilidad de incertidumbre de que el walker no pinte toda la zona delimitada, tambien intuyo que no posee una direccion concisa.

* Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.
``` js
   step() {
    const choice = floor(random(5));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 4) {
      this.x++;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
```
**SOLUCION:** se agrego en la funcion de los pasos un if else que sumara a x hacia la derecha (This.X++;) y se modifico el ramdomizador de 4 -> 5

### Actividad 05
``` js
function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 60);
  noStroke();
  fill(0, 10);
  circle(x, 120, 16);
}
```
**ANALISIS:** 

* Se observa en la "funtion Draw()" la implementacion de una nueva funcion `Let x = randomGaussian(320, 60)`, Let x "especifica la direccion de la distribucion", randomGaussian(Media, Desviacion Estandar)
* una funcion que dibuja un circulo `circle(x,120,16)`
  Dibuja un círculo en:

`x` → posición horizontal (aleatoria con distribución normal)

`120` → posición vertical fija

`16` → diámetro del círculo
* ` noStroke();` las figuras no tendran borde solo relleno.
* `fill(0, 100, 255, 50);` // define el color y la opacidad del objeto (Azul claro con opacidad baja)

``` js
function setup() {
  createCanvas(640, 240);
  background(0);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 15);
  let y = randomGaussian(100, 15);
  noStroke();
  fill(random(255), random(255),random(255),50);
  circle(x, y, random(200));
}
  ```
[Codigo editado](https://editor.p5js.org/nicolasparra2024/sketches/WEY5RuNXG)

### Actividad 06
* Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.
  
* Explica por qué usaste esta técnica y qué resultados esberabas obtener.
  
esta tecnica la verdad no se como usarla del todo, ya que a mi parecer hace movimientos muy bruscos creo que la podria implementar depronto con sonido y que suba i baje en funcion de los decibelios; el diseño lo dejare igual, no me enfocare en los graficos si no en la funcionalidad del experimento.

**Apuntes:**
esta es la funcion principal del codigo `Vuelo de Levy` lo que sucede es que elige dos variables aleatorias las cuales compara y si R2 es mayor a R1 acepta el salto.

```
function acceptreject() {
  while (true) {
    // Pick a random value. 
    let r1 = random(1);  // elige un numero aleatorio 0 al 1
    // Assign a probability.
    let probability = r1;
    // Pick a second random value.
    let r2 = random(1);

    //{!3} Does it qualify?  If so, we’re done!
    if (r2 < probability) {
      return r1;

```
no puede hacer la parte del microfono, entonce simplemente cambien las columnas por un circulo que ccrecia en fincion de R1 por medio del metodo de `acceptreject()` aqui dejo los apuntes relevantes que tome depues del experimento.
* se agrega la variable `r1 = 0;`
* dejamos las funcion `acceptreject()` tal cual como esta
* modificamos r1 intanciando la funcion `r1 = acceptreject();`
* creamos una variable radio en funcion de r1 que actua como el radio del circulo
* se crea la funcion de `ellipse(posicion x, posicion y, ancho, alto)`


  
* Copia el código en tu bitácora.

``` js
let r1 = 0;

function setup() {
  createCanvas(640, 240);
  noStroke();
}

function draw() {
  background(255);

  // Generar nuevo valor r1 en cada frame
  r1 = acceptreject();

  // Dibujar un círculo en el centro cuyo tamaño depende de r1
  fill(100, 150, 255, 200);
  let radius = r1 * 200; // escala el tamaño
  ellipse(width / 2, height / 2, radius, radius);

  // Mostrar valor r1
  fill(0);
  textSize(16);
  text("r1 (valor aceptado): " + nf(r1, 1, 3), 20, 30);
}

// Método de aceptación-rechazo (probabilidad y = x)
function acceptreject() {
  while (true) {
    let r1 = random(1);
    let probability = r1;
    let r2 = random(1);
    if (r2 < probability) {
      return r1;
    }
  }
}
```
  
* Coloca en enlace a tu sketch en p5.js en tu bitácora.

[Link del programa creado](https://editor.p5js.org/nicolasparra2024/sketches/O0_ubqVxs)
  
* Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.

  <img width="449" height="220" alt="image" src="https://github.com/user-attachments/assets/7f59729f-ad76-4c2f-8e65-83b5c506a521" />


