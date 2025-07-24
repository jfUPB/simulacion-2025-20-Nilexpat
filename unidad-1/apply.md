# Unidad 1

## 🛠 Fase: Apply

### Actividad 08
Creación de obra generativa

Vas a crear una obra generativa interactiva en tiempo real utilizando los conceptos de aleatoriedad que has aprendido en esta unidad.
Tu obra debe:

Usar al menos tres conceptos estudiados en esta unidad COMBINADOS de manera creativa y coherente.
Tu obra de ser interactiva y generativa en tiempo real. Puedes usar el mouse, el teclado o cualquier otro sensor de entrada para interactuar con la obra.
📤 Bitácora

Reporta en tu bitácora lo siguiente:

1. Un texto donde expliques el concepto de obra generativa.

con esta unidad quiero poner a prueba  si puedo convinar el ruido de perlin con los colres, para que haga una tansiciones suaves, tambien sera el primer prototipo para crear un sistemas de particulas que se expanda hacia los bordes de la pantalla. usare un ramndom, en los colores de las particulas, un noise perlin en el fondo, y generare particulas al dar click con el raton.

*variables globales*
``` js
let noiseOffset = 0;
let particles = [];
```

*function setup()*
```
```

*funcion draw()  "agregar para el cambio de color del canvas"*
``` js
function draw() {

//se agregan variables para configurar el noise en cada color RGB.
  let r = noise(noiseOffset) * 255;
  let g = noise(noiseOffset + 10) * 255; 
  let b = noise(noiseOffset + 20) * 255;

 // se llaman esas variables al color del fondo. 
  background(r,g,b);
...
...
...
/esta parte es la que hace toda la magia del Perlin recomiendo dejarlo a lo ultimo de la funcion draw
  noiseOffset += 0.01;
}
```

Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.

[Enlace de la Apply](https://editor.p5js.org/nicolasparra2024/sketches/EacQ1BuK4)
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
