Al momento de implementar algoritmos, se deben notar las maneras en que se almacena la información. Por ahora, se han visto listas de números que no se sabe realmente cómo se almacenan en la memoria.

# Memoria RAM
La memoria RAM es un 'repositorio' o espacio físico para almacenar información.

# Arreglos
Un arreglo es una representación secuencial de una secuencia de datos, y  se almacena contigua físicamente en la memoria RAM del computador.

# Listas
En una lista de tamaño $n$, se asignan $n$ espacios en la memoria. Cuando se agregan elementos y es necesario agrandar la lista, Python crea una nueva lista vacío con el doble de tamaño ($2n$) y copia los elementos a ella. Cuando la lista pierde elementos y queda de la mitad del tamaño, se hace el mismo proceso, pero con una lista nueva de tamaño $\frac{n}{2}$.

# Listas Enlazadas

Cuando se usa un arreglo de 100 millones de datos en Python, este le dice al sistema operativo que reserve 100 millones de bloques en la memoria. Es evidente que no siempre habrá tal cantidad de bloques de memoria contiguas, pero sí puede ser que hayan de forma separadas.  Para ello, se utilizan *listas enlazadas*.

## Nodo

Las listas enlazadas se componen de **nodos**, que corresponden a bloques que almacenan dos elementos de información, llamados *campos*:
1. La información del mismo (e.g. el número que almacena).
2. La posición en la que se encuentra el siguiente bloque.

La implementación de los **nodos** se hace a través de una [[3 - Contenido/Programación/Python/1. Expresiones, Tipos y Variables/Clases|clase]] con dos parámetros: `info` y `sgte`.

```py
class Nodo:
	def __init__(self, info, sgte=None)
		self.info = info
		self.sgte = sgte
```
- `info` contiene el dato que contendrá la casilla de la lista.
- `sgte` contiene la ubicación del siguiente elemento.

El método `__init__` instancia un nodo de tal forma que asigna los parámetros iniciados y, por defecto en la definición de la clase, se indica `None` como asignación en el campo siguiente, creando un nodo aislado.

![[nodo.svg]]
El nodo es la figura completa, el campo izquierdo es la información del elemento y el campo derecho es *el puntero hacia el siguiente nodo*.
## Lista Enlazada

Una lista enlazada puede comenzar directamente con un nodo o con un nodo *sin información* conocido como **nodo cabecera**, el cual solamente contiene el puntero al primer elemento. Este nodo es útil para simplificar funcionalidades para las listas enlazadas.
> Para acceder a la lista es necesario tener la información del nodo cabecera.

![[linkedList-Gral3.svg]]

Luego, una lista enlazada corresponde a almacenar en una sola entidad *nodos anidados*. Entonces, para crear una lista, se crean clases recursivamente:
```py
primero = Nodo(42, Nodo(65, Nodo(13, Nodo(44))))
```
Si se instancia un nodo solamente con información pero sin un nodo siguiente, se termina la lista enlazada.
![[Pasted image 20260501114951.png]]

Para recorrer la lista creada, se puede utilizar un ciclo `while` y almacenando el campo `sgte` del primero en una variable $p$, se puede acceder a los siguientes nodos si en cada iteración la variable $p$ se cambia por su mismo campo siguiente:
```py
primero = Nodo(42, Nodo(52, (...) ) )

p = primero.sgte

while (p != None):
	p = p.sgte
```
y termina cuando el campo siguiente del nodo actual sea `None`, o sea *el final de la lista*.

Para asociar a los nodos en una sola entidad, en una lista enlazada, estas se definen como una clase. El único campo de esta clase será el nodo cabecera, necesario para acceder a la lista.
```py
class Lista_Enlz:
	def __init__(self):
		self.cabecera = Nodo(0,None)
```
el primer nodo es el único que importa pues este *contiene la información del siguiente nodo que, a su vez, contiene la información del siguiente* y así sucesivamente para toda la lista. 
Cuando se instancie la lista enlazada, se almacena en el nodo de cabecera la información de los nodos siguientes, pero por defecto, este estará vacío para tener una lista vacía.
### Funciones
Las funciones para el procesamiento de listas enlazadas deben ser definidas nuevamente.

#### Insertar dato al Inicio
Si se tiene un dato que se quiere insertar en el inicio de una lista enlazada existente:
1. Se debe encapsular la información dentro de un nodo invocando la clase `Nodo()`:
	   ```py
	   nuevoPrimero = Nodo('nro que se quiere almacenar', )
	   ```
2. Se debe modificar el campo `sgte` de este nuevo nodo creado, para apuntar al anterior primer nodo. Esto estaba almacenado en el campo `sgte` del nodo cabecera:
   ```py
   nuevoPrimero = Nodo('numero',self.cabecera.sgte)
   ```

El proceso corresponde a una función dentro de la clase `Nodo`:
```py
def insertar_al_inicio(self,info):
	self.cabecera.sgte = Nodo(info, self.primero)
```
se actualiza el campo `sgte` del nodo de cabecera, pues el nodo creado será el nuevo primer nodo, para el cual su propio campo `sgte` apunta al que es el primer nodo antes de que se ejecute la función.

