Se van a ver formas de diseñar algoritmos que, en muchos casos, son más eficientes que una implementación común.

# Dividir para Reinar
Es un método que se basa en sub-dividir un problema, resolverlos recursivaente y combinar las soluciones.

## Multiplicación de Polinomios
Si se tienen dos polinomios, y se quiere multiplicarlos:
$$
A=2+2x+x^{2}
$$
$$
B=1-2x+3x^{2}
$$
si $C=A\cdot B$ es la multiplicación, en donde cada término de un polinomio se multiplica por todos los otros.
Se usa una forma de columnas: cada factor se ordena en su respectiva columna según el grado de $x$:
$$
\begin{matrix}
A = &  2 & + & 2x & + & x^{2} \\
B = & 1 & - & 2x & + & 3x^{2} \\
C= & 2 & + & 2x & + & x^{2} \\
 &  & - & 4x & - & 4x^{2} & - & 2x^{3} \\
  &  &  &  &  & 6x^{2} & + & 6x^{3} & + & 3x^{4} \\
C=  & 2 & - & 2x & + & 3x^{2} & + & 4x^{3} & + & 3x^{4}
\end{matrix}
$$
Se ve que hay un orden y, de hecho, si solo estuviese los coeficientes numéricos, se mantiene la estructura, pues se instalan en su posición correspondiente según el grado al que acompañan y se entendería el resultado de igual manera. Así, usando solo coeficientes numéricos:
```py
A = [2  2 1]
B = [1 -2 3]
```
y se multiplica cada elemento de los arreglos por todos los elementos del otro. Luego, *la cantidad de veces que se multiplican $n$ elementos* es de $n^{2}$. O sea, se tiene un algoritmo del orden de $O=(n^{2})$. La implementación sería:
Si se notan los índices de los polinomios iniciales `A` y `B`,
```py
A = [2  2 1]
B = [1 -2 3]
```
y, si se ve que $C$ es **una tabla**, en donde las columnas se enumeran desde el $0$:

| Índice | 0   | 1   | 2   | ... |
| ------ | --- | --- | --- | --- |
| C =    | 2   | +2  | 1   | ... |
|        |     | -4  | -4  | ... |
|        |     |     | 6   | ... |
La multiplicación entre $A$ y $B$ corresponde a la suma de los índices de los números que se multiplican, indica la columna a la que corresponden en $C$, además del grado de $x$ al que acompaña cada factor.
En pseuocódigo:
```py
check de igual grado
crear array de longitud 2n-1 con ceros
la mult de los nros se acumulan en la lista
C es el índice de C que es la suma de sus propios indices
```
es la implementación de orden $O(n^{2})$.

