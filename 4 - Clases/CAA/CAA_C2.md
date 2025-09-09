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

7. Sea $z=x+iy\neq 0$ se define:
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

*** 
Clase 09/09
# Límites y Continuidad
Como coincide el convergencia de sucesiones en $\mathbb{R}^{2}$ y $\mathbb{C}$, se heredan las nociones de continuidad y límites para funciones.
$$
f:\Omega \in \mathbb{C}\to \mathbb{C}
$$
por lo que no elaboraremos mayormente estos conceptos, asumidos aprendidos anteriormente.

Supongamos que $\Omega \subseteq \mathbb{C}$ es un abierto y que $z_{0}\in \Omega$, decimos que:
$$
\lim_{ z \to z_{0} } f(z)=L\in \mathbb{C}
$$
ssi para toda sucesión $Z_{n}\to z_{0}$ (con $z_{n} \neq z_{0}, \forall n  \in \mathbb{N}$, se tiene:
$$
f(Z_{n})\to L
$$

*def:*
diremos que $f$ es continua en $z_{0}\in \Omega$ si para toda sucesión $(Z_{n})_{n\geq 1}\subseteq \Omega$ tal que $Z_{n}\to Z_{0}$, se tiene:
$$
\lim_{ z \to z_{0} } f(z)=f(z_{0})
$$
o equivalentemente:
$$
\lim_{ z \to z_{0} } \lvert f(z)-f(z_{0}) \rvert =0
$$

*obs:*
1. Si lo anterior es cierto, para todo $z_{0}\in \Omega$, decimos simplemente que $f$ es continua en $\Omega$ y escribimos $f\in C(\Omega)$.
2. El álgebra compleja de límites se prueba a partir de $\mathbb{R}^{2}$.
   Por ejemplo, si
   $$
\lim_{ z \to z_{0} } f_{1}(z)=L_{1},\ \lim_{ z \to z_{0} } f_{2}(z)=L_{2}
$$
se tiene:
$$
\lim_{ z \to z_{0} } (f_{1}(z)+f_{2}(z))=L_{1}+L_{2},\ \lim_{ z \to z_{0} } (f_{1}(z)\cdot f_{2}(z))=L_{1}\cdot L_{2}
$$

Dado $z\in \mathbb{C}$, $f(z)$ tiene parte real e imaginaria, luego:
$$
f(z)=u(z)+i\ v(z)
$$
o bien,
$$
f(z)=u(x,y)+i\ v(x,y), z=x+iy
$$
donde $u=u(x,y),v=v(x,y)$ son a valores reales.
Con esto $f=u+iv$ es continua en $z_{0}=x_{0}+iy_{0}$ ssi $u:\Omega\to \mathbb{R}$ y $v:\Omega\to \mathbb{R}$ son continua en $(x_{0},y_{0})$

***ejemplo***
Si $f(z)=z^{2}$ con $z=x+iy$
entonces:
$$
f(z)=(x+iy)^{2}=x^{2}-y^{2}+i 2xy
$$
como $u,v$ con continuas en todo $\mathbb{R}2$ se tiene que $f$ es continua en todo $\mathbb{C}$
> para ver la continuidad de la función compleja, solo se necesita ver la continuidad de su parte real e imaginaria.

2)
Si $f(z)=\frac{1}{z}$, con $z=x+iy\neq 0$, entonces
$$
f(z)=\frac{1}{x+iy}=\frac{x}{x^{2}+y^{2}}-i \frac{y}{x^{2}+y^{2}}
$$
donde 
$$
u(x,y)=\frac{x}{x^{2}+y^{2}},v(x,y)=\frac{y}{x^{2}+y^{2}}
$$
como $u,v$ continua en $\mathbb{R}^{2} - \{ (0,0) \}$, se tiene que $f$ es continua en $\mathbb{C}\setminus0$

# Derivada Compleja
*def:*
Sea $\Omega in\mathbb{C}$ un abierto y $f:\Omega\to \mathbb{C}$
1. Diremos que $f$ es derivable $z_{0}\in \Omega$ si existe el límite:
   $$
f'(z_{0})=\lim_{ z \to z_{0} } \frac{f(z)-f(z_{0})}{z-z_{0}}
$$
cuyo valor $f'(z_{0})$ le llamaremos la derivada de $f$ en $z_{0}$

