# P1 : P1, C1, 2018-1
Para cada ecuación recursiva, indique a qué categoría pertenece (lineal de primer orden, lineal con coeficientes constantes, no lineal tipo [[Análisis de Algoritmos#Teorema Maestro| teorema maestro]]) y el orden asintótico más ajustado de su solución:
$$
\begin{aligned}
 & (\mathrm{a})T(n)=3\cdot T(n-1)+4\cdot T(n-2),\forall n\geq2,T(0)=T(1)=1 \\
 & (\mathrm{b})T(n)=2T(\frac{n}{2})+n,\forall n>0,T(0)=1 \\
 & (\mathrm{c})T(n)=T(\frac{n}{2})+1,\forall n>0,T(0)=1
\end{aligned}
$$

##### a)
Se tiene una [[Ecuaciones de Recurencia#Recurrencia Lineal|recurrencia lineal]]. Entonces, se reemplaza $T(n)=\lambda^{n}$:
$$
\begin{align}
 & \lambda^{n}=3\lambda^{n-1}+4\lambda^{n-2} & \iff \\
\iff & \lambda^{n}-3\lambda^{n-1}-4\lambda^{n-2}=0
\end{align}
$$
de esto se tiene como solución $\lambda=0$, pero se descarta por ser solución trivial. Así, se puede dividir la ecuación por $\lambda^{n-2}:$
$$
\begin{align}
 & \lambda^{2}-3\lambda-4=0\iff(\lambda-4)(\lambda+1)=0 \\
 \implies \lambda=4 ,\lambda=-1
\end{align}
$$
así, se tiene una solución como combinación lineal de los $\lambda$, o sea:
$$
T(n)=A\cdot 4^{n}+B(-1)^{n}
$$
y las constantes se obtienen utilizando las condiciones iniciales (o cond. borde): $T(0)=T(1)=1$:
$$
\begin{align}
T(0)=A+B=1 \\
T(1)=4A-B=1
\end{align}
$$
resolviendo el sistema de ecuaciones: $A=\frac{2}{5},B=\frac{3}{5}$ y se tiene finalmente que 
$$
T(n)=\frac{2}{5}4^{n}+\frac{3}{5}(-1)^{n}
$$
que tiene complejidad de $O(4^{n})$ por ser el término de mayor tamaño.

##### b)
Se tiene un algoritmo que *divide un arreglo en 2* y agrega una carga extra de n.
> Cuando se tenga un solo $T$ con una fracción y con un término extra, se vé similar al **teorema maestro**.

1°: No es homogénea por el término de carga extra $n$. Entonces, por teorema maestro se identifican:
$$
\begin{align}
p=2 \\
q=2 \\
r=1
\end{align}
$$
y se tiene que $q^{r}=p$, entonces aplicando el teorema maestro para este caso:
$$
q^{r}=p \implies T(n)=\Theta(n^{r}\log n)\implies T(n)=\Theta(n\log n)
$$

##### c)
por teorema maestro:
$$
\begin{align}
p=1 \\
q=2 \\
r=0
\end{align}
$$
entonces
$$
q^{r}=2^{0}=1=p \implies \Theta(n^{r}\log n)=\Theta(\log n)
$$

### Caso T(n) con raíz
Si se vé algo que tenga raíz cuadrada:
$$
x_{n}=\sqrt{ x_{n-1}x_{n-2} }
$$
**aplicar $\log$ a la ecuación para bajar los exponentes y que las multiplicaciones pasen a sumas:**
$$
\begin{align}
 & x_{n}=\sqrt{ x_{n-1}x_{n-2} } /\log() \\
\iff & \log(x_{n})=\frac{1}{2}(\log(x_{n-1}\cdot x_{n-2})) \\
\iff & \log(x_{n})=\frac{1}{2}\log(x_{n-1}) + \frac{1}{2} \log(x_{n-2})
\end{align}
$$
Y esto se puede linealizar usando un *cambio de variable* de la forma: $y_{n}=\log(x_{n})$, y reemplazando:
$$
\implies y_{n}=\frac{1}{2}y_{n-1}+\frac{1}{2}y_{n-2}
$$
y aquí se aplica el método de $\lambda^{n}$

Se va a tener una solución para $y_{n}$, entonces para llevar a $x_{n}$ se debe aplicar función exponencial: $/\exp()$

# P2: Subarreglo de suma máx
Dado un arreglo con enteros positivos y negativos, se quiere conseguir el subarreglo que contiene la suma máxima posible.
Un subarreglo es cualquier subconjunto consecutivo del arreglo. Por ejemplo si el arreglo es $[-2, -3, 4, -1, -2, 1, 5, -3]$ el resultado sería el subarreglo $[4, -1, -2, 1, 5]$ de suma total $7$.
a) Programe una solución que resuelva el problema, sin importar cuan eficiente es.
b) ¿Puede ser más eficiente la solución? Intente mejorar la solución anterior.
c) Intente mejorar la solución anterior usando una estrategia dividir para reinar.
d) Sea aún más eficiente: programe una solución que resuelva el problema en tiempo lineal. *Hint: La clave está en los números que son negativos.*
Para todos los casos anteriores entregue cuál es su costo en notación Big-O.

___

##### a) probar todas las sumas posibles.
Idea: para cada valor ir haciendo las sumas contiguas e ir comparándolas

```py
def suma_maxima_brutisimo(a):
	sumaAct = 0
	sumaMax = 0
	n = len(a=
	
	for i in range(0, n):
		for j in range(i, n):
			for k in range(i, j+1):
				sumaAct = += a[k]
				if sumaAct > sumaMax:
					sumaMax = sumaAct
				sumaAct = 0
```
cuando hay tres ciclos for, se tiene una complejidad del orden de $O(n^{3})$

##### b)
Se puede eliminar el tercer ciclo `for`, así se van sumando los siguientes números y cada resultado se suma:
```py
def suma_maxima_brutisimo(a):
	sumaAct = 0
	sumaMax = 0
	n = len(a=
	
	for i in range(0, n):
		for j in range(i, n):
			sumaAct = += a[j]
			if sumaAct > sumaMax:
				sumaMax = sumaAct
			sumaAct = 0
```

##### c)
si se divide la mitad, se tienen tres posibilidades de dónde puede estar la suma máxima:
1. A la izq
2. A la derecha
3. Entremedio
$$
T(n)=2T\left( \frac{n}{2} \right) + n
$$
en donde $2T\left( \frac{n}{2} \right)$ pues se dividen a 2 sub-partes de tamaño la mitad del arreglo original.
Y $+n$ para sumar la que pasa por el medio del arreglo.
Por teorema maestro $\Theta(n\log n)$

##### d)
cualquier subarreglo que dé suma negativa se descarta (cuando se suman contiguamente a la derecha, para cada número del arreglo).
Además, ningún sub-arreglo puede empezar a la izquierdo con un número negativo pues este sólo va a restar en la suma. Entonces ellos también se descartan (solo los números negativos a la izquierda).

# P3
La sustitución es la más poderos pues reemplaza borrar e insertar

> En general: Programación dinámica es mejor que la recursividad.

Esto pues con programación dinámica se van 'recordando' los casos anteriores y con la recursividad se van recalculando todos los casos cuando se llama la función.