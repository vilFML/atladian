# Crear Variables en Python

Crear una variable se denomina **declaración de una variable.**

Para declarar una variable se indica el nombre que tendrá la variable y se almacena un tipo de dato en ella con el *operador asignación '='*, de la forma:
$$
\text{Nombre de variable} = \text{Valor o expresion}
$$
se puede reasignar lo que contiene la variable si simplemente se le asigna otro dato.

\* En otros lenguajes de programación es necesario indicar qué tipo de dato almacenará la variable cuando ésta se declara: `int nombreVariable = 10`. En python no es necesario indicar el tipo de dato.

##### Ejemplo: Declaración y Reasignación
Inicialmente se declara una variable que indica tener un peluche de pikachu:
```py
peluche = 'pikachu'
```
en este caso se almacena un string.

Para cambiar el contenido de la variable (reasignar un nuevo valor), simplemente se reasigna otro dato:
```py
peluche = 'charmander'
```
se sobrescribe el string 'pikachu' con 'charmander'.

##### Ejemplo: Calcular el valor de otras
Suponiendo que se tienen dos variables:
1. El valor individual de un producto.
2. La cantidad del producto que se compra.
y se quiere almacenar la cantidad total a pagar de la compra:
```py
valor_producto = 500
cantidad_producto = 3

total = valor_producto * cantidad_producto
```
la variable 'total' se calcula en base a las otras dos variables.

### Asignación de expresión
Cuando se asigna una expresión que involucre variables, el proceso se debe leer de derecha a izquierda, de forma que:
1. Se reemplazan los valores de las variables en la expresión.
2. Se evalúa la expresión.
3. Se almacena el resultado en la variable.

*Ejemplo*: Calcular el área de un rectángulo,
```py
largo = 7
ancho = 2
area = largo * ancho
```
primero se reemplazan los valores de 'largo' y 'ancho', luego se evalúa la expresión (se realiza la multiplicación) y el resultado queda almacenado en la variable 'area'.

\* Si se modifica alguna de las variables de la expresión *después* del proceso de evaluación y asignación, la reasignación no hace efecto en la variable que almacena la expresión.

# Alcance en Python

Se tienen distintos alcances de [[Variables|variables]], y en python:

```py
x = 25

def f():
	y = 52
```
en el ejemplo, `x = 25` está en el ambiente global y `y = 52` es una variable en un ambiente local.

**Regla de Búsqueda**: Cuando se quiere acceder a una variable, el alcance comienza mirando dentro de sí por variables. Si no las encuentra, busca en un alcance 'más grande'. *Un alcance más grande **no** puede ver hacia alcances más pequeños.

```py
def f():
	x = 10
	print(x)

f()
print(x)
```
en este caso se tiene un problema cuando se intenta acceder a la variable `x` desde el ambiente global, y como en el alcance global no está definida `x` entonces se tiene un error.

```py
x = 100

def f():
	y = 200
	print(x + y)

f()
print(x)
```
no hay error al invocar `f()` pues `x` no está definida localmente, y entonces se busca en el ambiente global.

```py
x = 100

def f():
	x = 200
	y = 200
	print(x + y)

f()
print(x)
```
dentro de la función se comienza usando las variables en su interior. Así la variable `x` de valor 200 tiene precedencia sobre la asignación del valor 100 hecha globalmente pues cuando se accede a una variable primero se hace la búsqueda localmente y luego globalmente.

```py
x = 100
y = 200

def f():
	print (x + y)

f()
```
en este caso las variables `x` e `y` no están definidas en el ambiente local, pero si en el ambiente global y, por lo tanto, no hay error.


