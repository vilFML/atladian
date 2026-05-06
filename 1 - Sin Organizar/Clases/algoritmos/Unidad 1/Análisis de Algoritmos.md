Las propiedades invariantes sirven para ver si un algoritmo cumple su función. Ahora, se va a analizar la eficiencia de los algoritmos.

# Tamaño
Cuando se habla de tamaño, se está hablando de la cantidad de 'cosas' que debe procesar, esto se representa con $n$.
Cuando se tiene un algoritmo, si se quiere contar el número de operaciones se ve que hay una función discreta $f(n)$ (no tiene propiedades continuas como derivada). Esta función se puede analizar para tener la cantidad de operaciones que hará el algoritmo.
Ej: $f(n)=3n^{2}+10n+3$, en donde se analiza el término $n^{2}$, despreciando $n$ para una cantidad muy grande de datos.

## Notaciones Orden De
Con las notaciones se permite ver si hay funciones que sean cota superior o inferior. Matemáticamente, si se tienen $f(n),g(n)$, se ve el 
$$
\lim_{ n \to \infty^{+} } \frac{f(n)}{g(n)} 
$$
Si se va a una constante, entonces $f(n)$ está acotada por $g(n)$.
### Notación $O()$

La notación $O()$ simplifica el análisis. Indica el elemento dominante de la función: $f(n)\in O(n^{2})$. Esto dice que $f(n)$ tiene un orden de $n^{2}$ y significa que:
$$
\forall n\geq n_{0}:f(n)\leq Cn^{2}
$$
con $C$ una constante.
Se puede visualizar gráficamente
> Gráfico n cuadrado vs f(n)

El significado es que bajo un mismo punto $n_{0}$, la función va por 'debajo' de una $f(n)$, y para cuando $n$ sea lo suficientemente grande, $f(n)$ no será mayor que $n^{2}$.
También se puede ver que hay una cota superior ($n^{2}$) para $f(n)$, que se denota con $\Omega()$

### Notación $\Omega()$
Esto dice que hay una función **cota inferior** de la forma:
$$
f(n) \in \Omega
$$
esto significa que
$$
\forall n\geq n_{0}:f(n)\geq C\cdot g(n)
$$
gráficamente:
> gráfico xde

### Notación $\Theta()$
La notación $\Theta()$ se utiliza para cuando hay una *banda* entre dos funciones distintas, en donde una es cota superior y otra es cota inferior. De la forma:
$$
f(n)\in \Theta(g(n))
$$
que significa que
$$
C_{1}\cdot g(n)\leq f(n)\leq C_{2}\cdot g(n), \forall n\geq n_{0}
$$
gráficamente:
> gráfico

luego, la notación $\Theta()$ indica una *cota justa*. 
\* La función por arriba y por abajo $g(n)$ es la misma.

Ejemplo: Para el algoritmo de selección se tiene que
$$
f(n)=\frac{n^{2}-n}{2}
$$
- ¿Es cierto que $f(n) \in O(n^{2})$? Esto es lo mismo que preguntar que, si por cota superior (el peor caso posible o lo que más se demora) sería de orden cuadrático.
Es cierto pues existe una constante tal que: $f(n)\leq n^{2}$ con $C = 2$ tal que
$$
f(n)=\frac{n^{2}-n}{2}\leq 2n^{2}
$$
- ¿Es cierto que $f(n) \in \Omega(n^{2})$? Es lo mismo que preguntar si por cota inferior (o el mejor caso posible para el algoritmo) es de orden cuadrático.
Es cierto pues se cumple que $f(n)=\frac{n^{2}-n}{2} \geq C\cdot g(n)$ para cualquier $C$

- ¿Es cierto que $f(n) \in \Theta(n^{2})$?
  Sí, pues se cumplen las dos anteriores, entonces se tiene una banda de trabajo.

Ejemplo 2: ¿Es cierto que $n^{2} \in O(n)$?
Esto es cierto si $\forall n\geq n_{0}:n^{2}\leq C\cdot n\iff n\cdot n\leq Cn\iff \forall n\geq n_{0}:n\leq C$.
Esto no se cumple, pues $n$ aumenta y no es siempre menor que una constante $C$

# Recurrencias
En la iteración es posible contar el número de operaciones (o es más simple), pero en recursividad se tiene un funcionamiento implícito. Y para analizar estas funciones:
Se escriben de la forma
$$
a_{n}=a_{n-1} + C_{n}
$$
con trabajo algebraico se llega a distintos casos.

## Forma 1

Cuando la función recursiva es de la forma
$$
a_{n}=a_{n-1}+C_{n}
$$
la cantidad de operaciones para $n$, se tiene con:
$$
a_{n}=a_{0}+\sum_{1\leq k<n}^{}C_{k}
$$

## Forma 2
Cuando la función recursiva tiene forma
$$
a_{n}=b\cdot a_{n-1}+C_{n}
$$
la cantidad de operaciones que se va a hacer para $n$ elementos, se tiene con:
$$
a_{n}=a_{0}\cdot b^{n}+\sum_{1\leq k<n}^{}C_{k}\cdot b^{n-1}
$$

## Forma fibonacci
También se tienen otras formas, como la serie de fibonacci:
$$
f_{n}=f_{n-1}+f_{n-2}
$$
en donde $f_{0}=0,f_{1}=1$.
Para esta forma se hace una suposición de que $f_{n}$ tiene forma exponencial: $f_{n}\approx \lambda^{n}$, y luego:
$$
\frac{\lambda^{n}}{\lambda^{n-2}}=\frac{\lambda^{n-1}}{\lambda^{n-2}}+\frac{\lambda^{n-2}}{\lambda^{n-2}},\lambda^{2}-\lambda+1\iff \lambda^{2}-\lambda-1=0
$$
usando bashkara se llega a que $\phi=\frac{1+\sqrt{ 5 }}{2},\hat{\phi}=\frac{1-\sqrt{ 5 }}{2}$, y $f_{n}$ es una combinación lineal de la soluciones. De la forma $f_{n}=A\phi^{n}+B\hat{\phi}^{n}$. Usando las condiciones iniciales, se llega a que $f_{n}=\frac{1}{\sqrt{ 5 }}(\phi^{n}-\hat{\phi}^{n})$
se debe ver que $\hat{\phi}$ tiene un valor menor que 1, luego al elevarlo a $n$, este tiende a $0$. Finalmente
$$
f_{n}=\Theta(\phi^{n})
$$

## Teorema Maestro
La cantidad de operaciones para resolver el problema de tamaño $n$, se deben hacer 'p' veces la misma, pero para un problema de tamaño $\frac{n}{q}$ mas una cantidad de trabajo general $C_{n}$:
$$
T(n)=p\cdot T\left( \frac{n}{q} \right) + C_{n^{r}}
$$
esto dice el tamaño al resolver un problema que **se subdivide**.
Para resolver, se identifican los parámetros $p, q, r$ en lo que se tenga, y se tiene una complejidad según los casos:
1. Si $q^{r}<\implies T(n)=\Theta(n^{\log_{q}p})$
2. Si $q^{r}=p\implies T(n)=\Theta(n^{r}\log_{q}n)$
3. Si $q^{r>p}\implies T(n)=\Theta(n^{r})$

### Pasos comunes resolución
1. Ajustar forma de $T(n)$ para llevarlo a teorema.
2. Identificar $p,q,r$
3. Ver el caso que se tenga de $q^{r} <,=,> p$
4. Aplicar teorema según el caso.