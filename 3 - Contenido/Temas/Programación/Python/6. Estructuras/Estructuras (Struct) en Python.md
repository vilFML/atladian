Una **estructura** es una agrupación de atributos, los cuales en conjunto representan algo más complejo. El dato creado se denomina *dato compuesto*.

En python se utiliza el módulo ` estructura.py`, con definiciones básicas para poder crear estructuras.

## Crear Estructuras

Para crear estructuras se utiliza la función `crear()` del módulo, en donde el primer parámetro será el *nombre de la estructura* y los parámetros siguientes son los *atributos o propiedades* que tendrá la estructura.

**Sintaxis:**
```py
import estructura

# 'Nombre de la estructura': 'atributo1(tipo)', 'atributo2(tipo)', ..., 'atributoN'
estructura.crear("Nombre de la estructura", "atributo1 atributo2 ... atribunoN")
```

- También se tienen contratos para estructuras, de la forma: 
	```py
	# 'nombre estructura': 'atributo1(tipo)', 'atributo2(int)'
	```
  
## Uso de la Estructura
Definir una estructura permite la creación de *un nuevo tipo* según Python, el cual puede ser reconocido con la función `type()`.
Para crear una variable con una estructura, se debe utilizar con sintaxis similar a una función: Se indica el nombre de la estructura y los atributos que tendrá entre paréntesis, de la forma:
```py
'variable' = 'Estructura'('atributo1', 'atributo2', ..., 'atributoN')
```

#### Acceso a Propiedades
Cuando se tiene una estructura, se puede acceder a los atributos o propiedades de ella con `'estructura'.'atributoX'`


## Validación de Estructuras
Las estructuras son solo una *agrupación de valores*, así que se es posible ingresar atributos que no son útiles para la estructura. 
Para prevenir ello, se deben validar precondiciones para que se cumpla la funcionalidad, lo que se conoce como *función validadora*.

##### Ejemplo: Modelar Fracciones
Un uso de estructuras es para modelar fracciones, pues una fracción se compone de una división entre *dos números enteros* (`int`) que, para sumarse con otra fracción, se tendrá un valor `float` aproximado. El problema se centra en que se entregan 4 `int` para representar la suma de fracciones, la cual será representada por un `float` y no una fracción.
Para modelar una fracción con un `struct`:

Las fracciones poseen dos atributos: *numerador* y *denominador*, ambos de tipo `int`.

Se utiliza la función `crear()` del módulo:
```py
import estructura

# Fraccion: numerador(int), denominador(int)
estructura.crear('Fraccion', 'numerador denominador')
```

La estructura define un 'molde' de cómo deben crearse las fracciones. Para crear fracciones se debe utilizar la estructura de forma similar a una función, indicando los atributos que se quiere que tengan:

```py
import estructura

estructura.crear('Fraccion', 'numerador denominador')

f1 = Fraccion(5,8)
f2 = Fraccion(1,2)
```

en `f1` se crea una fracción de numerador `5` y de denominador `8` y para `f2` una fracción con numerador `1` y denominador `2`, osea $f_{1} = \frac{5}{8}$ y $f_{2}=\frac{1}{2}$

Para acceder a un número de la fracción, se puede acceder a un atributo de la estructura `Fraccion`:

```py
import estructura

estructura.crear('Fraccion', 'numerador denominador')

f = Fraccion(5,8)

print(f.numerador)
print(f.denominador)
```

Por último, hasta ahora es posible entregarle un string, así que se deben verificar las precondiciones para asegurar que se tenga una fracción, creando la función `esFraccion` 


