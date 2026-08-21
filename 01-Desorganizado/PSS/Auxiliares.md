# Aux 2
## Numero Binario
## Numero Hexadecimal


## Operaciones

### Extraer Bits

Para extraer bits en ciertas posiciones de un número binario, se opera con un número binario tal que: 
- Tiene `1` en las posiciones que se desean extraer.
- *Máscara*: Tiene `0` en las demás.
  Para crear una máscara es recomendable crear un número lleno de `1` y desplazar hacia la derecha una cantidad igual a cuantos números se desee extraer para que se rellenen las posiciones restantes con `0`, por ejemplo:
  ```C
  m = -1U
  mask = ~(m>>2)
  ```
  
  Ej: Para el número `01010011` y se desea

# Ejercicios
## P1
Una idea es usar una máscara compuesta por un solo `1`. La máscara se opera con el número para extraer 