# Unidad 1

## 🤔 Fase: Reflect

### Actividad 09
Autoevaluación
Mirando hacia adentro: autoevaluación de conceptos y creación

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

En este caso siento que fue mas la parte creativa, porque eran tantas funciones aleatorias que ya no sabia que meterle de mas aleatorismo.
  
* Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?

le agregaria un salto de levi en la funcion del mouse y cada ves que se active la probabilidad cambien de figura.

### Actividad 10

1. Basándote en la rúbrica para la actividad 08 evalúa el trabajo del compañero y escribe un comentario de retroalimentación constructiva. Esto lo harás en tu bitácora de aprendizaje.

fue un muy bonito concepto y visualmente creía que estaba viendo un estanque con peces, aunque solo fueran bolitas, en clase me comento unos problemas que tuvo con la programación entonces se hizo una autoevaluación, de cómo podría mejorar el movimiento de los peces ya que al ser aleatorio solían acercarse a la piraña.

Corrección: mi compañero me presento un acuario más interactivo y con la corrección de los peces que se movían con un Walker aleatorio ahora se mueven con un perlin noise, la "piraña" se come a un pez y entra en cooldawn, la función interactiva paso de controlar a la piraña a entretenerse darle comida a los peces mientras ellos crecen; la piraña sigue al pez mas grande.

**Mecánicas encontradas: ** si la piraña está persiguiendo un pez grande y luego aparece un pez más grande la piraña cambia de objetivo y empieza perseguir al otro pez.

3. Conversa con tu compañero sobre su obra y tu feedback. Escucha sus reflexiones y comparte tus propias ideas.

se conversó en clase, y su concepto me gustó mucho una pecera en donde los hay peces y una piraña que se los intenta comer, ideas que surgieron, que si los peces se comían o se tocaban entre ellos se hicieran más grande, o que si la piraña se comía al otro también se hiciera más grande



### Actividad 11

* Continuar: ¿Qué actividad, ejemplo o explicación de esta unidad te resultó más reveladora o útil para tu aprendizaje? ¿Qué deberíamos mantener sí o sí?

La liena del arte generativo me parece muy importante para el tema de experiencias interactivas.

* Dejar de hacer: ¿Hubo alguna actividad o concepto que te pareció redundante, confuso o menos útil? ¿Hay algo que eliminarías o cambiarías por completo?

No.


* Empezar a hacer: ¿Qué te faltó en esta unidad? ¿Quizás más ejemplos de artistas, más desafíos técnicos, más teoría? ¿Qué idea tienes para hacerla mejor?

me gustaria que hubieran retos, que podamos recrear con pistas en el camino, como replica esta animacion teniendo encuenta tal texto o codigo de esta unidad, siento que tengo un bloqueo mental que si no lo veo posible, no es posible crearlo mas que todo porque soy principiante en esta materia.


* Balance Teoría-Práctica: ¿Cómo sentiste el equilibrio entre analizar los ejemplos del texto guía y ponerte a programar tus propios sketches? Explica tu respuesta.

Me gusta la metodologia aunque sinto que puede ser un poco cargada para la distribucion de mi tiempo aveces me tomo mas de media hora por ejercicio.

* Comentario Adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad?
  
No.
