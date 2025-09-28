# Evidencias de la unidad 4

# Sesión de Exploracion

## Exploración Actividad 2

### Parte 1
* ¿Qué está pasando en esta simulación? ¿Cuál es la interacción?

Una vara rota cada vez que se le oprime espacio 


* Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?

porque la persona que lo dibujo, creo el objeto en las cordenadad 0,0 que en el canva es la cordenada empieza dedsde la esquina superior izquierda. por ello utuliza translade para que siempre se dibuje en el centro.


* Cuál es la relación entre el sistema de coordenadas y la función rotate().

Creo que la relacion se encuentra en que el sistema de cordenadas y la rotacion del los objetos se hacen desde el centro de canva.

### Parte 2

* ¿Qué hace la función heading()?

Esta funcion indica la direccion del maouse respecto al eje x positivo
  
* ¿Qué hace la función push() y pop()? Realiza algunos experimentos para entender su funcionamiento.

Estas son acotaciones que se pueden hacer en un objeto que se dibuja en la funcion draw para que la funcion rotate no afecte en todo el canva
 
* ¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.

Este define un punto de referencial para facilitar la rotaciond e un objeto en este caso se encuentra en el centro.
  
* ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.

El vector velocidad indica alobjeto donde se encuentra el mause, el objeto siempre se esta transladando y el heading transforma el angulo en radianes y le manda esa informacion a rotacion paraque el vector velocidad apunte hacia el mause.



## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Lo que quiero es jugar con los pendulos y y poder controlar la oscilacion por medio de la voz grave, media, aguda.

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Se incluyeron fuerzas parecidas al viento
>

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
>  agregue una interpolacion de color


* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Tiene un ramdomizador de color


## ¿Cómo resolviste la interacción?
> Tu respuesta aquí:
> Con la deteccion de frecuencias 

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra]([URL](https://editor.p5js.org/nicolasparra2024/sketches/xcmCKql9C))

## Código de la obra 

``` js
// ===================================
// 3 Péndulos reactivos al micrófono
// Grave - Medio - Agudo
// Con diferente sensibilidad
// ===================================

let mic, fft;
let pendulos = [];

function setup() {
  createCanvas(800, 500);

  // micrófono
  mic = new p5.AudioIn();
  mic.start();

  // análisis de frecuencias
  fft = new p5.FFT();
  fft.setInput(mic);

  // tres péndulos con diferentes largos y sensibilidad
// Péndulos con rangos personalizados de frecuencia
pendulos.push(new Pendulum(width/4, 50, 100, 100, 200, 0.2));     // grave
pendulos.push(new Pendulum(width/2, 50, 180, 250, 2000, 0.1));   // medio
pendulos.push(new Pendulum((3*width)/4, 50, 120, 2000, 8000, 0.2)); // agudo


  background(0);
}

function draw() {
  // efecto rastro
  fill(0, 25);
  noStroke();
  rect(0, 0, width, height);

  // espectro de frecuencias
  let spectrum = fft.analyze();

  // actualizar y mostrar cada péndulo
  for (let p of pendulos) {
    p.update(spectrum);
    p.show();
  }
}

// ===================================
// Clase Pendulum
// ===================================
class Pendulum {
  constructor(x, y, r, lowFreq, highFreq, sensibilidad) {
    this.pivot = createVector(x, y);
    this.bob = createVector();
    this.r = r;
    this.angle = PI / 4;
    this.angleVelocity = 0.0;
    this.angleAcceleration = 0.0;
    this.damping = 0.995;
    this.ballr = 20.0;

    this.currentColor = color(255, 0, 0);
    this.targetColor = color(0, 0, 255);

    // rango de frecuencias
    this.lowFreq = lowFreq;
    this.highFreq = highFreq;
    this.sensibilidad = sensibilidad;
  }

  update() {
    
    this.angleAcceleration = 0;
    let gravity = 0.94;
    this.angleAcceleration = ((-1 * gravity) / this.r) * sin(this.angle);

    // energía en rango específico
    let energia = fft.getEnergy(this.lowFreq, this.highFreq);

    let fuerza = map(energia, 0, 255, 0, 0.05) * this.sensibilidad;
    this.angleAcceleration += fuerza;

    this.angleVelocity += this.angleAcceleration;
    this.angle += this.angleVelocity;
    this.angleVelocity *= this.damping;

    if (frameCount % 30 === 0) {
      this.targetColor = color(random(255), random(255), random(255));
    }
    this.currentColor = lerpColor(this.currentColor, this.targetColor, 0.05);
  }

  show() {
    this.bob.set(this.r * sin(this.angle), this.r * cos(this.angle), 0);
    this.bob.add(this.pivot);

    stroke(255);
    strokeWeight(2);
    line(this.pivot.x, this.pivot.y, this.bob.x, this.bob.y);

    fill(this.currentColor);
    circle(this.bob.x, this.bob.y, this.ballr * 2);
  }
}
```

## Captura de pantalla representativa