2. Si $f$ es derivable en toda $z_{0}\in \Omega$, diremos que es holomorfa en $\Omega$

3. El conjunto de todas las funciones holomorfas en $\Omega$ se denota $H(\Omega)$, es decir:
   $$
H(\Omega)=\{ f:\Omega\to \mathbb{C}:f\text{ es holomorda en }\Omega \}
$$

*obs:*
Notemos que si $f$ es derivable en $z_{0}$, entonces
$$
f(z)=f(z_{0})+f'(z_{0})(z-z_{0})+r(z-z_{0})
$$
donde
$$
\lim_{ h \to 0 } \frac{r(h)}{h}=0
$$
en particular, si $f$ es diferenciable en $z_{0}$ entonces es continua en $z_{0}$

Supongamos que $f=u+iv:\Omega \subseteq \mathbb{C}\to \mathbb{C}$ es derivable en $z_{0}=x_{0}+iy_{0}\in \Omega$, tomando $z=z_{0}+h,h\in \mathbb{R}$ entonces:
$$
\begin{align}
\frac{f(z)-f(z_{0})}{z-z_{0}} & =\frac{f(z_{0}+h)-f(z_{0})}{h} \\
 & =\frac{u(x_{0}+h,y_{0})+iv(x_{0}+h,y_{0})-u(x_{0},y_{0})-i\ v(x_{0},y_{0})}{h} \\
 & =\frac{u(x_{0}+h,y_{0})-u(x_{0},y_{0})}{h}+i\ \frac{v(x_{0}+h,y_{0})-v(x_{0},y_{0})}{h}
\end{align}
$$
tomando $h\to 0$:
$$
\begin{align}
f'(z_{0}) & =\lim_{ h \to 0 } \frac{f(z_{0}+h)-f(z)}{h} \\
 & =\frac{ \partial u(x_{0},y_{0}) }{ \partial x } +i\ \frac{ \partial v(x_{0},y_{0}) }{ \partial x }
\end{align}
$$
del mismo modo, para $z=z_{0}+ih$, con $h\in \mathbb{R}$, se tiene:
$$
\begin{align}
\frac{f(z)-f(z_{0})}{z-z_{0}} & =\frac{f(z_{0}+ih)-f(z_{0})}{ih} \\
 & =\frac{u(x_{0},y_{0}+h)+i\ v(x_{0},y_{0}+h)-u(x_{0},y_{0})-i\ v(x_{0},y_{0})}{i\ h} \\
 & =\frac{-iu(x_{0},y_{0}+h)+v(x_{0},y_{0}+h)}{h}--i\frac{u(x_{0},y_{0})+v(x_{0},y_{0})}{h} \\
 & =\frac{v(x_{0},y_{0}+h)-v(x_{0},y_{0})}{h}-i \frac{u(x_{0},y_{0}+h)-u(x_{0},y_{0})}{h}
\end{align}
$$
y tomando $h\to 0$ se tiene
$$
f'(z_{0})=\frac{ \partial v(x_{0},y_{0}) }{ \partial y } -i\ \frac{ \partial u(x_{0},y_{0}) }{ \partial y } 
$$

Por unicidad de límite, se tiene:
$$
\begin{align}
\frac{ \partial u(x_{0},y_{0}) }{ \partial x } =\frac{ \partial v(x_{0},y_{0}) }{ \partial y }  \\
\frac{ \partial u(x_{0},y_{0}) }{ \partial y } =-\frac{ \partial v(x_{0},y_{0}) }{ \partial x } 
\end{align}
$$
son las conficiones de Cauchy-Riemann

*obs:*
El desarrollo anterior nos asegura que las condiciones de Cauchy-Riemann son necesarias para que $f$ sea derivable en $z_{0}$

Veamos ahora que las condiciones son suficientes. Para ello, notemos que si $f$ es derivable en $z_{0}$, entonces existe un complejo $f'(z_{0})=a+ib$ tal que:
$$
\lim_{ z \to z_{0} } \frac{\lvert f(z)-f(z_{0})-(a+ib)(z+z_{0}) \rvert}{\lvert z-z_{0} \rvert }=0
$$

