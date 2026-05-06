# P1
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