Se requiere entender los conceptos de
1. Funciones que se pueden entregar como parámetro a otras funciones
2. Funciones que no tienen nombre (Funciones Anónimas o Lambdas)
3. `If/else` en una sola línea (Operador Ternario Condicional)

# Tratamiento especial de Funciones en Python

## Almacenar Función en Variable

Las funciones se pueden almacenar en una variable. Lo que hace esto es darle un 'alias' (o apodo) adicional a la función. Por ejemplo:

```py
# suma: num, num -> num
# retorna la suma de dos numeros
# ej: suma(1, 2) retorna 3
def suma(x, y):
	return x + y
	
sumador = suma
```
en donde se guardó la función `suma()` en la variable `sumador`, tomándola como *alias*. Luego, invocar la función `suma()` o `sumador()` tiene el mismo efecto pues se invoca la misma función.

### Generalización de Operación de Números
Dentro de una función que recibe dos números como parámetros se pueden incluir las definiciones de funciones que hagan una resta, suma, multiplicación, etc. con éstos números. Y la forma de elegir qué operación se realiza *también se entrega como un parámetro a la función general*.
> La forma de generalizar la función es que reciba la función a invocar como parámetro.
Así no se necesita un condicional para determinar qué hacer y la función general invocará solamente la función en su interior que se entregue como parámetro.

![[Pasted image 20260305120338.png]]

luego, la función `operarNumerosGeneral()` se implementa de la forma:

```py
# operarNumerosGeneral: num, num, (f: num, num -> num) -> num
# retorna una operación matemática sobre a y b, determinada por funOp
def operarNumerosGeneral(a, b, funOp):
	return funOp(a, b)
```
en donde `funOp` es un **alias** de una función. Al estar guardado en una variable, se puede invocar y esta va a realizar las mismas funciones que la función original.

- Para probar la función `operarNumerosGeneral()` se deben tener funciones definidas que operen con dos valores para entregarlas como parámetro y realizar aserciones al resultado.
```py
# suma: num, num -> num
def suma(a, b):
	return a + b

# resta: num, num -> num
def resta(a, b):
	return a - b

# multiplicacion: num, num -> num
def multiplicacion(a, b):
	return a * b
```

```py
# operarNumerosGeneral: num, num, (f: num,num -> num) -> num
# retorna una operación matemática sobre a y b,
# determinada por funOp
def operarNumerosGeneral(a, b, funOp):
	return funOp(a, b)

assert operarNumerosGeneral(1, 2, suma) == 3

assert operarNumerosGeneral(1, 2, resta) == -1

assert operarNumerosGeneral(1, 2, multiplicacion) == 2

```
cada parámetro `'suma'`,`'resta'`, `'multiplicacion'` son `string` que se entregan a la función para que esta, a su vez, invoque a la función cuyo nombre coincida con el parámetro recibido.

***Nota***: Se tienen dos expresiones que parecen iguales, pero realizan operaciones distintas:
1. entregar el `string` `'suma'` invoca la función `suma()`
2. entregar la función `suma()`, lo que entrega a la función *la suma aritmética* de los números indicados.

# Funciones Anónimas (lambdas)
Una función **anónima o lambda** es una función pequeña y compacta **sin nombre**, que reciben parámetros y *retornan la evaluación de una expresión*:
```py
lambda x, y, ..., z: expresion
```

- `lambda` es una palabra reservada en Python que denota que se va a crear una función anónima.
- `x, y, z` son los parámetros que recibe la función anónima
- La expresión corresponde a *la operación* que se realiza con los parámetros, cuyo resultado se entrega al ejecutar la función.

Las funciones lambda son anónimas y, por lo tanto, no tienen nombre. La única forma en que 'tengan un nombre' es guardarlas en una variable. Y estas siempre (y de forma automática) siempre retornan la evaluación de la expresión y no requieren tener `return`.
\* Las funciones lambda no necesitan receta de diseño

## Funciones Equivalentes
Una función anónima es equivalente a otra función, de la forma:
```py
unaFunción = lambda x, y, ..., z : expresion
```
es **equivalente** a:
```py
def unaFuncion(x,y,...,z):
	return expresion
```

## Uso
Se puede reescribir la función `operarNumerosGeneral` de la forma:
```py
suma = lambda x, y: x + y
resta = lambda x, y: x - y
multiplicacion = lambda x, y: x * y

# operaNumerosGeneral: num, num, (f: num,num -> num) -> num
def operarNumerosGeneral(a, b, funOp):
	return funOp(a, b)

assert operarNumerosGeneral(1, 2, suma) == 3
assert operarNumerosGeneral(1, 2, resta) == -1
assert operarNumerosGeneral(1, 2, multiplicacion) == 2

```
en donde se definen las funciones suma, resta y multiplicación usando funciones lambda. En este caso, la ventaja es que no se requiere escribir la receta de diseño.

- Las funciones lambdas son funciones *'simples y desechables'*, es decir son para un uso en particular y después no son reutilizadas en el código. Por esto, son especialmente *útiles para ser entregadas como argumentos a funciones*, ya que su propósito de creación es específico para otra función.

##### Ejemplo
La versión final de `operarNumerosGeneral`, usando funciones lambda, queda:
```py
# operaNumerosGeneral: num, num, (f: num,num -> num) -> num
def operarNumerosGeneral(a, b, funOp):
	return funOp(a, b)

assert operarNumerosGeneral(1, 2, lambda x, y: x + y) == 3
assert operarNumerosGeneral(1, 2, lambda x, y: x - y) == -1
assert operarNumerosGeneral(1, 2, lambda x, y: x * y) == 2
```
en donde se utiliza la función lambda al invocar otras funciones como parámetro (sin necesariamente darle un nombre). Así, estas funciones sólo tienen sentido en el contexto de la función `operarNumerosGeneral`.

