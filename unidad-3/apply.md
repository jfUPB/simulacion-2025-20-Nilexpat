# Unidad 3


## 🛠 Fase: Apply

Diseña e implementa tu obra generativa interactiva en tiempo real.

- [x] Debe ser interactiva.
  
- [ ] Debes usar al menos dos algoritmos diferentes de la unidad 1, además de random.

- [x] Explica cómo modelaste el problema de los n-cuerpos en tu obra.

**Explicacion:** Es un lago de peces en donde te sentaras a darle comida a los peces mientras pasas el tiempo pensando de la vida.

Utilizare un codigo del libro como plantilla, el cual modificare la gravedad y que suba de forma progresiva cuando el jugador le de comida a los peces, tambien usare la funcion mousepresed para dar comida, y hare que el eje en donde coman los peces sea en donde el jugador haya dado click.

Copia el enlace a tu simulación en p5.js.

link: https://editor.p5js.org/nicolasparra2024/sketches/bk2jfWQIs

Copia el código.

**sketch.js**
```js
let movers = [];
let G = 0;
let targetG = 2;
let foods = []; // la comida será el "sol"

function setup() {
  createCanvas(640, 240);
  for (let i = 0; i < 100; i++) {
    let pos = p5.Vector.random2D();
    let vel = pos.copy();
    vel.setMag(random(2, 5)); // velocidades más suaves
    pos.setMag(random(50, 100));
    vel.rotate(PI / 2);
    let m = random(5, 10);
    movers[i] = new Mover(pos.x, pos.y, vel.x, vel.y, m);
  }
  background(255);
}

function draw() {
  background(50, 100, 200, 50);
  translate(width / 2, height / 2);

  // G se acerca al targetG
  G = lerp(G, targetG, 0.01);

  for (let mover of movers) {
    for (let food of foods) {
      mover.seek(food.pos);
    }
    mover.update();
    mover.show();
  }

  // Dibujar y actualizar comidas
  for (let i = foods.length - 1; i >= 0; i--) {
    let food = foods[i];
    noStroke();
    fill(255, 100, 0, food.life);
    ellipse(food.pos.x, food.pos.y, 10);

    // La comida se va consumiendo
    food.life -= 1;

    // Si se acaba, reducir targetG y quitarla
    if (food.life <= 0) {
      targetG = max(0, targetG - 0.2);
      foods.splice(i, 1);
    }
  }
}

function mousePressed() {
  foods.push({ pos: createVector(mouseX - width / 2, mouseY - height / 2), life: 255 });
  targetG += 0.2; // cada comida aumenta gravedad
}
```


**Mover.js**
```js

```
Captura una imagen representativa de tu ejemplo.

link: https://editor.p5js.org/nicolasparra2024/sketches/bk2jfWQIs


