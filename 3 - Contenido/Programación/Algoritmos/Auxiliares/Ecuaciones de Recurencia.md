# Recurrencia Lineal
Una recurrencia lineal es homogénea cuando no hay término independiente (es decir, ningún término que dependa solo de $n$, sin involucrar a $T$).
La forma general de una recurrencia lineal es:
$$T(n) = c_1 T(n - 1) + c_2 T(n - 2) + \cdots + c_k T(n - k) + \underbrace{ f(n) }_{ \text{termino independiente} }$$
- Si $f(n) = 0$: homogénea
- Si $f(n) \neq 0$: no homogénea (o inhomogénea)

Entonces la *solución es de la forma* 
$$
T(n)=\lambda^{n}
$$
**Este tipo de solución se tiene para lineales y también a constantes.**
Luego, se reemplaza $T(n)=\lambda^{n}$