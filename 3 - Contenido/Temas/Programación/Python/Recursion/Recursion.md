La recursión es la forma en la cual se especifica un proceso basado en su propia definición. 
También se puede pensar como un gran rompecabezas, el cual, para ser resuelto, se divide en piezas más pequeñas. Y cuando cada pieza pequeña esté resuelta, el rompecabezas completo estará resuelto.

Un problema puede ser definido en función de su tamaño (por ejemplo $N$). Y es resuelto *de manera recursiva* si:
1. Es dividido en instancias más pequeñas (de tamaños menores a $N$) del mismo problema
2. Se conoce una solución explícita para sus instancias más simples, conocido como **el caso base.**
3. Cada problema más pequeño *tiende a acercarse o converger* al caso base, los cuales son procesos conocidos como *pasos recursivos*.

# Funciones Recursivas
Las funciones recursivas son funciones **que se invocan a sí mismas** para resolver un determinado problema.
La idea es descomponer el problema inicial en problemas más pequeños y manejables, reutilizando la misma función para resolverlos.

Las funciones recursivas se componen de dos partes: **Caso base** y **llamado recursivo**.


```py
# funcion_recursiva: int -> None
def funcion_recursiva(valor):
	if valor == 10:
		return None
	else:
		return funcion_recursiva(valor + 1)
```
es una funcion en donde se tiene:
1. **Caso base**: Es la solución conocida del problema que **no** continúa con la recursión (también se llama *condición de término*).
   En este caso, el caso base o condición de término es cuando la variable `valor` llega a ser `10`.
2. **Llamado Recursivo:** La función se invoca a sí misma, pero con un argumento tal que tras sucesivos llamados, se acerca al caso base. Esta hecha de tal forma que se acerca al caso base o la condición de término.
   Aquí los llamados recursivos se tienen en el bloque `else` y acerca la variable al caso base al *sumarle 1* en cada llamado recursivo.

# Call Stack (Pila de Ejecución)
El call stack es el tiempo o procesos en el que la función realiza llamados a sí misma (o a otras funciones recursivas).

Ej:
```py
def A():
	return 'Me gustan ' + B()

def B():
	return 'los perros ' + C()

def C():
	return 'y los gatos.'
```
existe una *dependencia en cadena* de la funciones, en donde:
1. La función `A()` depende de `B()`
2. la función `B()` depende de `C()`
3. la función `C()` no depende de otra definición y retorna un string.

Al llamar la función `A()` se van a ejecutar las demás funciones. Y se tendrá una evolución del Call Stack de la forma:

| Call Stack            |
| --------------------- |
| 'y los gatos.'        |
| 'los perros ' + `C()` |
| 'Me gustan ' + `B()`  |
Se ejecuta `B()` y, en consecuencia, se ejecuta `C()`, retornando el string `'y los gatos.'` a la función `B()` la cual concatenará los strings para retornarlos, devolviendo `'los perros y los gatos.`

| Call Stack                |
| ------------------------- |
|                           |
| 'los perros y los gatos.' |
| 'Me gustan  ' + `B()`     |

Luego, se va a tener el retorno de `B()` anterior, y queda:

| Call Stack            |
| --------------------- |
|                       |
|  |
| 'Me gustan los perros y los gatos.' |

en donde para `A()` se recibe el retorno de `B()` y es en este punto que la función `A()` puede retornar un valor, concatenando los strings y entregándolos.

## Stack Overflow
Cuando a llamadas recursivas no se le implementa un caso base, no se podrá concluir con las ejecuciones recursivas de las funciones y la pila de ejecución queda sin memoria para mas ejecuciones.

##### Ejemplo
```py
def A():
	return A()
```
no tiene un caso base que devuelva un valor y termine con las llamadas recursivas.