# Operador Ternario Condicional
El **operador ternario** también se llaman **expresiones condicionales** . En Python permite retornar un determinado valor dependiendo si *una condición* es `True` o `False`.
Es útil si se quiere asignar un valor a una variable dependiendo de una condición, o bien, *usar condiciones en funciones lambda*.
- Se puede definir como un `if-else` compacto, de una sola línea.
**SINTAXIS:**
```py
"Valor a retornar con True" if "condicion" else "valor a retornar con False"
```


##### Ejemplo:
```py
a = 10
b = 20

if a > b:
	mensaje = "a es mayor que b"
else:
	mensaje = "a es menor que b"

print(mensaje)
# Se muestra "a es menor que b"
```
es equivalente a:
```py
a = 10
b = 20

mensaje = "a es mayor que b" if a > b else "a es menor que b"

print(mensaje)
# Se muestra "a es menor que b"
```
el mensaje se puede leer como:
	Asigna a la variable `mensaje` el string `'a es mayor que b` si se cumple que `a > b`. Si no, asigna a `mensaje` el string `'a es menor que b'`.

# Función equivalente en funcion lambda

Una de las ventajas del operador ternario condicional es su uso en funciones lambda condicionales:
```py
# esPar: num -> bool
# verifica si el número es par
# ej: esPar(77) entrega False
def esPar(n):
	if n % 2 == 0:
		return True
	else:
		return False

assert not esPar(77)
```
es equivalente a:
```py
esPar = lambda n: True if n % 2 == 0 else False

# o de forma equivalente

esPar = lambda n: n % 2 == 0
```

# Abstracción Funcional
Una forma de generalizar funciones es diseñarlas tales que permiten recibir funciones como parámetro. Con ello, la función no está ligada a resolver un solo problema en particular (y para datos/estructuras con una forma estricta), si no que se otorga una flexibilidad con la capacidad de 'inyectar' código a través de funciones externas.

La **abstracción funcional** es encapsular procesos y lógica al interior de funciones y combinarlas entre ellas para solucionar problemas más complejos. Al hacerlo se tienen los beneficios de:
- Prevenir la duplicación de código similar
- Extender el rango o dominio en donde puede operar una función
- Se pueden realizar rápidamente operaciones típicas al operar con datos (como filtrar o buscar algo en una lista de elementos).



##### Ejemplo:
Se puede visualizar esto en una función que recibe dos estructuras de animales y retorna `True` si son iguales o `False` si no. La igualdad debe hacerse bajo cierto criterio y no necesariamente con todos los atributos de la estructura (por ej. no importa si el animal tiene hambre)

```py
# igualdadAnimales: Animal, Animal -> bool
# indica si dos animales son iguales de acuerdo a nuestros criterios
# ej: igualdadAnimales(perrito, gatito) entrega False
def igualdadAnimales(animal1, animal2):
	assert esAnimal(animal1) and esAnimal(animal2)
	
	if (animal1.nombre == animal2.nombre and
		animal1.tipo == animal2.tipo and
		animal1.edad == animal2.edad):
		return True
	else:
		return False

perritoSinHambre = Animal("Linky", "perro", 1, False)
perritoConHambre = Animal("Linky", "perro", 1, True)
assert igualdadAnimales(perritoSinHambre, perritoConHambre)

```
en donde se usa el criterio de igualdad tal que dos animales son iguales si tienen el mismo `nombre`, `tipo` y `edad`; no importa `hambre`.

Ahora se puede crear la función que opera con listas de estructuras `Animal` usando la función anterior `igualdadAnimal()` en vez del operador de igualdad `==`. 

```py
# contieneAnimal: lista(Animal), Animal -> bool
# indica si el Animal existe en la lista de Animales
# ej: contieneAnimal(LAnimales, gatito) entrega True
def contieneAnimal(L, animal):
	assert esLista(L)
	assert esAnimal(animal)
	
	if L == listaVacia:
		return False
	else:
		actual = cabeza(L)
		if igualdadAnimales(actual, animal):
			return True
		else:
			return contieneAnimal(cola(L), animal)
```
La función `igualdadAnimales()` recién creada determina si dos animales son iguales o no, de acuerdo al criterio indicado.

Pero se tiene un problema: la función `contieneAnimal()` está ligada a la estructura de tipo `Animal`. Entonces la funcionalidad de buscar algún elemento en una lista de estructuras está restringida al tipo específico de estructuras con la forma de `Animal`. Para solucionar esto, se entrega como parámetro la función de igualdad, lo que permite tener distintos criterios de igualdad y *generalizar* la función `contiene` a distintas estructuras:
```py
# contieneEst: lista(any), any, (f: any,any -> bool) -> bool
# indica si el elemento e existe en la lista L
# ej: contieneEst(LAnimales, gatito, igualdadAnimales) entrega True
def contieneEst(L, e, funIgualdad):
	assert esLista(L)
	
	if L == listaVacia:
		return False
	else:
		actual = cabeza(L)
		if funIgualdad(actual, e):
			return True
		else:
			return contieneEst(cola(L), e, funIgualdad)

```
ahora *se recibe una función igualdad* definida por el usuario, que toma dos parámetros y dice si dos elementos son iguales.
En el bloque `else:` se invoca la función igualdad entregada como parámetro (sea de la forma que sea, esta debe funcionar para dos argumentos).

## Abstracciones Funcionales
Las tres mśa importantes son:
1. Filtro / filter
2. Mapa / map
3. Reductor / reduce / fold

### Función Filtro (filter)
