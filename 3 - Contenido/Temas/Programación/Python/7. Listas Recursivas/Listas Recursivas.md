Con estructuras se pueden agrupar valores y representar tipos de datos compuestos. También se quisiera enumerar y agrupar elementos *que compartan un mismo contexto*. Para ello se utilizan *listas recursivas*.

Una [[lista]] puede tener un largo arbitrario, o sea una cantidad finita de elementos pero *indeterminada*.

# Lista
La definición de una lista puede hacerse de forma **recursiva**, de la forma:
$$
\text{Lista} = 
\left\{
	\begin{array}{ll}
	\text{Vacia}, \text{si no contiene elementos} \\
	\text{Compuesta por un valor y un enlace a una Lista}, \text{ si tiene elementos}
	\end{array}
\right.
$$

## Definición como Estructura (Lista de Nodos)

También se puede definir una lista como una **estructura** que posee dos atributos:
1. `valor`: Que almacena el dato que contiene la lista.
2. `siguiente`: Que almacena una *referencia o enlace* al resto de la lista.

```py
import estructura

# lista: valor(any), siguiente(lista)
estructura.crear('lista', 'valor siguiente')

# La lista vacía se define como None
listaVacia = None
```
así una lista se define como una recursión de listas en donde un elemento de ella se compone de un elemento, seguido de una lista. Esto se cumple para cada elemento de la lista, hasta llegar hasta el último elemento de la lista, el cual corresponde, a su vez, a una lista compuesta por dicho elemento y una lista vacía, terminando la definición por recursión.

En resumen,
> Una lista es una unión de nodos, donde cada nodo es una lista que contiene un elemento y el siguiente nodo.



##### Ejemplo:
Si se quiere crear una lista con los números 7, 4, 25 y 2, y posteriormente guardarla en una variable `L`, se escribe:
```py
L = lista(7, lista(4, lista(25, lista(2, listaVacia))))
```
en donde `listaVacia` es equivalente a `None`, entonces también se puede reemplazar.

![[Pasted image 20260304122348.png]]
que también se puede visualizar de forma simplificada como *una lista de nodos*, todos unidos entre sí:
![[Pasted image 20260304122456.png]]

# Módulo Lista
Por comodidad, se encapsula la creación de listas como estructuras en un módulo, incluyendo funciones típicas de ellas:
- Función validadora de listas.
- Obtener el primer elemento de una lista.
- Obtener el resto de la lista.
- Obtener el largo de la lista (cuántos elementos tiene)

> Se va a trabajar con un patrón común para funciones que trabajan con listas: Un caso base que analiza qué hacer con la *lista vacía* y el caso recursivo es tomar el elemento actual (la 'cabeza' de la lista), procesarlo y continuar con el siguiente elemento (la 'cola' de la lista)
El patrón general es:
```py
# procesarLista: lista, ... -> ...
# ...
def procesarLista(L, ...):
	# Precondiciones (verificar tipo correcto obtenido)
	
	# Caso base: analisis de lista vacia
	if L es ListaVacia:
		# Procesar que hacer con caso base
	
	else:
		Extraer la cabeza de la lista (valor actual)
		Procesar cabeza de lista
		Continuar recursivamente con procesarLista(cola(L), ...)
```


## Función esLista()
Se quiere una función que verifique si el elemento es del tipo Lista, de forma que el uso principal es a modo de precondición en funciones que reciban una lista como dato. Es importante notar que solo se analiza el elemento entregado y, en caso de que corresponda a una lista, no se van a analizar los elementos dentro de ella. Entonces ésta puede tener o no elementos dentro de ella.

```py
# esLista: any -> bool
# Retorna True si el dato es de tipo lista (tenga o no elementos)
# en caso contrario devuelve False
def esLista(L):
	# caso en que la lista sea vacia
	if L == listaVacia:
		return True
	
	# sino, se pregunta si el nodo actual es una lista, y que lo que
	# siga sea lista tambien de forma recursiva
	return type(L) == lista and esLista(L.siguiente)

# tests
assert esLista(lista(1, listaVacia))
assert esLista(listaVacia)
```
el *caso base* corresponde a que `listaVacia` es una lista, entonces se retorna `True`. El *caso recursivo* es donde se valida que lo actualmente analizado (`lista` y `L.siguiente`) sea del tipo `Lista`


## Función cabeza()
Con la función `cabeza()` permite *obtener el primer elemento de una lista*.

Para una lista vacía, se define que su primer elemento retorna una lista vacía (`None`). 

```py
# cabeza: lista -> any
# Entrega el primer valor de una lista
# En caso de ser una lista vacia, retorna una lista vacia
# EJ: cabeza(lista('a', lista('b', listaVacia)) entrega 'a'
def cabeza(L):
	assert esLista(L)
	
	if L == listaVacia:
		return listaVacia
	
	return L.valor

# tests
assert cabeza(lista('a', lista('b', listaVacia))) == 'a'
assert cabeza(listaVacia) == listaVacia
```

> Para obtener el `valor` se usa la función `cabeza()` y no el atributo `'lista'.valor` pues la función sabe cómo actuar con listas que tienen y no tienen elementos.

## Función cola()
Con la función `cola()` permite obtener el resto de la lista, o sea lo que está contenido en el atributo `siguiente` de la lista analizada.

Como *caso base* se define el resto de una listaVacia, lo cual debe entregar una `listaVacia`

```py
# cola: lista -> lista
# Entrega una lista sin el primer elemento de la lista entregada
# En caso de ser una lista vacia, retorna una lista vacia
# ej: cola(lista('a', lista('b', listaVacia))) entrega lista('b',listaVacia)
def cola(L):
	assert esLista(L)
	
	if L == listaVacia:
		return listaVacia
	
	return L.siguiente

# tests
assert cola(lista('a', lista('b', listaVacia))) == lista('b', listaVacia)
assert cola(listaVacia) == listaVacia
```

 Para obtener el `siguiente` de una lista, se utiliza la función `cola()` definida y no el atributo de la lista `'lista'.siguiente` pues la función maneja listas con elementos y sin elementos.
> Para obtener elementos dentro de una lista se utiliza la función `cola()` recursivamente, con tantas llamadas como posiciones en la lista se quiere recorrer.

## Función largo()
Para obtener el número de elementos en una lista se utiliza la función `largo()`, tal que:
```py
# largo: lista -> int
# entrega cuantos elementos tiene una lista
# ej: largo(lista(5, lista(4, listaVacia))) entrega 2
def largo(L):
	assert esLista(L)
	
	# si la lista es la vacia, tiene largo 0
	if L == listaVacia:
		return 0
	
	# si no, se cuenta el elemento actual y se continua con el resto
	return 1 + largo(cola(L))

# tests
assert largo(lista(5, lista(4, listaVacia))) == 2
assert largo(listaVacia) == 0
```

# Listas de Estructuras

Al momento de definir las listas, se declara que pueden contener cualquier tipo de dato en su interior. En particular, las listas *pueden almacenar estructuras* en su interior. 

```py
import estructura

estructura.crear('nombreEstructura', 'atributo1 atributo2 ... atributoN')

LdeEstructuras = lista( estructura1, lista( estructura2, lista(estructura3, listaVacia)))

```

Luego, para realizar algún proceso con las estructuras en la lista, es necesario 'preguntar' por sus atributos.