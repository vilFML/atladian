##¿Qué es un invariante?

El invariante es una afirmación lógica, es decir, se puede verificar si es verdadero o falso.

Condiciones que debe cumplir un invariante para que esté bien definido:

* Debe ser verificable y verdadero en todo momento, es decir, antes de empezar un ciclo, luego de cada iteración realizada y tras finalizar el ciclo.
  > **Obs:** es posible que el invariante se rompa (su valor de verdad sea falso) **durante** una iteración, sin embargo, debe volver a cumplirse antes de terminar la iteración.

* Debe estar en función de TODOS sus índices/iteradores/contadores.

* Debe tener una condición inicial y una condición de término acorde.

Se llama invariante porque a pesar de estar definido en función de elementos variables (Ej: `for i in range(0,20)`), la afirmación es siempre la misma, es decir, no depende del valor que tome el iterador/contador.

Ejemplo: Partición de Hoare, ¿cuál es el invariante?

# P1: Suma Objetivo
Dado un arreglo ordenado con $n$ números enteros diferentes y un entero $T$, se pide encontrar dos números del arreglo cuya suma sea exactamente $T$.
___
Se usan dos variables con sus inicios: $i=0$,$j=n-1$ para recorrer el arreglo.
Para $j$ fijo: ver la suma con número en $i$.
- Si suma es $T$, salir.
- Si la suma no es $T$, se pueden tener dos casos:
  * $T$ sea mayor que la suma de $a[i]+a[j]$, en cuyo caso se aumenta $i$ pues se necesita la suma se acerque a $T$.
  * $T$ es *menor* que la suma de $a[i]+a[j]$, entonces se disminuye $j$ para que la suma se acerque a $T$.
**Propiedad Invariante**: Entre los intervalos $[0:i],[j+1:n]$ no se encuentra ningún par de números cuya suma sea el valor objetivo $T$.
* *Condiciones Iniciales*: $i=0,j=n-1$, no se ha sumado ningún número y todavía no se recorre la lista.
* *Condición de Término*: El algoritmo termina cuando se encuentran números que sumen $T$ o que $i\geq j$ pues ya se recorrió la lista.

##### Implementación
```py
def sumaObjetivo(a, T):
	n = len(a)
	j = n-1
	i = 0
	
	while (i<j):
		if (a[i]+a[j] < T):
			i += 1
		elif (a[i]+a[j] > T):
			j -= 1
		else: # suma == T
			return a[i], a[j]
	
	# Si se sale del ciclo, se tiene que i>=j, no hay par
	return None, None
	
A = [-6,-3,-2,0,1,6,12]
T = 7
print(sumaObjetivo(A,T))
```

# P2: Bandera Holandesa
La bandera holandesa está compuesta de tres colores: rojo, blanco y azul. Se tienen esferas de estos tres colores ordenadas al azar en una línea (no es importante cuántas esferas de cada color hay). El objetivo es ordenarlas de forma que todas las esferas del mismo color se encuentren juntas y los colores estén en el orden correcto.
a) Analice los posibles invariantes del problema y dibújelos.
b) Programe la solución al problema siguiendo alguno de los invariantes de la parte.

---

## a)
Se quiere diseñar un programa que, dada una lista de tres colores repetidos al azar, los retorne debidamente ordenados. Se definen tres índices $i,j,k$.
Hay 4 posibilidades de invariantes, que dependen de *dónde quedan ubicados los términos desconocidos*.
Se tiene que $i\leq j\leq k$ para los casos y en las tablas se indican sus condiciones iniciales.
- **Desconocidos al final**

|      | 0     | 1     | 2     | ?   |
| ---- | ----- | ----- | ----- | --- |
| C.I. | $i=0$ | $j=0$ | $k=0$ |     |

como condición final se tiene que $k=n$. Así se procesa el último elemento.

- **Desconocidos entre los 1 y 2:**

| 0     | 1     | ?   | 2       |
| ----- | ----- | --- | ------- |
| $i=0$ | $j=0$ |     | $k=n-1$ |

