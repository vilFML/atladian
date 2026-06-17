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

### Eliminar nodo
Se debe evitar eliminar un nodo cabecera, pues si se tiene lista vacía, no hay nada que eliminar; y si es una lista válida, eliminar el nodo cabecera hace perder el acceso a la lista.
```py
assert p is not None
```
Luego, se *actualizan los punteros de los nodos vecinos* para 'saltarse' el que se elimina.
1. Para acceder al nodo siguiente a $p$: `p.sgte` y al anterior `p.prev`
   - Para acceder a los *punteros* de los nodos vecinos
     * el siguiente al nodo anterior `p.prev.sgte`,
     * y el anterior al nodo siguiente `p.sgte.prev`.
1. Reemplazar los punteros de los nodos vecinos entre ellos mismos.

La función queda
```py
def eliminar(self,p):
	assert p is not None
	p.prev.sgte = p.sgte   # puntero del anterior al siguiente
	p.sgte.prev = p.prev   # puntero del siguiente al anterior
```

# Árboles Binarios
Las listas son estructuras de datos lineales y tienen la limitación de que para acceder a los elementos, se debe pasar por todos los anteriores,
Una alternativa es usar una estructura de forma jerárquica, formando gráficamente un árbol. Ahora, para cada nodo se pueden tener ambos enlaces apuntando a otros nodos y se les pone nombre jerárquico: De un nodo *padre* salen dos nodos *hijos*: izquierdo y derecho, que, a su vez, pueden ser padres de otros dos nodos.
![[Pasted image 20260504084501.png]]
> Cada nodo puede tener, a lo más, dos hijos.

Los árboles binarios son similares a las listas de doble enlace, pero la diferencia es que la información (sus datos) son jerárquicos y los punteros de cada nodo pasan a ser `izq` y `der`. 
![[Pasted image 20260504084521.png]]
El nodo 'inicial' se llama *nodo raíz* y los circulares (incluyendo la raíz) se llaman *nodos internos*. Los cuadrados son nodos vacíos y se llaman *externos*.
Así, la clase `Nodo` tiene otra implementación:
```py
class Nodo
	def __init__(self, izq, info, der):
		self.izq = izq
		self.info = info
		self.der = der
```

Y se encapsula a los nodos interconectados en una sola entidad, como una clase `Arbol`. Similar a la instanciación de una lista.
```py
class Arbol:
	def __init__(self, raiz=None):
		self.raiz = raiz
```
por defecto se crea un árbol vacío, si no, cuando se instancia, se debe indicar el nodo raíz del árbol. 

> Similar al nodo cabecera para las listas, es el nodo raíz el que permite el acceso a la información del árbol.

## Ordenes

Con respecto al acceso a la información, hay *diferentes formas de recorrer un árbol*: **Pre, In y Post** orden.
En su base, *se llama la función de recorrer recursivamente* sobre los elementos del árbol, pero se diferencian en el orden de la recursión:
1. **Preorden**: Primero la raíz, luego el sub-árbol izquierdo y finalmente el sub-árbol derecho.
   ```py
   def pre(p):
	   if p is not None:
		   print(p.info, end=' ')   #1. raiz
		   pre(p.izq)               #2. subarbol izq
		   pre(p.der)               #3. subarbol der
   ```
   
2. **In orden**: Primero sub-árbol izquierdo, después la raíz y al final el sub-árbol derecho.
   ```py
   def ino(p):
	   if p is not None:
		   ino(p.izq)
		   print(p.info, end=' ')
		   ino(p.der)
   ```
   
3. **Post orden**: Se recorre primero los nodos hijos, de forma que primero se recorre el sub-árbol izquierdo, después el sub-árbol derecho y finalmente la raíz.
   ```py
   def post(p):
	   if p is not None:
		   post(p.izq)
		   post(p.der)
		   print(p.info, end=' ')
   ```
   

En cada nodo se tienen tres piezas de información: sub-árbol izquierdo, la raíz y el sub-árbol derecho. Y cada método difiere *en el orden* en que se accede a la información.
```py
def pre(p):
	if (p is not None):
		print(p.info, end=' ')
		pre(p.izq)
		pre(p.der)
```
y para generar la lista en Python:
```py
def pre(p):
	if (p is not None):
		yield p
		yield from pre(p.izq)
		yield from pre(p.der)
```

Para los nodos externos, es posible crear una clase para ellos en vez de que sean simplemente `None` (no tienen datos en `izq`,`der` o `info`). Si se implementa una clase, puede usarse `pass` para que no tenga funcionalidad o cambiarlo por alguna otra cosa. Con la clase de nodos externos ya no es necesario agregar el `assert` para verificar que el nodo actual sea `None`, pues, si se definen las funciones `pre`,`in` o `post` se agrega `Yield None` para que no entregue valores.
Por lo tanto, se tendrían dos clases:
```py
class Nodoi:
	def __init__(self, izq, info, der):
		# no hay variación
```
```py
class Nodoe:
	def __init__(self):
		pass
	def pre(self):
		yield None
	def in(self):
		yield None
	def post(self):
		yield None
```
y para el árbol, la función pre, in o post:
```py
def inOrden(self):
	print('In orden: ', end=' ')
	self.raiz.inorden()
	print()
```