Como 
$$
(a+ib)(z-z_{0})= \left( \begin{matrix}
a &-b \\
b & a
\end{matrix} \right) 
\left( \begin{matrix}
x-x_{0} \\
y-y_{0}
\end{matrix} \right) 
$$
donde $z=x+iy$ y $z_{0}=x_{0}+iy_{0}$,
se tiene que la derivada de $f$ en $z_{0}$ equivale a:

$$
\lim_{ (x,y) \to (x_{0},y_{0}) } \frac{\lvert \lvert \left( \begin{matrix}
u(x,y) \\
v(x,y) 
\end{matrix} \right)-\left( \begin{matrix}
u(x_{0},y_{0}) \\
v(x_{0},y_{0})
\end{matrix} \right) -\left( \begin{matrix}
a&-b \\
b&a
\end{matrix} \right) \left( \begin{matrix}
x-x_{0} \\
y-y_{0}
\end{matrix} \right)   \rvert  \rvert }{\left| \left| \left( \begin{matrix}
x-x_{0} \\
y-y_{0}
\end{matrix} \right)  \right|  \right| }
$$

## Teorema
Una función de variable compleja $f:\Omega \subseteq \mathbb{C}\to \mathbb{C}$ es derivable en $z_{0}\in \Omega$ ssi 
es Fréchet-derivable en $(x_{0},y_{0})$ como función de $\mathbb{R}^{2}$ en $\mathbb{R}^{2}$ y además se satisfacen las condiciones de Cauchy-Riemann:
$$
\begin{align}
\frac{ \partial u(x_{0},y_{0}) }{ \partial x } =\frac{ \partial v(x_{0},y_{0}) }{ \partial y }  \\
\frac{ \partial u(x_{0},y_{0}) }{ \partial y } =-\frac{ \partial v(x_{0},y_{0}) }{ \partial x } 
\end{align}
$$
En tal caso:
$$
f'(z_{0})=\frac{ \partial u(x_{0},y_{0}) }{ \partial x } +i\ \frac{ \partial v(x_{0},y_{0}) }{ \partial x } 
$$

***EJEMPLO:***
1)
Sea $f(z)=z^{2}=x^{2}-y^{2}+i 2xy$, donde
$$
u(x,y)=x^{2}-y^{2}, v(x,y)=2xy
$$
son Fréchet-diferenciable en todo $\mathbb{R}^{2}$, y además:
$$
\frac{ \partial u(x,y) }{ \partial x } =2x =\frac{ \partial v(x,y) }{ \partial y } 
$$
y
$$
\frac{ \partial u(x,y) }{ \partial y } =-2y=-\frac{ \partial v(x,y) }{ \partial x }
$$
osea se cumple la condición Cauchy-Riemann.
Luego, 
$$
\begin{align}
f'(z_{0}) & =2x_{0} + i 2y_{0} \\
 & =2(x_{0}+i y_{0}) \\
 & = 2z_{0}
\end{align}
$$

2)
Sea 
$$
f(z)=z^{3}=(x_{0}+iy_{0})^{3}=\underbrace{ x^{3}-3y^{2}x }_{ u(x,y) }+i\underbrace{ (3x^{2}y-y^{3}) }_{ v(x,y) }
$$
luego, $f$ es diferenciable y además:
$$
\begin{align}
\frac{ \partial u(x,y) }{ \partial x }=3xy^{2}-3y^{2}=\frac{ \partial v(x,y) }{ \partial x }  \\
\frac{ \partial u(x,y) }{ \partial y } =-6xy =- \frac{ \partial v(x,y) }{ \partial x }  
\end{align}
$$
entonces cumple la condición cauchy-riemann.
Luego,
$$
f'(z_{0})=3x_{0}^{2}-3y_{0}^{2}+i 6x_{0}y_{0}=3(x_{0}^{2}-y_{0}^{2}+i 2x_{0}y_{0})=3z_{0}^{2}
$$

**ejercicio**
Estudiar la derivada de $f(z)=z^{K}, K\in \mathbb{N}$
recordar que $f'(z_{0})=Kz_{0}^{K-1}$
\*apunte de felipe álvarez




*obs:*
si $f=u+iv$ es derivable en el sentido complejo en $\Omega \subseteq \mathbb{C}$ y $u,v$ son además de clase $\mathcal{C}^{2}(\Omega)$, entonces las funciones $u,v$ son armónicos, esto es:
$$
\begin{align}
\Delta u=
\end{align}
$$