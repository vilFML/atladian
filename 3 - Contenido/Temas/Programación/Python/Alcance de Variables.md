El alcance de una variable se refiere a la región del código en la cual se puede reconocer y acceder. O sea en dónde se puede usar la variable y cuál es su tiempo de vida.
Se van a ver dos tipos de alcance: *global y local*.

1. **Alcance Global**: Corresponde al ambiente en el cual se encuentra el programa principal.
2. **Alcance Local**: Una función define un ambiente local, en donde las variables creadas en su interior solo viven dentro de la función.

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


