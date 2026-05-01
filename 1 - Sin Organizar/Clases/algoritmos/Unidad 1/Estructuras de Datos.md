Al momento de implementar algoritmos, se deben notar las maneras en que se almacena la información. Por ahora, se han visto listas de números que no se sabe realmente cómo se almacenan en la memoria.

# Memoria RAM
La memoria RAM es un 'repositorio' o espacio físico para almacenar información.

# Arreglos
Un arreglo es una representación secuencial de una secuencia de datos, y  se almacena contigua físicamente en la memoria RAM del computador.

# Listas
En una lista de tamaño $n$, se asignan $n$ espacios en la memoria. Cuando se agregan elementos y es necesario agrandar la lista, Python crea una nueva lista vacío con el doble de tamaño ($2n$) y copia los elementos a ella. Cuando la lista pierde elementos y queda de la mitad del tamaño, se hace el mismo proceso, pero con una lista nueva de tamaño $\frac{n}{2}$.

# Listas Enlazadas

Cuando se usa un arreglo de 100 millones de datos en Python, este le dice al sistema operativo que reserve 100 millones de bloques en la memoria. Es evidente que no siempre habrá tal cantidad de bloques de memoria contiguas, pero sí puede ser que hayan de forma separadas.  Para ello, se utilizan *listas enlazadas*.

Las listas enlazadas son tales que cada bloque almacena dos elementos de información:
1. La información del mismo (e.g. el número que almacena).
2. La posición en la que se encuentra el siguiente bloque.

~~~mermaid

flowchart LR
	1 --> 42
~~~

Una lista enlazada comienza con un **nodo cabecera**: que no contiene información, si no que solamente contiene la información del primer elemento.
> Para acceder a la lista es necesario tener la información del primer nodo (el nodo de cabecera).

La implementación de los elementos se hace a través de una [[3 - Contenido/Programación/Python/1. Expresiones, Tipos y Variables/Clases|clase]].
Para definir un nodo se utiliza una clase con dos parámetros: `info` y `sgte`.
- `info` contiene el dato que contendrá la casilla de la lista.
- `sgte` contiene la ubicación del siguiente elemento.
se tiene entonces una clase de la forma:
```py
class Nodo:
	def __init__(self, info, sgte=None)
		self.info = info
		self.sgte = sgte
```
El método `__init__` instancia un nodo de tal forma que asigna los parámetros iniciados y, por defecto en la definición de la clase, se indica `None` como siguiente. Pues si se inicia solamente con información pero sin un nodo siguiente, se termina la lista enlazada, de la forma:
![[Pasted image 20260429192446.png]]
En la práctica, para crear una lista enlazada
```py
primero = Nodo(42, Nodo(52, Nodo(...) ) )
```
y para recorrer esta lista, se puede utilizar un ciclo `while` y almacenando el campo `sgte` del primero en una variable $p$, se puede acceder a los siguientes nodos si en cada iteración la variable $p$ se cambia por su mismo campo siguiente:
```py
primero = Nodo(42, Nodo(52, (...) ) )

p = primero.sgte

while (p != None):
	p = p.sgte
```
y termina cuando el campo siguiente del nodo actual sea `None`, o sea *el final de la lista*.

Para asociar a los nodos como una sola entidad, en una lista enlazada, se define una lista como clase. El único campo de esta clase será el primer nodo.
```py
class Lista_Enlz:
	def __init__(self, primero):
		self.primero = primero
```
el primer nodo es el único que importa pues este *contiene la información del siguiente nodo que, a su vez, contiene la información del siguiente* y así sucesivamente para toda la lista.

## Funciones
Las funciones para el procesamiento de listas enlazadas deben ser definidas nuevamente.

### Insertar dato al Inicio
Si se tiene un dato que se quiere insertar en el inicio de una lista enlazada existente:
1. Se debe encapsular la información dentro de un nodo
2. Se debe modificar el campo `sgte` del nuevo nodo de cabecera, apuntando al anterior nodo de cabecera.
```py
def insertar_al_inicio(self,info):
	self.primero = Nodo(info, self.primero)
```
en donde `info` será su propia información y en su campo `sgte` se almacena la información del anterior nodo cabecera.

### Agregar nodo después de otro
El nuevo nodo se inicia tal que 
- El campo `sgte` del nodo anterior a la posición donde se reemplaza, será la `info` del nodo insertado.
- El campo `sgte` *del insertado* es el campo `sgte` del nodo que reemplazó.

### Eliminar nodo al inicio
Primero se debe verificar que el nodo de cabecera no sea `None` pues así, no se tiene nada para eliminar.
Para eliminar un nodo al inicio simplemente hay que modificar el campo `sgte` del nodo de cabecera para que contenga al segundo nodo.