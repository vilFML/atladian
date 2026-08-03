De forma general, testing es la verificación empírica y objetiva de la calidad de un producto. En contexto de programación el producto son programas y sus funciones, y se verifica que la función cumpla y respete su contrato.
> No es práctico probar con todos los datos posibles. No obstante, se deben verificar los que sean representativos de su dominio.

- Probar funciones es crucial para garantizar un comportamiento correcto y eficiente del software, detectando errores antes de que se llegue a producción. Además facilita el mantenimiento pues permite realizar cambios sin riesgo a perder funcionalidades existentes. En consecuencia, se tendrá código de calidad, al considerar diferentes casos y escenarios posibles.

Para diseñar pruebas:
- En el contrato de cada función se limitan el tipo y cantidad de datos con los que hay que probar la función (e.g. `# maximo: num, num -> num`)
   **Se debe probar la función con el tipo y cantidad indicados en su contrato.** Y evitar pruebas redundantes (que prueben el mismo tipo de dato)
   
   Ejemplo:
   ```py
   # maximo: num, num -> num
   # devuele el mayor de dos numeros
   # ej: maximo(2,4) devuelve 4
   def maximo(a,b):
	   # ...
	
	# tests
	assert maximo(10, 20) == 20
	assert maximo(2, 'gato') == 2
	assert maximo(2, 4) == 4
	assert maximo (2, 4.7) == 4.7
   ```
   se puede ver que la segunda instrucción de `assert` va en contra del contrato, pues se está entregando como argumento un tipo de dato `string`, cuando se especifica que acepta de tipo `num`. Por otro lado, la tercera instrucción de `assert` es redundante con la primera prueba, pues se testean los mismos tipos de datos.
   
   
   
- **Probar con todos los distintos dominios permitidos**. Osea si se indica el tipo `num` se deben probar con dominios `float` e `int`. Además **para cada dominio, probar todos los casos límite (o borde)**.
   Ejemplo:
	```py
	# maximo: num, num -> num
	# ...
	
	# tests
	assert maximo(2, 3.6) == 3.6    # int con float
	assert maximo(-2, -8) == 8      # negativo con positivo
	assert maximo(7.3, 3.6) == 7.3  # float con float
	assert maximo (2, 2) == 4.7     # ambos numeros iguales
	assert maximo(0, -6) == 0       # comparación con cero
	```
	en donde se probaron valores de distinto dominio (`int` vs `float`) y casos borde dentro de éstos (ambos iguales, con cero, etc.)

# Assertions (afirmaciones)
`assert` es una palabra clave (o reservada) de Python, que verifica que la expresión escrita inmediatamente a su derecha sea evaluada a `True`.
La sintaxis es
```py
assert 'expresion' 'mensaje'
```
el mensaje luego de la expresión es opcional y permite mostrar un mensaje personalizado *en caso de error* y el programa termina en esa línea.

##### Ejemplo
```py
a = 7
assert a == 20, 'El valor de a no es 20'
```


#  Precondiciones
Las precondiciones son afirmaciones realizadas con `assert`, que se *ejecutan antes de realizar cualquier instrucción* al interior de una función.
En caso de que no se cumplan todas las precondiciones, la función terminará su ejecución sin ejecutar ninguna de sus instrucciones internas.
> Con las precondiciones es posible evitar la invocación de funciones con parámetros no válidos.

## Tipos de Verificación

1. Verificación de Tipos
	Se contrasta el tipo de datos que recibe una función con los tipos definidos en su contrato.
	
	Usando la función `type(n)`, que devuelve el tipo de dato de $n$, para verificar que un dato o una variable es de un determinado tipo, de la forma:
	```py
	a = 2
	type(a) == int
	```
	en donde `type(a)`devolverá `int` y entonces la expresión será `True`

2. Verificación de Dominio
	Verificación de que los valores estén en un determinado *dominio o rango*. Por ejemplo, que un valor numérico sea estrictamente positivo.

##### Ejemplo
Precondiciones a la función `maximo()`
1. Para la verificación de tipo, se quiere que los datos a recibir sean estrictamente numéricos, o sea de tipo `int` o `float`.
2. Para la verificación de rango no se tienen restricciones.

```py
# maximo: num, num -> num
# devuele el mayor de dos numeros
# ej: maximo(2,4) devuelve 4
def maximo(a,b):
	assert type(a) == int or type(a) == float, 'el primer dato no es numerico'
	asser type(b) == int or type(b) == float, 'el segundo dato no es numerico'
	
	return max(a,b)

# ...
```
Las precondiciones van al interior de la función y deben ser las primeras intstrucciones que se ejecuten para terminar la ejecución en caso de errores.

# Testing con Números Aleatorios

#### Ejemplo

```py
import random

# azar: None -> int
# devuelve un numero al azar entre 1 y 10
# ej: azar() puede entregar 3
def azar():
	return random.randint(1, 10)

# tests
test = azar()

assert type(test) == int
assert test <= 10 and test >= 1
```
primero se genera el valor aleatorio y se almacena en una variable para probarla. Luego, se puerba que el *tipo* de la variable sea correcto y después se testea que la variable *se encuentre en un determinado rango*.


# Testing a Funciones sin Retorno
Si una función no devuelve explícitamente un valor (o retornan el valor `None`)  no se puede testear.

# Testing con Números Reales (float)

Si se considera la suma entre `0.1` y `0.2`, se ve que el resultado es `0.300000000000000004`, luego hacer un `assert` a `0.3` retornará un error. Esto sucede pues el computador aproxima los valores de los números reales. Así, *no se puede representar directamente todos los números reales.*
Para afrontar el problema de la notación, se usa una notación en aritmética de punto flotante, definida en el [[estándar IEEE-754]]

Debido a la problemática de la precisión de números reales, se utiliza un **valor de tolerancia épsilon** y comprobar si el número está dentro de un cierto rango de error dado por épsilon. Entonces la idea es indicar que se está tolerando un margen de error entre el valor esperado y el devuelto por la función.
$$
|\text{Valor}_{\text{esperado}} - \text{Valor}_{\text{devuelto}}| \leq \varepsilon
$$

## Función 'cerca'
Para simplicidad, se usará la función `cerca(x,y,eps)` que calcula si dos números (o resultados) `x`,`y` son similares *con un cierto margen de error* dado por `eps`

```py
# cerca: num, num -> bool
# indica si dos cantidades son iguales, con un margen epsilon
# ej: cerca(0.1, 0.2, 0.1) es verdadero
def cerca(x,y,eps):
	return abs(x - y) <= eps

# tests
assert cerca(0.1, 0.2, 0.1) == True
assert cerca(0.1, 0.2, 0.0001) == False
```
	