##### Ejemplo: Cálculo de Factorial
El factorial de un número puede definirse recursivamente usando la misma definición de factorial para un número anterior, de la forma:
$$
n! = 
\left\{
	\begin{array}{ll}
		1\; , \text{si } n = 0 \\
		n\cdot(n-1)!\; , \text{si } n > 1
	\end{array}
\right.
$$
en código:
```py
# factorial: int -> int
# devuelve el factorial de un numero entero
# ej: factorial(4) devuelve 24
def factorial(x):
	# Caso base
	if x == 0:
		return 1
	else:
		# Caso recursivo
		return x * factorial(x - 1)

#tests
assert factorial(0) == 1
assert factorial(4) == 24
```

![[Pasted image 20260302180001.png]]
![[Pasted image 20260302180113.png]]

# Parámetros por Omisión
Son parámetros entregados a las funciones que *toman un valor por defecto* en caso de que se invoque la función **sin asignarle un valor**. Y en caso de que se le entregue un valor al parámetro, se omite la asignación por omisión
\* En el contrato los parámetros por omisión van entre paréntesis.

Una de las utilidades que tienen los parámetros por omisión es que *permiten almacenar información* entre sucesivas llamadas recursivas. Así, cuando se invoca una función recursiva, recrea todas sus variables internas (creando efectivamente un nuevo ambiente local) olvidando todo lo que había calculado previamente.
> Una forma de mantener información entre invocaciones recursivas es utilizando parámetros por omisión.


##### Ejemplo
```py
# mascotas int, (str) -> str
def mascotas(n, tipo='perro')
	mensaje = f'Yo tengo {n} {tipo}'
	return mensaje
```
esta función tiene un segundo parámetro llamado `tipo` que es un parámetro por omisión, el cual su valor por defecto es `'perritos'`.

#####  Ejemplo:
Implementar una función que entrega el dígito mayor que compone a un número
```py
# digitoMayor: int, (int) -> int
# devuelve el digito mayor de N
# ej: digitoMayor(3102716) devuelve 7
def digitoMayor(N, mayor=0):
	# Caso base
	if N == 0:
		return mayor
	
	# Caso recursivo
	ultimo = N % 10
	resto = N // 10
	
	# si aun quedan digitos, se debe seguir revisando, pero 
	# se actualiza el mayor si corresponde
	if ultimo > mayor:
		return digitoMayor(resto, ultimo)
	else:
		return digitoMayor(resto, mayor)

#tests
assert digitoMayor(3102716) == 7
```
1. Se utiliza un parámetro por omisión `mayor` para ir almacenando el mayor número que se ha visto.
2. Si se llega al final, entonces se retorna el *máximo* que se ha ido guardando en la variable `mayor`.
3. En cada llamada recursiva se actualiza la variable `mayor` en caso de que corresponda. Notar que siempre se entrega recursivamente un número menor (sin el último dígito).

# Ciclos Recursivos
Se puede hacer uso de la recursión para implementar *ciclos interactivos* con el usuario. Un patrón usual para este tipo de funciones es:
1. Se pide al usuario cierta información
2. *Caso base:* Corresponde a un dato especial definido por el problema (como un número negativo, un punto, una palabra clave como 'fin', etc) con la cual la recursión finaliza.
3. *Caso recursivo:* Se hace alguna operación con el dato ingresado por el usuario y se vuelve a invocar la recursión.

##### Ejemplo:
Escribir una función recursiva que pida números positivos al usuario (hasta que ingrese un valor negativo) e imprima en pantalla la suma de ellos, sin considerar el número negativo.
```py
# suma_interactiva: None, (num) -> None
# Pregunta por numeros positivos hasta que se
# ingresa un numero negativo y luego entrega la suma de los numeros
# Ej: No hay ejemplo, la funcion solo muestra en pantalla.
def suma_interactiva(suma = 0):
	n = float(input('numero? '))
	
	# Caso base
	if n < 0:
		print('la suma es: ', suma)
		return None
	
	# Caso recursivo
	else:
		return suma_interactiva(suma + n)

# tests: no hay tests pues siempre retorna None
```
- El parámetro por omisión permite guardar la suma de los números en las sucesivas llamadas recursivas.

# Módulo turtle
Es un módulo que permite dibujar en pantalla usando una tortuga. Los dibujos de harán en una ventana gráfica que contiene dentro de sí un sistema cartesiano.
Al ejecutar el código se abre una ventana en la cual la tortuga podrá dibujar cosas.
- La tortuga siempre comienza en la posición `(0,0)` mirando hacia la derecha.
```py
import turtle

turtle.shape('turtle')
turtle.done()

```
entrega una tortuga.

## turtle.forward(n)
La tortuga se mueve $n$ pixeles en la dirección en la que se está mirando la tortuga.

## turtle.left(degrees)
La tortuga gira hacia la izquierda una cantidad de degrees indicados
\* Para giro a la derecha se usa `turtle.right(degrees)`

## más funciones de turtle

| Función            | Significado                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------- |
| `turtle.back(n)`   | Movimiento hacia atrás $n$ pixeles                                                                  |
| `turtle.penup()`   | Al avanzar, la tortuga no marca pixeles (levanta el lápiz)                                          |
| `turtle.pendown()` | La tortuga baja el lapiz para comenzar a marcar pixeles (baja lápiz)                                |
| `turtle.speed(n)`  | Para cambiar la velocidad de la tortuga, con `n = 0` se tiene máxima velocidad.                     |
| `turtle.done()`    | Previene el cierre de la ventana en donde se dibuja. Debe ser la última instrucción que se ejecute. |
|                    |                                                                                                     |
|                    |                                                                                                     |
##### Ejemplo: Dibujar cuadrado
```py
import turtle as t

t.shape('turtle')

# cuadrado: int -> None
# Dibuja un cuadrado de lado L pixeles
def cuadrado(L):
	t. forward(L)
	t.left(90)
	t. forward(L)
	t.left(90)
	t. forward(L)
	t.left(90)
	t. forward(L)
	t.left(90)

# invocamos la función cuadrado
cuadrado(100)
t.done()

```



# Fractales
Un fractal se puede definir como un objeto geométrico que *repite el mismo patrón en sí mismo*, a diferentes escalas y orientaciones.

##### Ejemplo: Fractal de Sierpinski (trifuerza)
Escribir la función `fractal_sierpinski(largo, n)` que recibe el largo del trazo y el nivel de profundidad recursiva $n$ que debe alcanzar el fractal.
- La figura base es un triángulo equilátero y en cada llamada recursiva su largo disminuye a la mitad.
1. **Caso base**: Se detecta que el caso base consiste en dibujar un triángulo equilátero de lados $L$.
2. **Caso recursivo:** Teniendo el triángulo equilátero de lado $L$, se deben dibujar *tres triángulos equiláteros recursivamente* (T1, T2 y T3) en su interior y cada uno de lado $\frac{L}{2}$. El triángulo de en medio se forma naturalmente.
   - Para dibujar los triángulos se parte siempre desde el punto inferior izquierdo de los triángulos T1, T2 y T3, puntos denotados como P1, P2 y P3, respectivamente.. Y al terminar de dibujar un triángulo, se deja siempre la tortuga mirando hacia la derecha para facilitar el cálculo de ángulos y giros necesarios.

**Algoritmo Cursive**
1. Se parte de `P1` y se dibuja recursivamente el fractal de Sierpinski del triángulo `T1`.
2. La tortuga queda en el mismo punto `P1`, mirando a la derecha.
3. Se avanza hacia `P2`
4. Se dibuja recursivamente el fractal de Sierpinski en el triángulo `T2`.
5. La tortuga queda en el punto `P2` mirando a la derecha.
6. Se avanza hacia `P3`
7. Se dibuja recursivamente el fractal de Sierpinski en el triángulo `T3`
8. La tortuga queda en el punto `P3`, mirando a la derecha.
9. Se avanza de vuelta al punto `P1`, dejándola mirando a la derecha.

Solución:
```py
# fractal_sierpinski: int, int -> None
# Dibuja un fractal del triangulo de sierpinski
def fractal_sierpinski(largo,n):
	if n == 1:
		turtle.forward(largo)
		turtle.left(120)
		turtle.forward(largo)
		turtle.left(120)
		turtle.forward(largo)
		turtle.left(120)
	else:
		fractal_sierpinski(largo / 2, n - 1)
		turtle.forward(largo / 2)
		turtle_sierpinski(largo / 2, n - 1)
		turtle.back(largo / 2)
		turtle.left(60)
		turtle.forward(largo / 2)
		turtle.right(60)
		fractal_sierpinski(largo / 2, n - 1)
		turtle.left(60)
		turtle.back(largo / 2)
		turtle.right(60)
```
- El **caso base** es el bloque `if`, en donde se dibuja un triángulo equilátero cuyo lado mide lo mismo que el largo que se entregue como parámetro.
  \*Se deja la tortuga mirando a la derecha para consistencia entre dibujos.
- El **caso recursivo** corresponde al bloque `else`. Se va a los puntos en donde debe dibujarse recursivamente y posteriormente dejar a la tortuga en su posición inicial.