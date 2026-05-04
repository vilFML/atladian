Al tipo de operaciones en donde se calcula una instancia en base a una menor, se le conoce como **recursión**. Para resolver el problema de un tamaño $n$, se debe primero resolver el mismo problema para un tamaño $n-1$ y así sucesivamente hasta llegar a un **caso base**.

## Exponenciación
Una exponenciación $y = x^{n}$  se puede resolver de la forma:
$$
y = x^{n} = 
\left\{
	\begin{array}{ll}
		x\cdot x^{n-1}\; , \text{si } n > 0 \\
		1\; , \text{si } n = 0
	\end{array}
\right.
$$
en código:
```py
def exp(x,n):
	if (n == 0):
		return 1
	else: return x * exp(x, n-1)
```
en la línea `exp(x, n-1)` se hace el llamado a la misma función, pero con un menor valor de $n$ (el exponente)

*ej:*`exp(2,4)`
luego, $x = 2, n=4$.
1. Se hace la pregunta si $n$ es 0, como no se cumple se ejecuta el siguiente subnivel con $n-1=4-1=3$

|                  |               |                 |               |                                    |
| ---------------- | ------------- | --------------- | ------------- | ---------------------------------- |
| `exp(2,4)`       | <-$2*8 = 16$  |                 |               |                                    |
| -> $n-1=4-1=3$-> | `2*exp(2,3)`  | <-$2*4=8$       |               |                                    |
|                  | $n-1=3-1=2$-> | `2*exp(2,2)`    | <- $2*2=4$    |                                    |
|                  |               | ->$n-1=2-1=1$-> | `2*exp(2,1)`  | <- $2*1 = 2$                       |
|                  |               |                 | $n-1=1-1=0$-> | `2*exp(2,0)`                       |
|                  |               |                 |               | $n=0$: Caso base<br>`exp(2,0) = 1` |
al ver $x^{n}=x\cdot x\cdot x\cdot\cdot\cdot x$, se tiene una multiplicación de x '$n$' veces, y para ver cuántas operaciones se hacen, se ve que se hacen $n$ operaciones. Se tiene un algoritmo de orden lineal $O(n)$.

Otra implementación era con el [[Propiedad Invariante#Algoritmo Binario|algoritmo binario]], en donde se hace: $x^{k}=(x^{2})^{\frac{k}{2}}$.
La implementación en código usando recursividad:
```py
def exp_recursivo(x,n):
	# Caso base
	if (n == 0):
		return 1
	elif (n%2 == 0):
		return exp(x*x, n//2)
	else:
		return x*exp(x,n-1)
```

## Buscar Máximo con Recursividad
En primer lugar, se debe pensar en el caso trivial (o caso base):
- El caso trivial sería una lista con un solo elemento, en cuyo caso *el valor máximo es el mismo elemento*. 
Luego, el paso recursivo es usar la misma función para un tamaño 
Luego, la función para tener el valor máximo de un arreglo $a$, 
$$
max(a,i)= 
\left\{
	\begin{array}{ll}
		max(a[i], max(a,i+1)), \text{ si } i < n - 1 \\
		a[i], \text{ si } i ==n-1
	\end{array}
\right.
$$
esta función se llama con `max(a,0)`, donde $a$ es el arreglo y se indica que se quiere comenzar las comparaciones desde el índice $0$. Así, para la llamada recursiva, se 'quita' el elemento en la posición $0$ y se compara con las posiciones restantes.

## Torres de Hanoi
Es un puzzle en el que se tienen 3 varillas y una torre de discos en 1 varilla. Se deben mover los discos desde la varilla izquierda a la derecha. Todos los discos son de distinto tamaño y están ordenados con el más grande abajo; al cambiar las posiciones, no se puede poner un disco mas chico abajo de uno mas grande y solo se puede mover 1 disco a la vez.
* Con 2 varillas se puede mover solo el más pequeño y nada mas.
* Con 3 varillas se usa la tercera como apoyo.
El caso base es que no se tengan discos: $n=0$, en cuyo caso no se hace nada y se tiene resuelto el puzzle.

> Para mover $n$ discos desde $a$ hasta $c$ (usando la estaca $b$ como auxiliar):
> * Primero movemos (recursivamente) $n-1$ discos desde la estaca $a$ a la estaca $b$.
>* Una vez despejado el camino, movemos 1 disco desde $a$ hasta $c$.
>* Finalmente, movemos de nuevo (recursivamente) los $n-1$ discos, ahora desde $b$ hasta $c$ (usando $a$ como auxiliar).
>El caso base es $n=0$, en cuyo caso no se hace nada.

Implementación:
```py
def Hanoi(n, a, b, c): # Mover n discos desde "a" a "c", usando "b" como auxiliar
    if n>0:   # Si hay discos
        Hanoi(n-1, a, c, b)   # Se mueven los n-1 discos desde A hasta C, con B aux
        # Se despeja B, entonces se mueven de C->B con aux A
        print(a, "-->", c) # Mueve 1 disco desde "a" hasta "c"
        Hanoi(n-1, b, a, c)
```

# Recursividad v/s Iteración

Cuando se tiene una implementación por iteración, se puede llevar a una definición recursiva. Un ciclo de la forma:
```py
while (A):
	C
```
se puede llevar a:
```py
def f():
	if (A):
		C
		f()

f()
```

Por ejemplo, para mostrar los elementos de una lista:
```py
def imprimir(a):
	k = 0
	while (k < len(a)):
		print(a)
		k += 1   #aumentar k permite avanzar
```
de alguna forma, $k$ es una variable de estado. Pues esta permite saber en qué punto de la iteración se encuentra el algoritmo.
Esta pasa a ser
```py
def imprimir (a,k):
	if (k < len(a)):
		print(a[k])
		imprimir(a, k+1)   #es el simil de aumentar k
```
En la recursividad no se define una variable de estado, si no que se entrega como un parámetro.

- En la iteración se inicia $k$ en un valor $0$, mientras que en la recursividad *se llama a la función con el $k$ en la posición 0* (en `imprimir(a,0)`).
- La definición recursiva dice 'imprimir la lista a,  partiendo desde la k-ésima posición'. Así, al aumentar $k$, se está accediendo a 'listas de listas'.
  $$
  a(1,lista(b,lista(\dots,lista(\dots))))
  $$
- La llamada recursiva se realiza al final. Estas funciones se llaman **tail recursion** (o recursión a la cola), y cualquiera de estas funciones se puede convertir a una función iterativa siguiendo el esquema indicado anteriormente.
La idea de tener equivalencias es que la solución puede ser mejor vista con cualquiera de las dos formas.
> Usualmente, la versión iterativa utiliza menos recursos que la recursión.

# Ejemplo: Ejercicio 2
Se le pide que escriba las instrucciones de la función ``genera_binarios`` de acuerdo al siguiente algoritmo:
* si el valor de ``k`` es igual a ``n``, ya se han generado todos los dígitos por
    lo cual se imprime el arreglo en pantalla ``(print(a))``
* si no, se hacen dos cosas:  
    - se pone un 0 en la ``k``-ésima posicion y se llama recursivamente
      a la función para que genere los dígitos restantes
    - luego se pone un 1 en la misma ``k``-ésima posición (reemplazando el 0) y se
      llama recursivamente a la función para que genere los dígitos restantes

Pruebe su función con para el caso ``n=4``. Asegúrese de que genere el mismo resultado que el que aparece en el enunciado.


Implementación:
---
Se pide que se entregue todos los posibles números binarios que se pueden escribir con una cierta cantidad de dígitos.

La implementación corresponde a un algoritmo recursivo, se deben identificar los casos base y la llamada recursiva:
* **Caso base**: $k-n=0$, esto es, no faltan dígitos. Entonces se imprime el arreglo.
* **Llamada recursiva**: Para cada dígito se tienen dos maneras de colocar un dígito: que tenga un `0` o un `1`. Esto se puede enfrentar recursivamente si se dividen los números a generar según qué número va en el primer dígito, y luego llamar recursivamente para todos los restantes, de la forma:
  1. Se coloca un `0` en la k-ésima posición y se llama recursivamente a la función para que genere los $n-k$ dígitos restantes. Así se tienen todos los posibles números de $n$ dígitos que empiezan con un `0`.
  2. Se coloca un `1` en la k-ésima posición y se llama recursivamente para los siguientes $n-k$ dígitos y se obtienen todos los números que empiezan con `1`.
  En la primera ejecución se va a llamar para $k=1$, o sea se pueden tener los dos casos. Y para cada uno, se llama recursivamente a la función en los dígitos restantes.

```py
def genera_binarios(a,k,n):
	if k == n:   # caso base: k-n = 0, no quedan dígitos restantes por llamarles recursivamente la funcion
		print(a)
	else:
		a[k] = 0    #primer dígito = 0
		genera_binarios(a,k+1,n)
		
		a[k] = 1    #primer dígito = 1
		genera_binarios(a,k+1,n)
```