```py
# esFraccion: any -> bool
# devuelve True si es una fracción válida
# ej: esFraccion(Fraccion(1,2) devuelve True
# ej: esFraccion(Fraccion(1,0)) devuelve False
# ej: esFraccion('gato') devuelve False
def esFraccion(x):
	
	# validacion del tipo de estructura correcto (Fraccion)
	if type(x) != Fraccion:
		return False
	
	# validacion de tipos para los atributos
	if type(x.numerador) != int:
		return False
	if type(x.denominador) != int:
		return False
	
	# validacion de rango y dominio para atributos
	if x.denominador == 0:
		return False
	
	# si ninguna condicion restringida se cumple, entonces es una fraccion valida
	return True
```
en primer lugar, siempre es buena idea *verificar primero si el dato entregado es del tipo esperado* (osea de tipo `Fraccion`). Luego, se verifica que el numerador y denominador no sean distintos al tipo `int`.  Para todos los casos anteriores, si se cumplen termina la función devolviendo `False` y en caso de que no se cumplan las condiciones, se continúa hasta devolver `True` validando la fracción analizada.

# Inmutabilidad de Estructuras
Las estructuras no son mutables, una vez creado un dato compuesto **no es posible modificar su valor** a través del acceso a un atributo. Para modificar la estructura se debe *volver a crear el dato compuesto*.

##### Ejemplo:

```py
import estructura
estructura.crear('Fraccion', 'numerador denominador')

f = Fraccion(5,8)
f.numerador = 2
```
entrega un error, pues se está tratando de modificar un atributo de la estructura. En cambio, se debe hacer:

```py
import estructura
estructura.crear('Fraccion', 'numerador denominador')

f = Fraccion(5,8)

f = Fraccion(7, f.denominador)
```
en donde se modificó su numerador a `7` y se mantuvo el denominador con el atributo de la fracción antes creada.

# Módulo Fracción
Es una buena práctica guardar en el mismo archivo/módulo la definición de la estructura junto con las funciones que operan con este nuevo tipo de dato.

Se va a crear un módulo con funciones útiles que permiten operar con la estructura `Fraccion`:
- Validación de fración con `esFraccion()`
- Suma de fracciones con `suma()`
- Simplificación de fracción con `simplificar()`
- Calcular su valor decimañ
- Retornar string con la representación de la fracción.

```py
# suma: Fraccion, Fraccion -> Fraccion
# devuelve la suma de dos fracciones
# ej: suma(Fraccion(1,2),Fraccion(3,4)) entrega Fraccoin(10,8)
def suma(x,y):
	assert esFraccion(x)
	assert esFraccion(y)
	
	num = x.numerador * y.denominador + x.denominador * y.numerador
	den = x.denominador * y.denominador
	
	return Fraccion(num, den)

#tests
assert suma(Fraccion(1,2), Fraccion(3, 4)) == Fraccion(10, 8)
```

```py
import math

# simplificar: Fraccion -> Fraccion
# simplifica una fraccion dada
# ej: simplificar(Fraccion(2,4)) es Fraccion(1,2)
def simplificar(f):
	assert esFraccion(f)
	
	m = math.gcd(f.numerador, f.denominador)
	num = f.numerador // m
	den = f.denominador // m
	
	return Fraccion(num, den)

# tests
assert simplificar(Fraccion(2, 4)) == Fraccion(1, 2)
assert simplificar(Fraccion(7, 5)) == Fraccion(7, 5)
```

```py
# valorDecimal: Fraccion -> Fraccion
# entrega el valor decimal de una fracción
# Ej: valorDecimal(Fraccion(2,4)) entrega 0.5
def valorDecimal(f):
	assert esFraccion(f):
	return round(f.numerador / f.denominador, 2)

# tests
f1 = Fraccion(1,2)
f2 = Fraccion(1,3)

assert valorDecimal(f1) == 0.5
assert valorDecimal(f2) == 0.33
```

```py
# aTexto: Fraccion -> str
# devuelve un string con la fraccion dada
# ej: aTexto(Fraccion(1,2)) es '1/2'
def aTexto(f):
	assert esFraccion(f)
	return f'{f.numerador}/{f.denominador}

#tests
assert aTexto(Fraccion(1, 2)) == '1/2'
```



