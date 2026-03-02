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

