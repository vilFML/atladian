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