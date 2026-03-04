Con las listas se pueden organizar datos de manera lineal, pero a veces se necesita agrupar de forma jerárquica y con más de alguna referencia recursiva.

Un **árbol binario** es una *estructura recursiva*, ya que puede definirse de la forma:

![[Pasted image 20260304174026.png]]

$$
\text{ABB} = 
\left\{
	\begin{array}{ll}
	\text{Vacio}, \text{si no contiene elementos (None)} \\
	\text{Arbol de un valor y enlaces a otros DOS arboles binarios}, \text{ si tiene elementos}
	\end{array}
\right.
$$

entonces un árbol contiene referencia a otros **dos** árboles binarios, que se les llama *izq* y *der* pues se refiere a un sub-árbol izquierdo y sub-árbol derecho en un diagrama:
![[Pasted image 20260304174711.png]]

Al igual que las listas, los árboles son *estructuras*:
```py
import estructura

# AB: valor(any), izq(AB), der(AB)
estructura.crear('AB', 'valor izq der')

# el arbol vacio se define como None
arbolVacio = None
```

- Al primer nodo de un ábol se denomina **raíz**: 
  ![[Pasted image 20260304175007.png]]

- A los nodos que *ambos* sub-árboles (izquierdo y derecho) referencian a un `arbolVacio`, se les denomina **hojas**.
  \* En diagramas los nodos vacíos (`arbolVacio` o `None`) se indican como círculos o cuadrados negros, aunque no se suelen dibujar las referencias a árboles vacíos: Se asume que al no salir ninguna flecha de un sub-árbol, éste corresponde a un `arbolVacio`.

Las funciones básicas que se realizan sobre un árbol son:
- Función validadora para determinar si un dato es árbol
- Contar cuántos nodos tiene
- Calcular la altura (o niveles de profundidad)
- Contar la cantidad de hojas
- Buscar si existe un elemento en un árbol.

## Dibujo de árboles

Los nodos se suelen de dibujar con esferas o cuadrados y las flechas que salen en su respectiva dirección representan la rama `izq` y `der`, como ejemplo:

![[Pasted image 20260304180642.png]]

que, representado en código es:

```py
raiz = AB(25, AB(16, AB(26, arbolVacio, arbolVacio), AB(31, AB(40, arbolVacio, arbolVacio), AB(5, arbolVacio, arbolVacio))), AB(9, AB(39, arbolVacio, arbolVacio), arbolVacio))
```
que es más legible de la forma:
```py
raiz = AB(25,
		AB(16,
			AB(26, arbolVacio, arbolVacio),
			AB(31,
				AB(40, arbolVacio, arbolVacio),
				AB(5, arbolVacio, arbolVacio))
			),
		AB(9,
			AB(39, arbolVacio, arbolVacio),
			arbolVacio
			))
```


## Funciones

### Verificar si es árbol

```py
# esAB: any -> bool
# indica si lo entregado cumple con ser AB
# ej: esAB(raiz) entrega True
def esAB(A):
	if A == arbolVacio:
	return True
	
	return type(A) == AB and esAB(A.izq) and esAB(A.der)

assert esAB(raiz)
```
en el *caso base* el `arbolVacio` se considera como árbol y en el *caso recursivo*, el nodo actual debe ser un árbol binario, y sus ramas `izq` y `der` también.

### Cantidad de elementos en un árbol
Para este caso se comienza desde la raíz del árbol.
- Si se tiene `arbolVacio`, no se cuenta como nodo y se retorna `0`.
- Si se tiene un `AB` no vacío, se cuenta y además:
  1. Se cuenta cuántos valores hay para la rama `izq` con la misma función
  2. Se cuenta cuántos valores hay para la rama `der` con la misma función.
  3. Se suman los resultados de ambas cuentas.


```py
# cantidadElementos: AB -> int
# cuenta cuantos nodos tiene el arbol
# ej: cantidadElementos(raiz) entrega 8
def cantidadElementos(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return 0
	else:
		return 1 + cantidadElementos(A.izq) + cantidadElemento(a.der)


assert cantidadElementos(raiz) == 8
```

-  En el **caso base**, un árbol vacío no se cuenta como un nodo con valores, entonces se retorna `0`.
- En el *caso recursivo* se cuenta el nodo actual y se aplica la misma función a la rama `izq ` y `der` del mismo nodo.

### Altura (nivel de profundidad) de un árbol
- Para el caso base, si se tiene `arbolVacio`, por definición se tiene altura `0`.
- Para el *caso recursivo*, si se encuentra con un `AB` no vacío, se cuenta como un nivel y además:
  1. Se calcula la altura del sub-árbol `izq` aplicándole la función.
  2. Se calcula la altura del sub-árbol `der` aplicándole la función
  3. Se considera la altura **mayor** entre ambas.

```py
# altura: AB -> int
# cuenta cual es la profundidad del arbol
# ej: altura(raiz) entrega 4
def altura(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return 0
	
	else:
		return 1 + max(altura(A.izq), altura(A.der))


assert altura(raiz) == 4
```

### Cantidad de hojas
- Como *caso base*: Si se tiene `None`, no es una hoja (ya que no tiene valor asociado)
- Y para *caso recursivo*, si se tiene un árbol no vacío:
  1. Si no tiene rama `izq` ni `der`, entonces se cuenta como hoja.
  2. Si tiene al menos una rama no nula, entonces se aplica la función a la hoja no nula.

```py
# hojas: AB -> int
# cuenta cuantos nodos sin ramas hay en el arbol
# ej: hojas(raiz) entrega 4
def hojas(A):
	assert esAB(A)
	
	if A == arbolVacio
		return 0
	
	elif A.izq == arbolVacio and A.der == arbolVacio:
		return 1
	
	else:
		return hojas(A.izq) + hojas(A.der)

assert hojas(raiz) == 4
```

### Buscar elemento en árbol
- Para el **caso base**, para un `arbolVacio`, no se tiene donde más buscar, entonces el elemento *no está*, retornando `False`.
- Para el **caso recursivo**, si se tiene un `AB` no vacío, se revisa si coincide con el elemento que se busca:
  1. Si coincide, se retorna `true`
  2. Si no coincide, se sigue buscando si existe en la rama `izq` o bien en la rama `der`, árboles aplicándoles la función.

```py
# buscar: AB any -> bool
# busca si existe el elemento buscado en el arbol
# ej: buscar(raiz, 40) entrega True
def buscar(A, elem):
	assert esAB(A)
	
	if A == arbolVacio:
		return False
		
	if A.valor == elem:
		return True
	
	return buscar(A.izq, elem) or buscar(A.der, elem)

assert buscar(raiz ,9)
assert buscar(raiz, 40)
assert not buscar(raiz, 99)

```

## Patrón de resolución con árboles

- El *caso recursivo* consiste en:
  1. Tomar el **elemento actual** y decidir qué se hace con el o cómo procesarlo
  2. Decidir si hay que procesar los elementos de alguna de sus ramas `izq` o `der` o ambas.
  3. Finalmente, entregar un resultado o continuar la recursión por alguna de las ramas en específico (o ambas)

```py
def funcionArbol(A):
	if A es arbolVacio:
		Ver que hacer en este caso
	
	if A es hoja:
		ver que se hace en este caso
	
	Extraccion del valor usando A.valor
	Realizar posibles acciones recursivas con rama izq y der
	... funcionArbol(A.izq)...
	... funcionArbol(A.der)...
	
	return resultado
```

y un patrón exhaustivo:

```py
def funcionArbol(A):
	if A es arbolVacio:
		Ver que hacer en este caso
		
	... A.valor ...
	
	if A.izq == arbolVacio and A.der == arbolVacio:
		ver que hacer en este caso
		
	if A.izq != arbolVacio and A.der == arbolVacio:
		... funcionArbol(A.izq) ...
	
	if A.izq == arbolVacio and A.der != arbolVacio:
		... funcionArbol(A.der) ...
	
	if A.izq != arbolVacio and A.der != arbolVacio:
		... funcionArbol(A.izq) ...
		... funcionArbol(A.der) ...
	
	return resultado
```
- En el primer caso base, se vé que se hace en el caso que tengamos un `arbolVacio`
- en el segundo caso base se vé que se hace en el caso que el nodo sea una hoja
-  en el caso recursivo se tienen:
  1. Solo existe la rama `izq`
  2. Solo existe la rama `der`
  3. Caso general donde existen ambas ramas.

# Arboles Binarios de Expresiones (AB-exp)
Los `AB-exp` son representaciones de expresiones matemáticas como cadenas de operaciones entre `int` y se va a tener que:
- Las hojas almacenan valores numéricos
- Los nodos interiores almacenan un `string` que representa la operación aritmética a realizar entre el valor de su rama `izq` y `der`
- No hay nodos con una sola rama (Todas las operaciones se realizan con dos operandos)
El objetivo es **obtener un valor numérico final** después de evaluar el árbol completo.


##### Ejemplo:
La operación matemática $((26-(40+5))*2)$ se representa con el siguiente `AB-exp`:
![[Pasted image 20260304185514.png]]
de la forma
```py
ABexp = AB('*',
			AB('-',
				AB(26, arbolVacio, arbolVacio),
				AB('+',
					AB(40, arbolVacio, arbolVacio),
					AB(5, arbolVacio, arbolVacio)
					)
				),
			AB(2, arbolVacio, arbolVacio))
```

## Funciones
### Validar Árbol Binario de Expresión

```py
# esABexp: any -> bool
# indica si un AB en particulas es AB-exp
# ej: esABexp(ABexp) entrega true
def esABexp(A):
	if not esAB(A):
		return False
	
	if A == arbolVacio:
		return False
	
	if A.izq == arbolVacio and A.der == arbolVacio:
		return type(A.valor) == int or type(A.valor) == float
	
	return type(A.valor) == str and esABexp(A.izq) and esABexp(A.der)

assert esABexp(ABexp)
assert not esABexp(raiz)
```

- El primer **caso base** corresponde a ver si el árbol no es un `AB`, entonces no puede ser un `AB-exp`.
- El segundo *caso base*: Un árbol vacío por sí solo no es un `AB-exp`
- El tercer *caso base*: El nodo es una hoja, entonces su valor debe ser numérico.
- El *caso recursivo*: Si es un nodo interior (ya que no es hoja), entonces su valor debe ser una operación y sus ramas deben ser `AB-exp`.

### Función para evaluar el resultado final

- Si es un nodo interior, entonces hay que evaluar el valor resultante de sus ramas `izq` y `der`, y luego operar sus resultados con la operación guardada en el nodo actual.
- Si es una hoja, entonce se entrega su valor asociado para que pueda ser operado más arriba en el árbol.
```py
# evaluar: ABexp -> num
# evalua el arbol de expresiones, entregando el resultado de la operacion
# ej: evaluar(A) entrega -38
def evaluar(A):
	assert esABexp(A)
	
	if A.izq == arbolVacio and A.der == arbolVacio
		return A.valor
	
	valorIzq = evaluar(A.izq)
	valorDer = evaluar(A.der)
	operador = A.valor
	
	if operador == '+':
		return valorIzq + valorDer
	elif operador == '-':
		return valorIzq - valorDer
	elif operador == '*':
		return valorIzq * valorDer
	elif operador == '/':
		return valorIzq / valorDer

assert evaluar(ABexp) == -38
```

# Árboles de Búsqueda Binaria (ABB)
Los Árboles de Búsqueda Binaria `ABB` son un caso particular de `AB` y es de los más utilizados. Está diseñado para que las búsquedas sean más rápidas al mantener sus *elementos bajo cierto orden*.
En este tipo de árboles:
* Todos los valores en la rama `izq` son **menores** que el valor en la raíz
* Todos los valores en la rama `der` son **mayores** que el valor en la raíz.
* Los sub-árboles de las ramas `izq` y `der` también cumplen lo anterior.
* Se asume que no hay valores repetidos (Hay ciertos tipos que los valores iguales deben estar siempre por una rama específica, usualmente la `der`).


##### Ejemplo
![[Pasted image 20260304191617.png]]
de código:
```py
ABB1 = AB(31,
		AB(16,
			AB(5,arbolVacio, arbolVacio),
			AB(25,
				AB(19, arbolVacio, arbolVacio),
				AB(26, arbolVacio, arbolVacio))
				),
			AB(40,
				AB(39, arbolVacio, arbolVacio),
				arbolVacio))
```

## Funciones
### Menor y Mayor
Como en un `ABB` los valores están ordenados, es mas sencillo encontrar el mayor o menor valor almacenado en el árbol.
En un `AB` tradicional, se tenía que buscar entre todos sus valores de forma exhaustiva, pero en un `ABB`:
- El *menor* valor se encuentra **en el nodo más profundo hacia la izquierda**.
- El *mayor* valor se encuentra **en el nodo más profundo hacia la derecha**.

```py
# menor: AB -> any
# entrega el menor valor de un ABB
# ej: menor(ABB1) entrega 5
def menor(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return arbolVacio
	
	if A.izq == arbolVacio:
		return A.valor
	else:
		return menor(A.izq)

assert menor(ABB1) == 5
```


```py
# mayor: AB -> any
# entrega el mayor valor de un ABB
# ej: mayor(ABB1) entrega 40
def mayor(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return arbolVacio
	
	if A.der == arbolVacio:
		return A.valor
	else:
		return mayor(A.der)

assert menor(ABB1) == 40
```
* Si no es puede seguir avanzando en la respectiva rama, entonces *el nodo actual* es el mayor o menor valor del árbol.
* Por ser `ABB`, si o si el valor menor o mayor debe estar en la rama `izq` o `der`, respectivamente.

### Verificar si un AB es ABB

- Por definición, un `arbolVacio` es `ABB`
- Si la rama `izq` no es vacío, se debe verificar que esta:
  1. Sea un `ABB`
  2. Su *mayor valor sea menor* que el valor de la raíz actual.
- Si la rama `der` no es vacía, se debe verificar que.
  1. Sea un `ABB`
  2. Su *menor valor sea mayor* que el valor de la raíz actual.

```py
# esABB: AB -> bool
# indica si un AB cumple con ser ABB o no
# ej: esABB(ABB1) entrega true
def esABB(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return True
	
	v = A.valor
	
	if A.izq == arbolVacio and A.der != arbolVacio:
		return True
	
	elif A.izq == arbolVAcio and A.der != arbolVacio:
		return esABB(A.der) and v < menor(A.der)
	elif A.izq != arbolVAcio and A.der == arbolVAcio:
		return esABB(A.izq) and v > mayor(A.izq)
	
	else:
		return esABB(A.izq) and esABB(A.der) and mayor(A.izq) < v and v < menor(A.der)

assert esABB(ABBej)
```


### Buscar un elemento en un ABB
Como ahora se tiene una relación de orden en los elementos del árbol, ahora en vez de realizar una búsqueda a través de todos los elementos, se puede realizar una búsqueda más eficiente:

- Si se tiene un `arbolVacio`, entonces el elemento *no estaba* en el árbol y se retorna `False`.
- Si es un nodo, se compara el elemento a buscar con el actual:
  1. Si es menor, entonces se continúa la búsqueda por la rama `izq`.
  2. Si es mayor, se continúa la búsqueda por la rama `der`.
  3. Si es igual, entonces se encontró y se retorna `True`.

```py
# enABB: ABB any -> bool
# determina si un elemento está en un ABB o no
 # ej: enABB (ABB1, 26) entrega True
def enABB (A, e):
	assert esABB (A)
	if A== arbolVacio:
		return False
	
	V = A. valor
	
	if e < v:
		return enABB (A.izq, e)
		
	elif e > v:
		return enABB (A.der, e)
	else:
		return True
```

### Función para agregar un nuevo elemento en un ABB
Como los árboles son estructuras no mutables, y dado que se está modificando el árbol, es necesario recrearlo con los cambios que se quiere realizar.
Debido a la propiedad de orden, solo existe un posible lugar en donde se puede insertar el nuevo elemento. Este lugar es el espacio vacío al que se llega luego de una búsqueda infructuosa, por lo que el procedimiento es:
1. Se realiza una búsqueda del elemento a agregar.
2. Cuando se encuentra un `arbolVacio`, entonces ese es el lugar en donde debiese haber estado el elemento, por lo que se agrega en ese espacio.

```py
# insertar: ABB any -> ABB
# entrega un nuevo ABB, con el nuevo elemento agregado
def insertar(A, e):
	assert esABB(A)
	
	if A == arbolVacio:
		return AB(e, arbolVacio, arbolVacio)
		
	v = A. valor
	
	if e < v:
	return AB(v, insertar (A.izq, e), A.der)
	
	elif e > v:
		return AB(v, A. izq, insertar (A.der, e))
	
	else:
		return AB(v, A. izq, A.der)
```

# Recorridos en un árbol AB
Se tienen distintas maneras de navegar en los elementos de un `AB`. Dependiendo de cómo se recorre, se pueden obtener distintos resultados, siendo los maś típicos: Pre-orden, In-orden y Post-orden

## Notación L-R-D
Una notación útil para entender los recorridos de árboles corresponde a **L-R-D**, que se refiere a:
* L: Left
* R: Right
* D: Data del nodo actual.

Un nodo del árbol quedará marcado con:
- Una letra **L** cuando quede esperando el llamado recursivo de su *rama izquierda*.
- Una letra **R** cuando quede esperando el llamado recursivo de su *rama derecha*.
- Una letra **D** cuando se procese el *contenido actual del nodo*.
Se sabrá que un nodo de un árbol se ha procesado completamente **cuando posee las tres letras L,R y D**.

## Recorridos
En cada función sólo va cambiando el orden en el que se procesa el nodo actual.
### In-Orden LDR
Se recorre en el orden:
1. Rama `izq` L
2. el nodo `D`
3. Rama `der` R

> Útil para obtener los elementos de un `ABB` ordenados de menor a mayor.

![[Pasted image 20260304195513.png]]

#### Imprimir elementos en Pre-orden

```py
# imprimirPreorden: AB -> None
def imprimir Preorden(A):
	assert esAB(A)
	
	if A== arbolVacio:
		return None
	
	print(A. valor)
	imprimirPreorden(A.izq)
	imprimirPreorden(A.der)
```


### Pre-orden DLR
Se recorre en el orden:
1. El nodo `D`
2. Rama `izq`
3. Rama `der`
![[Pasted image 20260304195553.png]]

#### Imprimir elementos en In-orden

```py
# imprimirInorden: AB -> None
def imprimir Inorden(A):
	assert esAB(A)
	
	if A== arbolVacio:
		return None
	
	imprimirInorden(A.izq)
	print (A. valor)
	imprimirInorden(A.der)
```

### Post-Orden LRD
Se recorre en orden:
1. Rama `izq`
2. Rama `der`
3. El nodo `D`
![[Pasted image 20260304195640.png]]

#### Imprimir elementos en Post-Orden

```py
# imprimirPostorden: AB -> None
def imprimir Postorden(A):
	assert esAB(A)
	
	if A== arbolVacio:
		return None
	
	imprimirPostorden(A.izq)
	imprimirPostorden(A.der)
	print (A. valor)
```

# Transformar Árboles Binarios (AB) a Listas
Para crear una lista con el contenido de un `AB`, se va a seguir el recorrido *in-orden* y se va a ir 'pegando' las distintas listas de elementos que se van generando en cada una de las ramas.
1. Se genera *una lista* con el valor actual `Lactual`
2. Se obtiene *recursivamente* la lista con los valores de la rama `izq` (`Lizq`)
3. Se obtiene *recursivamente* la lista con los valores de la rama `der` (`Lder`)
4. Se junta `Lizq` con `Lactual` y el resultado de aquello se junta con `Lder` (en ese orden).

Luego `L` será:

| `Lizq`         | `Lactual` | `Lder`       |
| -------------- | --------- | ------------ |
| Rama izquierda | Actual    | Rama derecha |

```py
# ABaLista: AB -> lista
# convierte un AB a lista con sus elementos en inorden
# ej: ABaLista (ABB1) entrega lista(5, lista(16, lista(19, # lista(25,
# lista(26, lista(31, lista(39, lista(40, listaVacia))))))))
def ABaLista(A):
	assert esAB(A)
	
	if A == arbolVacio:
		return listaVacia
		
	Lactual = lista (A. valor, listaVacia)
	Lizq = ABaLista (A.izq)
	Lder = ABaLista (A.der)
	
	Lextendida = juntar (Lizq, Lactual)
	Lresultado juntar (Lextendida, Lder)
	return Lresultado
```

- En el *caso base*: Si se llega al `arbolVacio`, entonces se retorna `listaVacia`, ya que no hay elemento.
- En el *caso recursivo* se crea la lista con el elemento actual y luego se obtiene recursivamente las listas de los elementos de la rama `izq` y los de la rama `der`.
- Se juntan las listas en el orden apropiado (preorden)

# Árboles ABB de Estructuras
Tanto los árboles `AB` como `ABB` pueden ser estructuras, es decir, el valor de cada uno de sus nodos es entonces una estructura.
Para los árboles `ABB` de estructuras, debe existir un orden de acuerdo con *uno de los atributtos* de las estructuras.

Por ejemplo, para un árbol de canciones, se puede ordenar por nombre, artista o duración de la canción.

##### Ejemplo: ABB de estructuras Canción
En este caso el árbol está ordenado de acuerdo al nombre de las canciones:
\* Los strings se comparan de forma *lexicográfica*, en donde: `'A' < 'Z' < 'a' < 'z'`
![[Pasted image 20260304201339.png]]

```py
canciones = AB(imagine,
			AB(bohemianRhapsody,
			   arbolVacio,
			   AB(heyJude, arbol Vacio, arbolVacio)),
			AB(stopCryingYourHeartOut,
			   AB(karmaPolice,
				  arbolVacio,
				  AB(novemberRain, arbolVacio, arbolVacio)),
				arbolVacio))
```


## Buscar en ABB de Estrucura

```py
# buscarCancion: AB(Cancion), str -> bool
# busca si existe una canción en el arbol con el nombre
# ej: buscarCancion(canciones, "Hey Jude") entrega True
def buscarCancion(A, nombre):
	assert esABB(A)
	assert type(nombre) == str
	
	if A == arbolVacio:
		return False
	if nombre < A.valor.nombre:
		return buscarCancion(A.izq, nombre)
	elif nombre > A.valor.nombre:
		return buscarCancion(A.der, nombre)
	else:
		return True

assert buscarCancion(canciones, "Hey Jude") == True
assert buscarCancion(canciones, "One") == False
```

- **Caso Base**: En un `arbolVacio` no hay canciones por lo que se retorna `False`
- **Caso recursivo**: Recordar que ahora `A.valor` es una estructura, por lo que se debe extraer su nombre con la notación `A.valor.nombre`. Notar que se puede hacer una búsqueda con las propiedades de `ABB` debido a que el árbol de canciones está ordenado por nombre