### Variación de mayor eficiencia: Algoritmo de Karatsuba
Si para los mismos $A,B$ se factorizan, se tienen polinomios de menor tamaño:
$$
A = 1+2x+3x^{2}+2x^{3}=(1+2x)+x^{2}(3+2x)
$$
$$
B = 4-2x+x^{2}-4x^{3} = (4-2x)+x^{2}(1-4x)
$$
y definiendo $A',A'',B',B''$ como los nuevos polinomios:
$$
A'=1+2x, A''=3+2x, \dots
$$
y para tener $C=A\cdot B$, se tendría que multiplicar, de la forma:
$$
C = A'B'+A''B'x^{2}+A'B''x^{2}+A''B''x^{4}=A'B'+(A''B'+A'B'')x^{2}+A''B''x^{4}
$$
ahora se tienen multiplicación de polinomios de grado $\frac{n}{2}$, en donde los términos que se multiplican por $x^{2},x^{4}$ es solamente *mover el resultado de la multiplicación numérica* en la lista $C$.
En este caso, **se dividió el ŕoblema original en tamaños menores del mismo**. O sea, para resolver el problema de tamaño $n$, se está pasando a un problema de resolver 4 multiplicaciones de tamaño $\frac{n}{2}$ más un trabajo para mezclar los resultados. Viendo la cantidad de operaciones:
$$
T(n)=4\cdot T\left( \frac{n}{2} \right)+n
$$
mezclar los resultados es de $n$ operaciones pues se recorre la lista de tamaño $n$.
Se tiene la forma del [[Análisis de Algoritmos#Teorema Maestro|teorema maestro]] y se analizan los casos según $p,q,r$. Finalmente se tiene $p=4,q=2,r=1$ y se tiene que $2^{1}<4\iff q^{r}<p$, entonces:
$$
T(n)=\Theta(n^{\log_{q}p})\iff T(n)=\Theta(n^{\log_{2}4})=\Theta(n^{2})
$$
No se tiene un algoritmo de menor complejidad que el inicial, pues se sigue teniendo $n^{2}$ de cota superior.
Para mejorarlo, se definen nuevos polinomios $E,F,G$ de la forma:
$$
E=A\cdot B,\ F =A''\cdot B'',\ G=(A'+A'')\cdot(B'+B'')=A'B'+A'B''+A''B'+A''B''
$$
y el término central de $C$ es $G-E-F=\cancel{ A'B' }+A'B''+A''B'+\cancel{ A''B'' }$. Así, *se reemplazó una multiplicación por una suma*. Y se tiene un problema de la forma:
$$
T(n) = 3\cdot T\left( \frac{n}{2} \right)+C_{n}
$$
y se bajó a tres multiplicaciones, aumentando un poco el trabajo al término que redistribuye los resultados. Luego, con el teorema maestro se tiene que la complejidad del algoritmo es del orden de $\Theta(n^{1,59})$

## Ejemplo: Ejercicio 4

Se tiene una lista $A$ que consta de un conjunto de números ceros seguidos por un conjunto de números unos. Un ejemplo de lista $A$ es el siguiente:
$$
A = [0,0,0,0,0,0,0,0,0,1,1,1]
$$
Implemente la función "contar_ceros" que use la estrategia "dividir para reinar" y que devuelve la cantidad de ceros de la lista de entrada en tiempo $O(\log{n})$

```py
def contar_ceros(A, i, j):
  # Se entrega una lista de ceros contiguos, entonces el índide del último es la cantidad de ceros que hay
  # Para una última llamada de la función, como i es en donde empieza a buscar, es también la cantidad de ceros cuando se llega al ultimo 0 de los contiguos en la lista

  # Se va a usar recursión, en donde:
  # Caso Base: En la recusión final, se tiene un solo elemento: i = j entonces si este es 0, se 
  # retorna el indice siguiente
  if (i == j):
    if (A[i] == 0):
      return (i + 1)
    else:
      return i

  # Como se va dividiento lista, la suma de i,j (son sus nuevos inicios y fin) es la longitud de ella
  mitad = (i + j) // 2
  #si nro es 1:
  if A[mitad] == 1:
    # Usar recursivamente a la izq
    return contar_ceros(A, i, mitad)
  else:
    # se tiene 0, usar recursivamente a la der
    return contar_ceros(A, mitad + 1 , j )

```



# Programación Dinámica
Viendo el cálculo del n-ésimo término de la serie de fibonaci, antes de hizo un algoritmo con recursividad. El cual tiene una complejidad del orden de $\Theta(\phi^{n})$, esto pues para tener la serie de fibonacci para un término, se tiene una especie de árbol, en donde las cantidades de operaciones que hace cada rama es similar:
Para tener $f(5)$, se debe hacer $f(4)$ que, a su vez, requiere $f(3)$ y así sucesivamente.

~~~mermaid
---
config:
  layout: elk
---
graph TD
    f5["f(5)"] --> f4a["f(4)"]
    f5 --> f3a["f(3)"]
    f4a --> f3b["f(3)"]
    f4a --> f2a["f(2)"]
    f3a --> f2b["f(2)"]
    f3a --> f1a["f(1)"]
    f3b --> f2c["f(2)"]
    f3b --> f1b["f(1)"]
    f2a --> f1c["f(1)"]
    f2a --> f0a["f(0)"]
    f2b --> f1d["f(1)"]
    f2b --> f0b["f(0)"]
    f2c --> f1e["f(1)"]
    f2c --> f0c["f(0)"]
    f1a --> base1a["1"]
    f1b --> base1b["1"]
    f1c --> base1c["1"]
    f1d --> base1d["1"]
    f1e --> base1e["1"]
    f0a --> base0a["0"]
    f0b --> base0b["0"]
    f0c --> base0c["0"]
    
    classDef callNode stroke:#818cf8,fill:#eef2ff,color:#1e1b4b
    classDef baseNode stroke:#4ade80,fill:#f0fdf4,color:#1e1b4b
    class f5,f4a,f3a,f3b,f2a,f2b,f2c,f1a,f1b,f1c,f1d,f1e,f0a,f0b,f0c callNode
    class base1a,base1b,base1c,base1d,base1e,base0a,base0b,base0c baseNode
~~~
se ve que se recalculan muchas veces algunas llamadas de la función. Entonces se podría *memorizar* alguna parte del problema, para cuando se encuentra con un sub-problema, se guarda el resultado por si se necesita en otra parte y se tiene el resultado de inmediato, sin recalcular. En pseudocódigo:
```py
se define una fibonacci nueva
	y si no te tiene la solucion de una fibonacci
		se implementa recursivamente
```
```py
import numpy as np
def fibonacci(n):   # Se define una nueva fibonacci
    F=np.zeros(n+1,dtype=int)
    def fib_rec(k):
        if k>0 and F[k]==0: # primera vez que se calcula
            if k<=1:
                F[k]=k
            else:
                F[k]=fib_rec(k-1)+fib_rec(k-2)
        return F[k]
    return fib_rec(n)
```

Esto se puede implementar con un ficlo `for`, en donde se van sumando las series de fibonacci anteriores. Esto reduce la complejidad del problema al orden de $O(n)$.

Se puede mejorar la complejidad aún mas si se implementa un algoritmo que haga cambios de variable de la forma $g_{n}=f_{n-1}$.
Si se almacenan en una matriz, se termina usando el algoritmo binario, pero para matrieces:
$$
\begin{matrix}
f_{n} \\
g_{n}
\end{matrix}
= 
\left( \begin{matrix}
1 & 1 \\
1 & 0
\end{matrix}\right)
\left( \begin{matrix}
f_{n-1} \\
g_{n-1}
\end{matrix} \right)
$$
pasa a ser
$$
\left( \begin{matrix}
f_{n} \\
g_{n}
\end{matrix}\right)
=
\left( \begin{matrix}
1 & 1 \\
1 & 0
\end{matrix}\right)^{n}
\left( \begin{matrix}
1 \\
0
\end{matrix}\right)
$$
y se tiene que $f=A^{n}\cdot x$, en donde $A^{n}$ tiene complejidad $O(\log_{2}n)$

# Algoritmos Avaros (Greedy)
Se tiene una lista de actividades con sus asignaciones de horarios. Un conjunto de actividades que son compatibles de forma maximal (que no se solapen sus horarios) es, por ejemplo: $\{ a_{1},a_{3},a_{4},a_{6},a_{7} \}$, así estas actividades pueden suceder en una misma sala, pero en distintos horarios.
La información de las actividades se almacena en una lista, guardados los tiempos de inicios y fin de todas ellas:
$$
a_{k}=[t_{ini}^{k},t_{fin}^{k}]
$$
Luego, ordenando en una lista las actividades según sus tiempos finales: $(a1,a_{3},\dots,a_{8})$.
Para armar el conjunto solución:
1. En primer lugar se asume el primer elemento como parte de él. Entonces $a_{2}\in S$
2. Cuando se encuentra una actividad cuyo horario se solapa con el otro, no se incluye.

Este algoritmo está tomando decisiones que no son necesariamente correctas, pero que sí son óptimas, y toma el nombre de *greedy*.
Por ejemplo, la primera actividad podría no ser parte del conjunto solución $S$, pero si este no se incluye, igual se está resolviendo el problema. Entonces, se debe demostrar que el primer elemento es parte de la solución. Usando un razonamiento similar a la contradicción:
* Para el conjunto solución $S$ anterior. Sea $a_{k},k\neq 1$ el primer elemento (o sea uno distinto de $a_{1}$).
  Como $a_{k}\in S$, entonces se sabe que *no* se solapan sus horarios con las siguientes actividades.
  Como $a_{k}\neq a_{1}$ y viene después, entonces es una actividades que termina después de $a_{1}$.
  Si se elimina la actividad $a_{k}$, $a_{1}$ cumple con que su horario no se solapa con el resto de actividades, entonces $a_{1}\in S$.

# Backtracking
Para un problema que solo se puede resolver probando todas las combinaciones posibles. Este algoritmo hace que se busquen varias formas de solución hasta que se dé con alguna.
*Ejemplo*: Robot en laberinto,
Un robot se ubica en una posición aleatoria y éste se puede mover solo horizontal y verticalmente.
Usando esta metodología, se evitan los casos duplicados (caminos probados que no funcionaron)
Se implementa una función que, recursivamente, comprueba si se puede mover a un espacio contiguo. Pero esto genera un bucle pues cambiará de casilla y, en ella una posibilidad es devolverse a la misma.
Para evitar el bucle, se va a marcar la posición probada con una `x`.
Bajo este algoritmo, qué tan rápido se encuentre la solución depende de dónde empiece el robot y  del orden de comprobación entre las casillas.

- El algoritmo $A^{*}$ realiza lo mismo, pero le asigna una puntuación a cada posibilidad. Si la alternativa lo acerca a la solución, se le asigna un mayor puntaje y se toma la decisión con mayor puntaje.
