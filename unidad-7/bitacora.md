# Evidencias de la unidad 7

1. Muestra el código de los dos (o más) experimentos básicos que replicaste integrando Matter.js y p5.js.
2. Incluye una **captura de pantalla o ENLACE a un GIF (no olvides, enlace) de cada experimento funcionando.
3. Proporciona tu explicación clara y concisa de los conceptos clave (Engine, World, Bodies, Constraint, MouseConstraint).
4. Menciona brevemente cualquier dificultad encontrada al configurar o usar Matter.js inicialmente.

### Tutorial 1

```js
const {Engine, Body, Bodies, Composite, Render, Runner} = Matter;

let engine;
let render; let runner;
let box; let circle; let polygon;
let ground;

function setup() {
  noCanvas();
  engine = Engine.create();
  render = Render.create({
    element: document.body,
    engine: engine,
    options: {
    width: 400,
    height: 400
    
  }
});
  
  box = Bodies.rectangle(100,100,50,50);
  Body.setAngularVelocity(box, 0.2);
  
  circle = Bodies.circle(130,0,30);
  polygon = Bodies.polygon(150,30,6,50)
  
  ground = Bodies.rectangle(200, 300, 400, 10,{isStatic: true});
  
  Composite.add(engine.world, [box, circle, polygon, ground]);

  
  Render.run(render);
  
  runner = Runner.create();
  Runner.run(runner, engine);

}
```
<img width="378" height="295" alt="image" src="https://github.com/user-attachments/assets/5a4d9669-4ae9-4712-9dc9-2559ba80862e" />


### Tutorial 2

```js
const {Engine, Body, Bodies, Composite} = Matter;

let engine;
let render; 
let box;
let ground;

function setup() {
  createCanvas(400,400);
  engine = Engine.create();

  box = Bodies.rectangle(100,100,50,50);
  Body.setAngularVelocity(box, 0.2);
  
  circle = Bodies.circle(130,0,30);
  polygon = Bodies.polygon(150,30,6,50)
  
  ground = Bodies.rectangle(200, 300, 400, 10,{isStatic: true});
  
  Composite.add(engine.world, [box, ground]);
  
}

function draw(){  
background(220);
Engine.update(engine);

 push();
  rectMode(CENTER)
  let x = box.position.x;
  let y = box.position.y;
  let angle = box.angle;
  
  translate(x,y);
  rotate(angle);
  rect(0,0,50,50);
  pop();
  
  
 let gp1 =ground.bounds.min.x;
 let gp2 =ground.bounds.min.y;
 let gp3 =ground.bounds.max.x;
 let gp4 =ground.bounds.max.y;
  
  rectMode(CORNERS)
  rect(gp1,gp2,gp3,gp4);
  
  }
     
```
<img width="391" height="306" alt="image" src="https://github.com/user-attachments/assets/49e56f91-4ab4-4474-8c04-685d95be3fb7" />


Proporciona tu explicación clara y concisa de los conceptos clave (Engine, World, Bodies, Constraint, MouseConstraint).

* **Engine:** Este es el motor que le da vida al programa durante cada frame.
* **World:** Este como su nombre los dice es el espacio o mundo donde se encuentra el motor y se accionan todas las fisicas de los objeto.
* **Bodies:** Estos son los objetos fisicos dentro de este mundo.
* **Constraint:** creo que este es el que hace que los objetos tengan un coliciones.
* **MouseConstraint:** Es el que perimte que uno interactue con el mundo por medio del mouse.

## Actividad 3 (apply)

     
```js 
const { Engine, World, Bodies, Body } = Matter;

let engine, world;
let ground;
let letters = [];
let word = "MATRIX";
let fontSize = 64;

// Dos fuentes
let customFont;
let defaultFont;

function preload() {
  customFont = loadFont("matrix.ttf"); // 👈 tu fuente decorativa
}

function setup() {
  createCanvas(800, 800);
  defaultFont = "monospace"; // fuente estándar del sistema
  textAlign(CENTER, CENTER);
  textSize(fontSize);
  noStroke();

  engine = Engine.create();
  world = engine.world;
  world.gravity.y = 1;

  // Suelo
  ground = Bodies.rectangle(width / 2, height/2 +50, width, 40, {
    isStatic: true,
    restitution: 1,
  });
  World.add(world, ground);

  // Crear cuerpos para cada letra
  let spacing = width / (word.length + 1);
  for (let i = 0; i < word.length; i++) {
    let x = spacing * (i + 1);
    let y = random(-200, -50);
    let body = Bodies.rectangle(x, y, fontSize, fontSize, {
      restitution: 0.6,
      friction: 0.3,
    });
    World.add(world, body);

    letters.push({
      body,
      char: word[i],
      display: random(["0", "1"]),
      revealed: false,
      glow: 0, // efecto de brillo
    });
  }
}

function draw() {
  background(0);
  Engine.update(engine);

  textSize(fontSize);

  for (let l of letters) {
    let pos = l.body.position;
    let vel = l.body.velocity;
    let angle = l.body.angle;

    push();
    translate(pos.x, pos.y);
    rotate(angle);

    let speed = Math.abs(vel.x) + Math.abs(vel.y);

    // Si ya no rebota, revelar la letra
    if (speed < 0.2 && !l.revealed) {
      l.revealed = true;
      l.display = l.char;
      l.glow = 255; // empieza con brillo fuerte
    }

    // Mientras se mueve, mostrar 0 o 1 con fuente normal
    if (!l.revealed) {
      if (frameCount % 3 === 0) {
        l.display = random(["0", "1"]);
      }
      textFont(defaultFont);
      fill(0, 255, 70);
    } else {
      textFont(customFont);
      // Efecto de brillo
      let glow = l.glow;
      fill(0, glow, 70 + glow / 4);
      l.glow = max(70, l.glow - 5); // el brillo va bajando suavemente
    }

    text(l.display, 0, 0);
    pop();
  }
}

```

[link de la Apply](https://editor.p5js.org/nicolasparra2024/sketches/nth9t54V1)
