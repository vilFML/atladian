# Operadores



# Usos de Operadores

## División Entera //
La división entera por 10 permite 'cortar' un número, eliminando dígitos a su derecha.
- El exponente de la potencia de 10 (la cantidad de ceros) determina la cantidad de dígitos que **se eliminan** *contando desde la derecha*
###### Ejemplos
1. `12345 // 10 = 1234`: Se elimina solo un número a la derecha pues hay solo un cero ($10^{1}$)
2. `12345 // 1000 = 12`: Se eliminan tres dígitos pues hay tres ceros ($10^{3}$)
3. `12345 // 100000`: Se eliminan todos los números pues hay cinco ceros ($10^{5}$)

## Modulo %
Aplicar módulo por 10 permite **cortar** el número al que se le aplica. Se extraen (rescatan) dígitos **desde su derecha.**
- El exponente de la potencia de 10 (la cantidad de ceros) indica cuántos dígitos **se extraen** *contando desde la derecha.*
###### Ejemplos
1. `12345 % 10 = 5`: Se extrae solo un número desde la derecha pues hay solo un cero ($10^{1}$)
2. `12345 % 100 = 345`: Se extraen tres números por los tres ceros ($10^{3}$)
3. `12345 % 100000 = 12345`: Entrega todo el número pues se extraen los cinco dígitos por los cinco ceros ($10^{5}$).