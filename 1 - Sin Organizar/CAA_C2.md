# Funciones de Variable Compleja

## Conceptos Básicos
Consideremos $f:\Omega \subseteq \mathbb{R}^{2}\to\mathbb{R}^{2}$, $\Omega$ abierto, $f$ diferenciable y considerando a $\mathbb{R}^{2}$ dotado de la operación producto.
Así $\mathbb{C}$ es el cuerpo (a partir de $\mathbb{R}^{2}$) con su suma habitual, y el producto será de la forma:
$$
(a,b)(c,d)=(ac-bd,ad+bc)
$$

El producto complejo se puede escribir de manera más simple de manera matricial, de forma:
$$
(a,b)(c,d)=
\left( \begin{matrix}
a & -b \\
b & a
\end{matrix} \right) 
=
\left( \begin{matrix}
c \\
d
\end{matrix} \right)
=
\left( \begin{matrix}
ac-bd \\
ad+bc
\end{matrix} \right) 
$$

Denotamos, en llugar de la notación de pares ordenados, tomando:
$$
i=(0,1),\ 1=(1,0)
$$
entonces se tiene:
$$
(a,b)=a+bi
$$
Con esto, resulta que:
$$
i\cdot i =i^{2}=-1
$$
y naturalmente:
$$
\begin{align}
(a,b)(c,d) & =(a+bi)(c+di) \\
\text{se toma como un binomio comun:} \\
 & =ac+adi+bci+bdi^{2} \\
 & =ac-bd+(ad+bc)i
\end{align}
$$

### Propiedades Números Complejos
Para un número complejo $z=x+iy$, se define
1. Parte real: $\mathrm{Re}(z)=x$
2. Parte imaginaria: $\mathrm{Im}(z)=y$
3. El conjugado: $\bar{z}=x-iy$

#### Propiedad
*prop:* para $z_{1},z_{2}\in \mathbb{C}$, se tiene que:
1. $\bar{z_{1}+z_{2}}=\bar{z_{1}}+\bar{z_{2}}$
2. $\bar{z_{1}\cdot z_{2}}=\bar{z_{1}}\bar{z_{2}}$
3. $\bar{z_{1}}=z_{1}\iff z_{1}\in \mathbb{R}$
4. $\bar{(\bar{z_{1}})}=z_{1}$ y además $z_{1}\bar{\cdot}z_{1}=x_{1}^{2}+y_{1}^{2}$ si $z_{1}=x_{1}+iy_{1}$
5. $\mathrm{Re}(z_{1})=\frac{1}{z}(z_{1}+\bar{z_{1}})$
6. $\mathrm{Im}(z_{1})=\frac{1}{z_{1}}(z_{1}-\bar{z_{1}})$

Sea $z=x+iy\neq 0$ se define:
$$
z^{-1}=\frac{\bar{z}}{z\cdot \bar{z}}=\frac{x}{x^{2}+y^{2}}-i \frac{y}{x^{2}+y^{2}}
$$
y de manera más general:
$$
\frac{a+ib}{c+id}=\frac{1}{c^{2}+d^{2}}(ac+bd+i(bc-ad))
$$

Dado $z=x+iy\in \mathbb{C}$, se define el módulo (valor absoluto o norma) como:
$$
\lvert z \rvert =\sqrt{ z \bar{z} }=\sqrt{ x^{2}+y^{2} }=\left| \left| (x,y) \right|  \right|
$$
con esto, podemos dar el **producto interno** en $\mathbb{R}^{2}$ la siguiente expresión en términos de números complejos:
$$
(x_{1},y_{1})\cdot(x_{2},y_{2})=x_{1}x_{2}+y_{1}y_{2}=\mathrm{Re}(z_{1} \bar{z_{2}})
$$
donde $z_{1}=x_{1}+iy_{1},\ z_{2}=x_{2}+iy_{2}$


## Topología en Complejos
En $\mathbb{C}$ podemos definir una topología. Para ello, se define el concepto de **distancia** (o métrica).

### Distancia en Complejos
Sean $z_{1},z_{2}\in \mathbb{C}$ se define la **distancia** como:
$$
d(z_{1},z_{2})=\lvert z_{1}-z_{2} \rvert 
$$

#### Propiedades
La distancia en complejos tiene las siguientes *propiedades:*
1. $d(z_{1},z_{2})=0\iff z_{1}=z_{2}$
2. $d(z_{1},z_{2})>0$
3. $\forall z_{1},z_{2},z_{3}\in \mathbb{C}:d(z_{1},z_{2})\leq d(z_{1},z_{3})+d(z_{3},z_{2})$
se cumplen las mismas propiedades que en $\mathbb{R}^{2}$