# Tipos de Datos Abstractos

En Python se tienen tipos de datos internos. Los tipos de datos básicos son `int`,`float`,`bool`, que se denominan **tipos de datos primitivos** y para cada tipo ed dato se definen operaciones (e.g. para `int`: `+`,`-`, etc.)

Un **tipo abstracto de dato (TAD)** se construye en base a los tipos primitivos, estos almacenan un conjunto de datos y tienen operaciones para el conjunto; el dato también contiene sus operaciones del tipo.
Por ejemplo, una lista de Python `L = [1,2,3]`, que tiene operaciones `len(L)`,`L.append(x)`
La implementación de las operaciones de un TAD está hecha de alguna forma desconocida para un usuario, pues este solamente sabe cómo se utilizan las operaciones, estas son conocidas como **interfaz**.

## Pila (o Stack)
Una pila es un tipo abstracto de dato, y corresponde a una *colección de elementos* con funcionalidades particulares:
Las pilas tienen un **tope**, que corresponde al límite superior. Cuando se agrega un elemento, siempre se agrega por encima del tope; también cuando se saca, se eliminan desde el tope.

Se tienen las operaciones:
* para *insertar* un elemento en la pila: `push()`
* para *sacar*, eliminando el elemento de la pila (no se guarda): `pop()`
* Acceder a un elemento, *sin sacarlo*: `top`

La implementación se hace a través de una clase:
```py
class Pila:
	def __init__(self):
		self.s=[] # Se empieza una pila como una lista vacía.
		
	def push(self,x):
		self.s.append(x)   # viendolo como lista: se agrega elem al final
		
	def pop(self):
		assert len(self.s)>0
		return self.s.pop()   #simil de lista: se una fn 'pop'
```

Como la implementación de `append()` y `pop()` son desconocidos, se pueden tener ordenes de operaciones distintas a la esperada cuando se trabaja con estas funciones en una pila. De hecho, como Python crea nuevas listas según el tamaño de la que se va modificando, la complejidad de estas operaciones no son necesariamente del orden de $O(n)$.

Otra forma de implementación de una pila es en forma de arreglo (o array), lo que permite más control. Así, por ejemplo para hacer `push()`, se sabe en dónde se requiere agregar el elemento (en $n$) y también para `pop()` (se saca en $n-1$).
\* Como se tiene un array, la pila tiene un tamaño máximo cuando se instancia.

```py
class Pila:
	def __init__(self, maxn=100):
		self.n = 0   #n almacena la cant de elemento del array, inicio vacio
	def push (self,x)
		assert self.n<len(self.s)-1   #check si hay espacio para meter nro
		self.s[self.n] = x   # n tmb es la pos en dde se debiese insertar nuevo elemento
		self.n += 1   #se aumenta tmñ de array
		
```
La implementación de `push()` de esta forma permite contar la cantidad de operaciones para cierto número de elementos. Más control sobre la complejidad.

```py
def pop(self):
	assert self.n>0
	self.n -= 1   #n contaba que elem son parte de la pila
	return self.s[self.n]   #se indica cual es el que se saco
```
Esta implementación también permite contar la cantidad de operaciones para $n$, de hecho siempre son 3 operaciones y no depende del tamaño $n$ del array.

```py
def is_empty(self):
        return self.n==0
```

Para evitar el límite de tamaño se puede implementar la pila como una lista enlazada. Para ello es conveniente *definir el tope como el inicio de la lista enlazada*, pues ya se tiene las funcionalidades de insertar e insertar:
-  Para insertar se crea una nodo con campo `info` según lo que se quiera ingresar a la pila y el campo `sgte` se define apuntando al elemento que se encuentra actualmente (antes de ser insertado el elemento) en el tope.
- Para eliminar (`pop`) se cambia el campo `sgte` del tope al siguiente elemento.

### Aplicaciones
Al ejecutar en Python este primero verifica la sintaxis. Lo que hace es crear una pila que comienza a ingresar con `push` los caracteres en el código. Cuando encuentra el caracter que le corresponde al almacenado, elimina ambos con `pop` y así para cada elemento ingresado. Finalmente, la sintaxis es válida si la pila esta vacía.

También se pueden almacenar las operaciones de forma *post fijo*. Por ejemplo, una notación de una operación matemática es $(2*3)-(1*2)$, que se puede llevar a forma de árbol binario con los nodos como operaciones y luego recorrer el arbol en *post orden*:
$$
2,3,*,1,2,*,-
$$
esto en forma de pila indica que, luego de acumular números, estos se operan con el operador que se encuentre en un nodo.

#### Recorrido no recursivo de un árbol binario
Para pasar a una implementación iterativa, se debe pasar la recursividad a una forma compatible con hacer la [[Recursividad#Recursividad v/s Iteración|'traducción' a iteración]]:
Se pasa a forma *preorden*, en donde se hace push a la derecha primero y luego a la izquierda. Con ello se garantiza que el siguiente ciclo saque el elemento de la izquierda.