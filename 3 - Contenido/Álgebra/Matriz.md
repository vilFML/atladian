[[Álgebra Lineal]]
***def:*** Una matriz A de *m* filas y *n* columnas con coeficientes en el cuerpo $\mathbb{K}$ (de ahora en adelante será $\mathbb{R} \text{ o }\mathbb{C}$) es una **tabla** de doble entrada:
$$
A = \begin{pmatrix}
a_{{11}} & \dots & a_{1n} \\
\vdots &  & \vdots \\
a_{m1} & \dots & a_{mn}
\end{pmatrix}\;,\; a_{ij} \in \mathbb{K},\; \forall i=1,\dots,m\;;j=1,\dots,n
$$
*notación:* La matriz A también se puede denotar como $A=(a_{ij})$
y también el conjunto de todas las matrices de *m* filas y *n* columnas con coeficientes en el cuerpo $\mathbb{K}$ = $\mathcal{K}_{mn}(\mathbb{K})$

## Igualdad de Matrices

***def***: Dadas dos matrices $A \in \mathcal{K}_{{mn}}(\mathbb{K}),\; B\in\mathcal{M}_{m'n'}(\mathbb{K})$, son **iguales** si:
- $m = m',\; n=n'$
y
- $\forall i=1,\dots,m\;;j=1,\dots,n$ se cumple que $a_{ij}=b{ij}$

### [[Vector]]
Un **caso especial** de matrices son las de $n \times 1$ , llamados **vectores** de $\mathbb{K}^n$. Esto es: los vectores son matrices de ***una sola columna***.