Se tiene un arreglo de tamaño $n$ y esta se sub-divide en un arreglo de tamaño $2\cdot\frac{n}{3}$ más una cantidad constante de procesos $C$ para obtener los sub-índices. Entonces se tiene:

$$
T(n)= T\left( 2\cdot\frac{n}{3} \right) + C_{n^{0}}=T\left( \frac{n}{\frac{3}{2}} \right) + C_{n^{0}}
$$
usando el teorema maestro, se identifican los elementos $p = 1$, $q = \frac{3}{2}$, $r = 0$ y se compara $q^{r}$ con $p$:
$$
q^{r} = \left( \frac{2}{2} \right)^{0}=1
$$
entonces $q^{r}=1=p$, luego, la complejidad es:
$$
T(n)=\Theta(n^{r} \log_{q}n)=\Theta(n^{0}\log_{2}n)=\Theta(\log_{2}n)
$$