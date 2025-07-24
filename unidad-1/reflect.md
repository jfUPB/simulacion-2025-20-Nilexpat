# Unidad 1

## 🤔 Fase: Reflect

### Actividad 09
Autoevaluación
Mirando hacia adentro: autoevaluación de conceptos y creación

El objetivo de esta actividad es que recuperes de tu memoria los conceptos fundamentales sobre aleatoriedad y que reflexiones sobre tu propio proceso creativo y de aprendizaje. Al forzarte a recordar sin ver tus notas, fortaleces las conexiones neuronales de lo que has aprendido.

📤 Bitácora

En tu bitácora de aprendizaje. Sin consultar tus apuntes, el editor de código o cualquier otro material, responde con tus propias palabras a las siguientes preguntas. Lo importante es el esfuerzo de recordar, no la perfección.

Parte 1: recuperación de conocimiento (Retrieval Practice)

* Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?

**RTA:** visualmente la aletatoriedad hecha por random hace saltos muy aleatorio lo que da un efecto visual algo seco o tosco, en cambio el ruido de Perlin existe una forma de controlar la longitud de estos saltos y ademas visualmente entre los datos pareciera que existiera una interpolacion entre cada salto aleatorio ya que crea un movimiento delicado como si fuera una trancision; el ramdom lo usaria para crear particulas explosivas de diferentes colores. en cambio el ruido de perlin lo usaria para modificar cosas que requiera un movimiento organico como el sonido de un bajo.

* Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?

Entiendo por distribucion de probabilidad, la probabilidad que tiene un punto, una linea o una figura de cualquier dimension de ocupar un lugar en background, la caminatsa aleatoria se tiene la misma probabilidad de hacer que un objeto en cada frame se mueva a cuaquiera de las dos direcciones X y Y, la distribucion uniforme crea una media y una desviacion estandar la cual hace que en cada frame los objetos tengas mas probabilidad de caer en una zona en especifica, la distribucion uniforme como su nombre lo dice es una distribucion controlada en una area que llena de manera uniforme.


* ¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
Piensa en tu obra final (Actividad 08).

la aleatoriedad, puede crear visuales nunca antes vistas, las cuales pueden generar imagenes que podemos predecir si conocemos el codigo, tambien tener en cuenta que gracias a la creacion del ruido de Perlin los directores la pelicula de TRON puedieron ahorrarse tiempo con las animaciones y me imagino que tambien ahorraron dinero.

* Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
  el noise() en lo personal siento que fue uno de los conceptos aleatorios mas importantes y creo que ahora que lo conozco podria usarlo para crear visuales mas organicas
  
* ¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?
los Walks son saltos que dan figuras o puntos. El Levy flight nace para que estos saltos que dan a la hora de hacer una caminata aleatoria tengan una mayor probabilidad de no devolverse este consiste en dos variables aleatorias del 0 al 1 las cuales son representadas por r1 y r2 se comparan y si r2 > r1 retorna r1

Parte 2: reflexión sobre tu proceso (Metacognición)

* ¿Cuál fue el concepto más abstracto o difícil de “visualizar” para ti en esta unidad? ¿Qué hiciste para finalmente comprenderlo?
Describe un momento durante el desarrollo de tu obra final (Actividad 08) en el que un “error” o un resultado inesperado te llevó a una idea creativa interesante.

*Dificil*

Salto de Levy: no estudie el ejemplo adecuado 

*abstracto*

El ruido de perlin: me parecio bello cuado lo vi en formato 3D.


* Al combinar diferentes técnicas de aleatoriedad, ¿Cuál fue el mayor desafío? ¿La interacción entre los sistemas, el control de los parámetros, el rendimiento?

en este caso siento que fue mas la parte creativa, porque eran tantas funciones aleatorias que ya no sabia que meterle mas aleatorismo.
  
* Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?

le agregaria un salto de levi en la funcion del mause y cada ves que se active la probablidad cambien de figura.
