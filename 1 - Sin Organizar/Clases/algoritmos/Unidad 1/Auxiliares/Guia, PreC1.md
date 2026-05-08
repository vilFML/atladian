# P1

^5b4e55

Resolver las relaciones de recurrencia
## a.
$$
\begin{align}
 & T(n)=3T(n-1)+4T(n-2) \\
 & T(0)=2,  \\
 & T(1)=3
\end{align}
$$
es similar a [[Aux3#a)]]

## b.
$$
f(n)=2f(\sqrt{ n })+\log_{2}n
$$
*hint*: Hacer cambio de variable $n=2^{k}$ y aplicar teorema maestro.
___
Haciendo cambio de variable $n=2^{k}$, la ecuación pasa a ser:
$$
\begin{align}
 & f(2^{k})=2\cdot f(\sqrt{ 2^{k} })+\log_{2}(2^{k}) \\
\iff & f(2^{k})=2\cdot f(2^{k/2})+k\cdot \underbrace{ \log_{2}(2) }_{ =1 } \\
\iff & f(2^{k})=2\cdot f(2^{k/2})+k
\end{align}
$$
haciendo una nueva función incógnita $a(k)=f(2^{k})$ se  pasa a:
$$
a_{k}=2\cdot a_{\frac{k}{2}}+k   \iff a(k)=2\cdot a\left( \frac{k}{2} \right)+\underbrace{  }_{ C=1 }\underbrace{ k }_{ n=k, r=1 }
$$
por [[Análisis de Algoritmos#Teorema Maestro|teorema maestro]]: $p=2,q=2,r=1$, luego $q^{r}=2^{1}=2=q$ entonces se tiene una complejidad de $a(k)=\Theta(n^{r}\log n)$ (en este caso $n$ es de la forma general del teorema maestro)$\implies \Theta(k \log k)$
Para volver a términos de $n$:
$$
\begin{align}
 & n=2^log{k} / \log() \iff \log(n) = k \log(2)\iff k=\frac{\log(n)}{\log2}=\log_{2}n \\
  \implies & a(k)=f(2^{k})=f(n) \\
 \implies & f(n)=\Theta(k\log k) \\
  & f(n)=\Theta(\log_{2}n \cdot \log(\log_{2}n)) 
\end{align}
$$

## c.
Es similar a a)

# P2
Considere la siguiente ecuación de recurrencia:
$$
\begin{align}
 & T(n)=8T(n-1)-15T(n-2) \\
 & T(0)=1 \\
 & T(1)=1
\end{align}
$$
a) Escriba una función recursiva que calcule $T(n)$ en base a esta ecuación e indique el orden de magnitud del tiempo que demoraría (no es necesario ser preciso, basta que diga si es lineal, cuadrático, logarítmico, exponencial, etc.)
b) A continuación, use una estrategia de tabulación para obtener un algoritmo más eficiente. Indique el orden de magnitud del tiempo que demoraría. 
c) Finalmente, resuelva analíticamente la ecuación para $T(n)$.

___
Tomando la sucesión de fibonacci con una resta:
$$
\begin{align}
 & f(n)=f(n-1)-f(n-2) \\
 & f(0)=0 \\
 & f(1)=1
\end{align}
$$
la secuencia es $0,1,1,0,-1,-1,0,1,1,\dots$ o sea se tiene un comportamiento *periódico u oscilatorio*.
\* Esto viene de resolver la ecuación con el polinomio característico haciendo $f(n)=\lambda^{n}$ como en [[Aux3#a)]]
___

##### a)
Para $T(n)=8T(n-1)-15T(n-2)$, con $T(0)=1,T(1)=1$ puede hacerse una función simple que retorne directamente lo de la llamada recursiva para el caso n-ésimo, o sea que haga `return 8*f(n-1) - 15*f(n-2)` y retorne los casos base directamente. Entonces:
```py
def t(n):
	if n==0:
		return 1
	elif n==1:
		return 1
	else:
		return 8*t(n-1)-15*t(n-2)
```
como la función **llama dos veces** a ella misma por cada ejecución, se puede ver la situación como:
$$
\underbrace{ 2 }_{ 1 \text{ vez} }\cdot\underbrace{ 2 }_{ 2\text{° vez} }\cdot 2\cdot 2 \dots \underbrace{ 2 }_{ n\text{ veces} } = 2^{n}
$$
luego, tiene complejidad del orden de $O(2^{n})$

##### b)
Estrategia de tabulación es la [[Diseño de Algoritmos#Programación Dinámica|programación dinámica]].
en pseudocódigo:
```
se def t(n) nueva:
	si no tiene la sol para n
		se implementa recursivamente
```
de la forma
```py
def t(n):
	Taux = np.zeros(n+1, dtype=int)
	
	def t_rec(k):
		if k>0 and Taux[k] == 0: # hay un 0 en la pos: no se ha implementado
			if k<=1:   # caso base, llega a 1
				Taux[k] = k
			else:   # casos recursivos
				Taux[k] = 8*t_rec(k-1) - 15*t_rec(k-2)
		return Taux[k]   #entregar solucion para valor pedido
	
	return t_rec(n)
```
usando esta forma de resolución se tiene una complejidad de orden lineal: $\Theta(n)$ pues un caso se resuelve una única vez, y si se tienen $n$ llamadas, se resuelve sólo una vez cada una.

##### c)
Se desarrolla analíticamente haciendo el cambio de variable usual para recurrencia homogénea de coeficientes constantes: $T(n)=\lambda^{n}$ igual que en [[Aux3#a)]].

# P3
Se tiene algo similar a [[Tarea 3]]. La diferencia es que se descarta el tramo en donde se encuentre el número mayor.

Para justificar la complejidad del orden $\Theta(\log n)$:
Utilizando el teorema maestro, para tener una complejidad de $\Theta(\log n)$ se debe tener que $r=0$ entonces no debe tener término 'extra', o sea se requiere que el algoritmo sea de la forma:
$$
T(n) = p\cdot T\left( \frac{n}{q} \right)+C\cdot n^{r=0} \implies T(n)=p\cdot T\left( \frac{n}{q} \right)
$$
esto significa que se debe dividir para reinar.