### Topología en Complejos
Con las propiedades de la distancia en complejos, se tiene:
1. Un conjunto $A\subseteq \mathbb{C}$ se dice abierto si para todo punto $z_{0}\in A$, existe un radio $\rho>0$ tal que el disco:
   $$
D(z_{0},\rho)=\{ z\in \mathbb{C}:\lvert z-z_{0} \rvert <\rho \}
$$
está contenido en $A$

2. Un conjunto $A\subseteq \mathbb{C}$ se dice cerrado si $A^{c  }=\mathbb{C}/A$ es un conjunto abierto.

3. Un conjunto abierto se dice acotado si existe un radio $\rho_{0}>0$ tal que $A\subseteq D(0,\rho_{0})$
   $$
\forall z\in A,\lvert z \rvert \leq M, \text{para algun }M \in \mathbb{R}
$$

4. Un conjunto $A\subseteq \mathbb{C}$ es compacto si es cerrado y acotado.
5. Una sucesión de números complejos $z_{n}=x_{n}+iy_{n}$ se dice que converge el complejo $z=x+iy$ y se escribe $z_{n}\to z$ si se tiene que 
   $$
\lim_{ n \to \infty } \lvert z_{n}-z \rvert =0
$$
o equivalentemente si se tiene que $x_{n}\to x$ e $y_{n}\to y$ como sucesiones de números reales.

## Complejo como Par Ordenado
Consideremos $z=x+iy\in \mathbb{C}$ que corresponde a un número $P$ de coordenadas $x$ e $y$: 
***grafico punto P como par ordenado***

Si escribimos en coordenadas polares, se tiene que:
$$
z=x+iy=r\cos \theta+i\ r \sin \theta
$$

***mismo grafico pero con valores correspondientes*** 
pero no hay una única forma de escribir $\theta$ por periodicidad. Entonces, para evitar ambigüedad se restringen los valores de $\theta$ de la forma:
$$
\theta \in (-\pi,\pi]
$$
osea, puede dar sólamente una vuelta. Y en cuyo caso, se dice que $\theta$ es el **valor principal** del argumento de $z$ y se escribe como:
$$
\theta=\text{arg}(z)
$$

\*más adelante se verá que es posible darle sentido a la función exponencial evaluada en un numero complejo, y con ello obtener la fórmula de euler:
$$
e^{ i\theta }=\cos \theta+i\sin \theta
$$
lo que permite escribir 
$$
z=re^{ i\theta }=\lvert z \rvert e^{ i\theta\text{arg}(z) }
$$
más aún, si $z_{1}=r_{1}e^{ i\theta_{1} },z_{2}=r_{2}e^{ i\theta_{2} }$, se tiene:
1. $z_{1}\cdot z_{2}=r_{1}r_{2}e^{ i(\theta_{1}+\theta_{2}) }$
2. $\frac{z_{1}}{z_{2}}=\frac{r_{1}}{r_{2}} e^{ i(\theta_{1}-\theta_{2}) }, \text{si }r_{2}>0$

así
$$
\text{arg}(z_{1}z_{2})=\text{arg}(z_{1})+\text{arg}(z_{2})\text{con mod }2\pi
$$
además como
$$
(e^{ i\theta })^{n}=e^{ i\theta }\cdot e^{ i\theta }\cdot\cdot\cdot e^{ i\theta }=e^{ i n \theta }
$$
se tiene la fórmula de Moivre:
$$
(\cos \theta+i\sin \theta)^{n}=\cos(n\theta)+i\sin(n\theta)
$$

Finalmente, dado $K\in \mathbb{N}$, las raíces k-ésimas de la unidad son aquellas que satisfacen:
$$
z^{k}=1
$$
luego,
$$
\begin{align}
z^{k}=1\iff r^{k}e^{ ik\theta } & \iff r^{k}=1,\ k\theta=0 \text{ (mod}2\pi) \\
 &\iff r=1,\ \theta=0, \frac{2\pi}{k},2\left( \frac{2\pi}{k} \right),\dots,(k-1) \frac{2\pi}{k} \\
 & \iff z=1,\ e^{ i 2\pi/k },\dots,e^{ i(k-1) 2\pi/k }
\end{align}
$$

*obs:* Esto nos dice que:
$$
e^{ i\pi }+1=0
$$

##### Ejemplo
si $K=2$, $z^{2}=1$
***grafica eje***

si $k=3,z^{3}=1$
***grafica ej2***

- [ ] agregar graficos
