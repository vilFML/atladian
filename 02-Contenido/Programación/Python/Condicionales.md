# Expresiones Condicionales
Una expresión de la forma
```python
valor_si_verdadero if condicion else valor_si_falso
```
permite por ejemplo definir funciones por tramos, como por ejemplo:

$$
|x| =
\begin{cases}
-x & \text{si } x<0 \\
x & \text{en caso contrario}
\end{cases}
$$


```python
def valor_absoluto(x):
    return -x if x<0 else x
print(valor_absoluto(-5), valor_absoluto(5))
```

    5 5

## If
La instrucción `if` permite ejecutar bloques de código solo si es que se cumple una determinada condición.

### Sintaxis en Python

```py
if 'condicion':
	instruccion 1
	instruccion 2
	...
	instrucion n

instruccion #fuera del bloque condicional
```

Cuando se tiene un `if` ocurre que:
1. Si es que la condición se evalúa a `True`, entonces se ejecutan sucesivamente la instrucción 1, instrucción 2, y así hasta que se ejecuten las $n$ instrucciones.
2. Si es que la condición se evalúa a `False`, *se ignora* todo el conjunto de instrucciones y, por lo tanto, se ejecuta la instrucción fuera del bloque condicional.

gráficamente en un diagrama de flujo:
![[Pasted image 20260302140637.png]]


## if-else
Para ejecutar líneas de código únicamente en caso de que la confición sea evaluada a `False`, se utiliza la palabra reservada `else`. En este caso, las instrucciones del bloque `else` se ejecutarán únicamente si es que la condición es `False`.

**Sintaxis:**
```py
if 'condicion':
	instrucciones bloque if
else:
	instrucciones bloque else

instrucciones #fuera del bloque condicional
```

gráficamente:
![[Pasted image 20260302141022.png]]

## elif
`elif` es una abrevación de else-if
Se utiliza para evaluar varias condiciones que se puedan cumplir y ejecutar un bloque de código para cada caso.
-  El primer bloque `elif` cuya condición sea `True` se ejecutará, ignorando los siguientes `elif` y `else`

el código enraizado de la forma:
```py
if 'condicion1':
	instrucciones1
else:
	if 'condicion2':
		instrucciones2
	else:
		if 'condicion3':
			instrucciones3
			else:
				instruccionesELSE
```
es poco claro, y se puede escribir mejor con `elif`:
```py
if 'condicion1':
	instrucciones1
elif 'condicion2':
	instrucciones2
elif 'condicion3':
	instrucciones3
else:
	instruccionesElse
```

gráficamente, el flujo de comprobación es:
![[Pasted image 20260302165428.png]]

# Funciones Condicionales
Las [[Funciones|funciones]] pueden contener condicionales dentro de sus instrucciones.
Si una ramificación del código necesita retornar un determinado valor, entonces debe tener un `return` asociado.

- Se deben identificar *todos los escenarios posibles* que puede devolver la función, dependiendo de los valores de entrada. Estos casos se deben testeer (de ser posible) según la receta de diseño.

##### Ejemplo: Función esPar
Una función que, dado un número, devuelve `True` si es par o `False` en caso contrario:
```py
# esPar: int -> bool
# devuelve True si x es par, False si no
# ej: esPar(2) devuelve True y esPar(3) devuelve False
def esPar(x):
	if x % 2 == 0:
		return True
	else:
		return False

# tests
assert esPar(2) == True
assert esPar(3) == False
```

y se puede simplificar aún mas retornando inmediatamente la evaluación de la expresión del operador módulo:
```py
# esPar: int -> bool
# devuelve True si x es par, False si no
# ej: esPar(2) devuelve True y esPar(3) devuelve False
def esPar(x):
	return x % 2 == 0

# tests
assert esPar(2)
assert esPar(3)
```
esto, debido a que se redundaba en que la expresión se evalúa a `True`, entonces se devuelve `True` y lo mismo para `False`.
Y, de igual manera, se pueden simplificar los tests haciendo assert a lo que retorna la función.

