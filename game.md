# Concepto de Video Juegos

## Cuadros por segundo (Frame Rate)

 Un video juego en escencia es un gran bucle, comunmente conocido como 'Game Loop'. Cada iteración del bucle tiene como objetivo las siguiente tres cosas:
 
 1. El video juego obtiene entradas de usuario.
 2. Actualizacion dentro del mundo del juego ya sea cosas fisicas, personaje, inteligencia artificia o uso de la entrada del usuario.
 3. Actualizar los que el usuario ve por la pantalla.
 
Cada corrida del bucle como resultado nos muestra cuadros o imagenes distinta en pantalla. Cuadros por segundo o fotogramas por segundo "Frame rate" es el termino el cual describe la frecuencia el cual los cuadros o imagenes son dibujadas y mostradas en pantalla o a que frecuencia de velocidad el bucle del juego se ejecuta. Usualmente esta frecuencia es medida en segundos como cuadros por segundos.

Los video juegos suelen reproducirse a 30 o 60 cuadros por segundo.

## Delta Time

Nuestro codigo del juego es convertido a leguaje maquina para luego ser ejecutado por el CPU de la maquina, este CPU tiene una velocidad por segundo que nos permite sabes cuantas instrucciones por segundo pueden ser procesadas. Esta velocidad es medida en gigahercios "gigahertz" (GHz).

Existen tipos de CPU que pueden ejecutar o procesar intrucciones a diferentes velocidades, como por ejemplo CPU con velocidades de 3GHz o 2.6GHz. Esto nos puede demostrar que tenemos maquina que son un poco mas lentas que otras al momento de ejecutar o procesar intrucciones.