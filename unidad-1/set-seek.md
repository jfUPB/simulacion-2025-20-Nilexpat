# Unidad 1

## 🔎 Fase: Set + Seek

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

 <codigo><https://editor.p5js.org/nicolasparra2024/sketches/O0_ubqVxs>
  
* Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
