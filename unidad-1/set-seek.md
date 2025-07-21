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
**SOLUCION:**: se agrego en la funcion de los pasos un if else que sumara a x hacia la derecha (This.X++;) y se modifico el ramdomizador de 4 -> 5
