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
  
* Copia el código en tu bitácora.
* Coloca en enlace a tu sketch en p5.js en tu bitácora.
* Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.