![[linkedList-addFirst.svg]]

#### Agregar nodo después de otro
Definiendo como $p$ al nodo anterior al que se insertará:
1. El campo `sgte` de $p$, será la `info` del nodo insertado.
2. El campo `sgte` *del insertado* es el campo `sgte` del nodo que reemplazó. Este puntero va hacia el siguiente elemento antes de que se ejecute la función.

```py
def insertar_despues_de(self,p,info):
	p.sgte = Nodo(info,p.sgte)
```


![[linkedList-addNew.svg]]

#### Eliminar nodo al inicio
1. Primero se debe verificar que el campo siguiente del nodo cabecera no sea `None` pues así, no se tiene nada para eliminar:
   ```py
   ...
   assert (self.cabecera.sgte is not None)
   ...
   ```

2. Simplemente hay que modificar el campo `sgte` del nodo de cabecera para redireccionarlo al segundo nodo.
   ```py
   ...
   self.cabecera.sgte = self.cabecera.sgte.sgte
   ...
   ```

la función queda:
```py
def eliminar_al_inicio(self):
	assert (self.cabecera.sgte is not None)
	self.cabecera.sgte = self.cabecera.sgte.sgte
```
   ![[linkedList-deleteFirst.drawio.svg]]

#### Eliminar siguiente de otro
Definiendo $p$ como el nodo al que se le eliminará su nodo siguiente, se tienen:
1. Verificar que $p$ tenga efectivamente un nodo siguiente para eliminar:
   ```py
   ...
   assert (p.sgte is not None)
   ...
   ```
2. Modificar el puntero de $p$ para apuntar al nodo sub-siguiente, saltándose el que se quiere eliminar:
   ```py
   ...
   p.sgte = p.sgte.sgte
   ...
   ```

Y la función es
```py
def eliminar_despues_de(self,p):
	assert (p.sgte is not None)
	p.sgte = p.sgte.sgte
```

#### Retornar k-esimo elemento
Para recorrer la lista se utiliza una iteración sobre los punteros. Se inicia el iterador sobre el puntero del nodo cabecera y luego este va pasando por todos los punteros hasta que se llegue al nodo $k$ buscado.
```py
def k_esimo(self,k):
	p = self.cabecera
	j = 0
	while (p is not None):
		if (j==k):
			return p
		p=p.sgte
		j+=1
	return None
```

#### Obtener valores
La información de una lista enlazada está capturada en una estructura de datos particular, que se debe acceder con la palabra clave `yield` de Python, en donde se estará almacenando cada elemento al que se le aplica `yield` en una lista interna, para luego ser utilizada. Entonces, usando una iteración sobre los campos `info` de cada nodo:
```py
def valores(self):
	p = self.cabecera.sgte
	while (p is not None):
		yield p.info
		p = p.sgte
```

####
Imprimir valores
Para imprimir los valores de una lista enlazada, estos se deben almacenar en una lista interna en la cual se le aplica la función `print()` a cada elemento de ella (por ej. con una iteración). Esto se realiza con `yield` sobre cada elemento:
```py
def valores(self):
	p = self.cabecera.sgte
	while (p is not None):
		yield p.info
		p = p.sgte

L = lista_con_cabecera()

for x in L.valores()   # Una lista
	print(x, end=' ')

print([x for x in L.valores()])   # Un array
```

# Lista de Doble Enlace
En las listas de un enlace, cuando se está en cierto nodo no es posible acceder a la información del nodo anterior. Para ello, se debiese siempre empezar a recorrer la lista desde el inicio hasta el nodo que se busca, por eso se introducen las listas de enlace doble.
Las listas de enlace doble agregan un campo a los nodos que apunta hacia el nodo anterior a ellos.
![[Pasted image 20260502135345.png]]
Se tiene entonces una definición de la case `Nodo` con un campo adicional:
```py
class Nodo:
	def __init__(self, prev, info, sgte):
		self.prev = prev
		self.info = info
		self.sgte = sgte
```

Para el nodo de cabecera se agrega como campo `prev` el último nodo de la lista, y para este último, se elige como campo `sgte` la cabecera. Se tiene así una lista cíclica, aunque conceptualmente no lo es.
![[Pasted image 20260502140138.png]]

> Una lista de doble enlace vacía es aquella que su nodo cabecera tiene sus ambos enlaces `prev` y `sgte` apuntando hacia él mismo.

Luego, para crear una lista de doble enlace:
```py
class Lista_doble_enlace:
	def __init__(self):
		self.cabecera = Nodo(None,0,None)   #instanciar cabecera sin enlaces
		# se asignan los punteros a sí mismo
		self.cabecera.prev = self.cabecera
		self.cabecera.sgte = self.cabecera
```

## Funciones
### Insertar nodo
```py
def insertar_despues_de(self,p,info): # inserta después de nodo p
	r = p.sgte
	p.sgte = r.prev = Nodo(p,info,r)
```
