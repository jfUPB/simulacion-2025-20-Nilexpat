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