condición final: $j=k+1$


- **Desconocidos entre 0 y 1.**
  * En el intervalo $[0:i]$ hay ceros, 
  * $[i:j+1]$ son los términos que faltan revisar
  * $[j+1:k+1]$ hay unos
  * $[k+1:n]$ del arreglo hay dos

| 0     | ?   | 1       | 2       |
| ----- | --- | ------- | ------- |
| $i=0$ |     | $j=n-1$ | $k=n-1$ |
como condición final se tiene que $i=j+1$


- **Desconocidos al inicio.**

| ?   | 0       | 1       | 2       |
| --- | ------- | ------- | ------- |
|     | $i=n-1$ | $j=n-1$ | $k=n-1$ |
y como condición final: $i=-1$
## b)
Implementando el tercer caso,
```py
def ordenarBandera(a):
	n = len(a)
	#indices, casos iniciales
	i = 0
	j = n-1
	k = n-1
	
	#condicion de fin: i = j+1
	while (i <= j):
		if (a[i] == 0): # elem es cero, pasarlo a conjunto solucion
			i += 1
			
		elif (a[i] == 1):   # desconocido es 1
			#elem tiene que estar en j
			a[i], a[j] = a[j], a[i]
			j -= 1
			
		else:   # desconocido es 2: debiese estar en ultimo conj sol.
			#1° iesimo con kesimo
			a[i], a[k] = a[k], a[i]
			#2° iesimo con jesimo
			a[i], a[j] = a[j], a[i]
			# crecio ultimo conj: afecta a j y k
			k -= 1
			j -= 1
	return a

import random
random_list = [i%3 for i in range(0,20)]
random.shuffle(random_list)
print(random_list)
ordered_list = ordenarBandera(random_list)
print(ordered_list)
```

# P3: Ordena Polinomios
Un polinomio se puede evaluar en tiempo lineal sin necesidad de una variable auxiliar si observamos que 𝑃 (𝑥) se puede factorizar como:
$$
P(x)=a_{0}+x(a_{1}+x(\dots+x(a_{n-1}+x(a_{n}))\dots))
$$
Por ejemplo,
$$
P(x)=5+2x-3x^{2}+4x^{3}=5+x(2+x(-3+x(4)))
$$
Programe un algoritmo iterativo que evalúe el polinomio utilizando esta idea. Comience desde el paréntesis más interno y avance hacia la izquierda. Indique cuál es el invariante que utiliza.
El algoritmo resultante se llama la Regla de Horner.

---

Se busca diseñar un algoritmo *iterativo*.
Se va a utilizar una única variable que acumule el resultado de forma sucesiva.
Asumiendo que la función recibe como entrada un arreglo $a=[a_{0},a_{1},\dots,a_{n-1},a_{n}]$ con cada número en su respectivo grado del polinomio de grado $n$, y el valor a evaluar $x$. La función retorna un valor $P$ con la evaluación del polinomio.
**Propiedad Invariante**:
Cuando el índice vale $i$, el valor de la variable `P` es la evaluación parcial del polinomio de grado $n-i+1$ considerando los coeficientes desde $a_{i+1}$ hasta $a_{n}$.
*Condiciones Iniciales*: 
- $P=0$ pues todavía no se evalúa ningún valor.
- $i=n$ ya que se apunta al grado mayor.
*Condición de Término*:
$i=-1$ o sea el ciclo finaliza cuando se su,a el coeficiente $a_{0}$.

##### Implementación:
```py
def evalp(a,x):
	n = len(a)-1   # corresponde al grado del polinomio a evaluar
	
	# Condiciones iniciales
	P = 0
	i = n
	
	while (i >= 0):
		P = P*x + a[i]
		i -= 1 # se reestablece el invariante
	
	# cuando i<0 se sale del ciclo, se sumaron todos los coef y P es el total
	return P

print(evalp([5,2,-3,4],2))
```

