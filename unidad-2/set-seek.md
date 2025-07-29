# Unidad 2

## 🔎 Fase: Set + Seek

##APUNTES

* ¿Cómo funciona la suma dos vectores en p5.js?

 `` 
  position = createVector(100, 100); // se posiciona el vector en la posicion del canva
  velocity = createVector(2.5, 2);
  ``

como hacer para que un vector no se salga de los bordes, este ejemplo da una ilusion de rebote con los bordes.

``  if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1; // la velocidad en el eje x se vuelve negativa 
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1; // la velocidad en el eje y se vuelve negativa 
  }
``
* ¿Por qué esta línea position = position + velocity; no funciona?

 porque la sobre carga de la suma no esta implementada en esta biblioteca si lo queremos hacer debemos usar el metodo add.
ejemplo  ``position.add(velocity)``
