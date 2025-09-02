Materia: Cálculo Avanzado y Aplicaciones
	Fecha cátedra: 05/08/25
	Fecha digitalización: 06/08/25
	*tags: #Educación #Cálculo/CálculoAvanzado

Materia:
# [[Campo Escalar]]
Sea $\Omega \subseteq \mathbb{R}^{3}$ abierto y no vacío,
un **campo escalar** es una aplicación $f:\Omega \to \mathbb{R}$, que asigna a cada $\vec{x} \in \Omega$ una función:
$$
f=f(\vec{x})
$$

# [[Campo Vectorial]]

Se puede definir en $\mathbb{R}^n$, pero se definirá sólo en $\mathbb{R}^{2}, \mathbb{R}^{3}$ por su uso en física.

***def:*** Campo vectorial
Es una aplicación $\vec{F}:\Omega \subseteq \mathbb{R}^{3} \to \mathbb{R}^{3}$, de la forma
$$
\vec{F}=\vec{F}(\vec{x})
$$
*obs:* en cartesianas se tiene que
$$
\vec{F}(\vec{x})=F_{1}(\vec{x})\hat{i}+F_{2}(\vec{x})\hat{j}+F_{3}(\vec{x})\hat{k}
$$
donde $\vec{F}_{i}(\vec{x})$ son [[Campo Escalar|campos escalares]].

*ej:* los puntos de un disco plano que gira en sentido antihorario, con velocidad angular $\omega>0$ constante y de radio $r=1$, tiene como campos de velocidad:
![[Pasted image 20250828111223.png]]

$$
\implies  \vec{v}(x,y,0)=-\omega y \hat{i} + \omega x \hat{j}+0\hat{k}
$$
ej2:Gravitación universal
ej3: gravitación cerca de la tierra

# Integración en Curvas N-Dimensionales
Para integrar en $\mathbb{R}^n$ se requiere un conjunto [[Jordan-medible]]. Esto es equivalente a decir que el 'borde' tenga medida 0, por ejemplo: el volumen; pero una curva no tiene volumen, entonces, se definen para integrar una curva:

### [[Curva Continua]]
*def:* 
Una curva continua en $\mathbb{R}^n$ es un par $(\Gamma,\vec{\gamma})$, donde:
$\Gamma=\vec{\gamma}([a,b])$

y $\vec{\gamma}:[a,b]\to \mathbb{R}^n$ es continua, llamada [[parametrización]] de $\Gamma$, donde
$$
\vec{\gamma}(t)=\left(\begin{matrix}
\gamma_{1}(t) \\
\vdots \\
\gamma_{n}(t)
\end{matrix}\right)
= \gamma_{1}(t)e_{1}+\dots+\gamma_{n}(t)e_{n}
$$
así, se define una curva como un par $(\Gamma,\vec{\gamma})$ correspondiente al gráfico, y una [[parametrización]].
*obs:* no se indica siempre una curva con el par y su parametrización, si no que solamente se escribe $\vec{\gamma}$

###### Ejemplo: Las parametrizaciones
$\vec{\gamma}_{1}(t)=(t^{2},t^{4}), \text{con }0\leq t\leq \sqrt{ 2 }$
$\vec{\gamma}_{2}(t)=( (1+t),(1+t)^{2}), \text{ con }-1\leq t\leq 1$
ambas representan el arco parabólico $y=x^{2}$ que va desde $(0,0) \to(2,4)$ 

- Una misma curva puede estar dadas por parametrizaciones distintas
- Ambas van en la misma dirección: aumentan en el mismo sentido, no es la misma curva si no crecen en la misma dirección.
![[Pasted image 20250828111843.png]]

### [[Traza]]
*def:* 
diremos que un punto $x_{0}$ está sobre $\Gamma$ si existe 
$$
t_{0} \in [a,b]\text{ tq: }\vec{x_{0}}=\vec{\gamma}(t_{0})
$$
la colección de todos aquellos puntos se llama la **traza** de la curva $\Gamma$ y se denota $\text{tr}(\Gamma)$
	la traza corresponde a los puntos que pertenecen a la curva, esto es efectivamente el grafo de la curva.
##### ej: 
las parametrizaciones
$$
\begin{align}
\vec{\gamma}_{1}(t)=(\cos(t), \sin(t)), &\; 0\leq t\leq 2\pi  \\
\vec{\gamma}_{2}(t)=(\cos(3t),\sin(3t)), & \; 0\leq t\leq 2\pi \\
\vec{\gamma}_{3}(t)=(\sin(t),\cos(t)), & \; 0\leq t\leq2\pi
\end{align}
$$
tienen la misma traza (la circunferencia $x^{2}+y^{2}=1$), pero la recorren de forma diferente, pues 
- $\vec{\gamma}_{1}$ recorre la circunferencia 1 vez.
- $\vec{\gamma}_{2}$ recorre la circunferencia 2 veces.

### [[Curva cerrada]]
Dada una curva $(\Gamma,\vec{\gamma})$, con los puntos $\vec{\gamma}(a)\text{ y}\; \vec{\gamma}(b)$ los puntos inicial  y final respectivamente, si:
$$
\vec{\gamma}(a)=\vec{\gamma}(b)
$$
se dice que la **curva es cerrada**.
	si la curva vuelve al mismo punto, entonces es cerrada

### [[Curva simple]]
Dada una curva $(\Gamma,\vec{\gamma})$, si
$$
\begin{matrix}
\vec{\gamma}(t_{1}) \neq \vec{\gamma}(t_{2}), & \text{para }a\leq t_{1} < t_{2} < b \\
 & \text{o para }a\leq t_{1}<t_{2}\leq b 
\end{matrix}
$$
entonces la ***la curva es simple***
	cuando la curva no se intersecta a sí misma, entonces la curva es simple (no hay nudos).
### [[Curva de Jordan]]
*def:*
una curva se llama **de jordan** si ella es [[curva cerrada|cerrada]] y [[Curva simple|simple]].

recordemos que la derivada de una función $\gamma:[a,b]\to \mathbb{R}^{n}$ es:
$$
\vec{\gamma}'(t)=
\left( \begin{matrix}
\gamma_{1}'(t) \\
\gamma_{2}'(t) \\
\vdots \\
\gamma_{n}'(t)
\end{matrix} \right)
= \gamma_{1}'(t)e_{1}+\gamma_{2}'(t)e_{2}+\dots+\gamma_{n}'(t)e_{n}\text{ , con } t \in [a,b]
$$
*obs:* $\vec{\gamma}'(a),\;\vec{\gamma}'(b)$ deben ser interpretadas como derivadas a la izquierda y derecha, respectivamente.
![[Pasted image 20250828112103.png]]

### [[Curva suave]]
Una curva es suave (o de [[clase C1]]) si su parametrización $\vec{\gamma}:[a,b]\to \mathbb{R}^{n}$ es continuamente diferenciable y además:
$$
\vec{\gamma}'(t) \neq \left(\begin{matrix}
0 \\
\vdots \\
0
\end{matrix} \right), \forall t\in[a,b]
$$

las curvas se pueden concatenar:
![[Pasted image 20250828112140.png]]
### 
si $\gamma_{1}:[a_{1},b_{1}],\;\gamma_{2}:[a_{2},b_{2}]$ son parametrizaciones de $\Gamma_{1},\Gamma_{2}$ respectivamente, C1 por tramos y tal que $\vec{\gamma}_{1}(b_{1})=\vec{\gamma}_{2}(a_{2})$, entonces:
$$
\vec{\gamma}:[a_{1},b_{1}+b_{2}-a_{2}]\to \mathbb{R}^{n}
$$
definida por
$$
\vec{\gamma}(t)=
\left\{
	\begin{array}{ll}
		 \vec{\gamma}_{1}(t)\;,\;t\in[a,b] \\
\vec{\gamma}_{2}(a_{2}+t-b_{1})\;,\;t\in [b_{1},b_{1}+b_{2}-a_{2}]
	\end{array}
\right.
$$
es una parametrización de la curva $\Gamma$, de la forma:
$$
\Gamma=\Gamma_{1}\cup\Gamma_{2}
$$
y se denota como la suma de ambas:
$$
\Gamma=\Gamma_{1}+\Gamma_{2}
$$

*obs:* una curva $\Gamma$ se dice seccionalmente suave si $\Gamma=\Gamma_{1}+\Gamma_{2}+\dots+\Gamma_{n}$, donde $\Gamma_{i}$ son suaves. O sea una curva es seccionalmente suave si se puede escribir como unión de curvas suaves.

***
# Clase 2, 07/08
#### Ejemplos curvas suaves
##### Ejemplo 1: Circunferencia
La circunferencia de centro (0,0) es una curva suave. En efecto, puede ser representada por:
$$
\begin{align}
 & \vec{\gamma}(t)=(\cos t,\sin t),\; 0\leq t\leq 2\pi \\
\implies  & \vec{\gamma}'(t) = (-\sin t,\cos t), 0\leq t\leq 2\pi
\end{align}
$$
donde $\vec{\gamma}'$ es continua, y además $\vec{\gamma}'\neq(0,0),\; \forall t \in [0,2\pi]$

###### Ejemplo 2:
La curva dada por
$$
\vec{\gamma}=(t-\sin t,1-\cos t),\; -2\pi \leq t \leq 2\pi
$$
es **seccionalmente suave**. En efecto:
$$
\begin{align}
\vec{\gamma}'(t)=(1-\cos t,\sin t),\; t \in [-2\pi, 2\pi] \\
\vec{\gamma}'(t)=(0,0) \iff t=-2\pi,0,2\pi \\
\end{align}
$$
![[Pasted image 20250828112530.png]]
	se sacan las 'puntas' y se secciona en 2 curvas $\Gamma_{1},\Gamma_{2}$

# Recta tangente
Para una curva suave, en el punto $x_{0}=\vec{\gamma}(t_{0})$, se puede definir la recta tangente:
$$
x=x_{0}+s\;\vec{\gamma}(t_{0}),\;s \in \mathbb{R}^{n}
$$
* es la recta tangente común que pasa por un punto.
y $\vec{\gamma}(t_{0})\neq_{0}$ es un vector tangente a la curva. Esto dice que $\Gamma$ puede representar una trayectoria recorrida por una partícula en el instante 't', mediante $\vec{\gamma}(t)$,y el vector $\vec{\gamma}'(t)$ representa la velocidad de la partícula en instante 't'.

# Orientación o Sentido
En física se define un sistema de referencia (Origen, sentidos positivos y negativos). De esto se tiene la noción de sentido y dirección de una curva, por lo que recorrer una curva en sentidos distintos no son lo mismo.

Una curva puede ser recorrida en 2 sentidos opuestos, por ejemplo, si se tiene una parametrización $\vec{\gamma}:[a,b] \to \mathbb{R}^{n}$ que recorre la curva según:
$$
\tilde{\vec{\gamma}}(t)=\vec{\gamma}(b+a-t)
$$
ésta la recorre en el sentido 'opuesto'. Cuando una curva se recorre en el sentido opuesto se puede denotar como $\Gamma^{-} \text{ o }-\Gamma$
	Ejemplo: La parametrización del segmento de recta que una los puntos $x_{0},x_{1}\in \mathbb{R}^{n}$ está dada por:
	$\vec{\gamma}(t)=(1-t)x_{0}+tx_{1},\; t\in[0,1]$
	y la curva en el sentido opuesto **para este caso** es:
	$\tilde{\vec{\gamma}}(t)=tx_{0}+(1-t)x_{1},\; t\in[0,1]$

# Longitud de Curva
Dada una curva $\Gamma$ parametrizada por $\vec{\gamma}:[a,b] \to \mathbb{R}^{n}$ y sea $P=\{ t_{0}=a,t_{1},t_{2},\dots ,t_{n}=b \}$  una partición de $[a,b]$, se define:
$$
L_{p}(\Gamma)=\sum_{i=1}^{n}\lvert\lvert \vec{\gamma(t_{i})}-\vec{\gamma}(t_{{i-1}}) \rvert\rvert 
$$
![[Pasted image 20250828112711.png]]
	cuando se agregan puntos, se acerca a la longitud de la curva completa.

Se dice que $\Gamma$ es **rectificable** si el conjunto $\{ L_{p}(\Gamma),P \text{ es una partición de }[a,b] \}$ es acotado superiormente.
*recuerdo:* si el conjunto es acotado superiormente, entonces tiene supremo. Y tiene ínfimo por norma ser no negativa.
Y en cuyo caso, la longitud de la curva (o del arco) se define como:
$$
L(\Gamma)=\text{sup}\{ L_{p}(\Gamma),\;P\text{ es una partición de }[a,b] \}
$$

para tener la longitud $L_{P}(\Gamma)$ sin calcular supremo:
si se multiplica $L_{p}(\Gamma)$ por un 1 conveniente $=\frac{||t_{i}-t_{i-1}||}{||t_{i}-t_{i-1}||}$, o sea:
$$
L_{p}(\Gamma)=\sum_{i=1}^{n}\lvert\lvert \vec{\gamma(t_{i})}-\vec{\gamma}(t_{{i-1}}) \rvert\rvert · \frac{||t_{i}-t_{i-1}||}{||t_{i}-t_{i-1}||}
$$
el término 
$$
\frac{\lvert \lvert\vec{\gamma(t_{i})}-\vec{\gamma}(t_{{i-1}}) \rvert\rvert}{||t_{i}-t_{i-1}||}
$$
es similar a una **derivación**

#### Proposición
$\Gamma = \Gamma_{1}+\dots+\Gamma_{k}$ es **rectificable** $\iff \Gamma_{i},\;i\in \{ 1,\dots,k \}$ son rectificables, y en ese caso:
$$
L_{P}(\Gamma)=L(\Gamma_{1})+L(\Gamma_{2})+\dots+L(\Gamma_{k})
$$

#### Teorema
Si $\Gamma$ es una curva suave parametrizada por $\vec{\gamma}:[a,b] \to \mathbb{R}^{n}$, entonces $\Gamma$ es rectificable y se cumple que:
$$
L(\Gamma)=\int_{a}^{b} ||\vec{\gamma}'(t)||df
$$
* Si curva es suave, entonces se puede tener longitud
	*Ejemplo 1*: La longitud de un arco de la circunferencia de centro $(0,0) \text{ y }r>0$,
	$\Gamma:\vec{\gamma}(t)=(R\cos t,R\sin t),\; 0\leq t \leq 2\pi$
	en este caso se tiene que $a = 0,\; b=2\pi$, entonces:
	$L(\Gamma)=\int_{0}^{2\pi}||(-R\sin t,R\cos t)||dt$

	Ejemplo 2: Longitud del segmento de hélice curvo, parametrizada por: ...

# Integral de Línea (o de Trabajo)
Si se supone que la partícula se mueve a lo largo de una curva $\Gamma$ bajo la acción de un campo vectorial de fuerzas $\vec{F}$, se busca calcular el **trabajo realizado** por el campo de fuerzas sobre la partícula cuando ésta describe una curva.
Si $\Gamma$ es un desplazamiento rectilíneo dado por un vector $\vec{d}$, y $\vec{F}$ es constante, entonces $\mathbb{W}=\vec{F}\cdot\vec{d}$
Cuando $\Gamma$ no es una recta y $\vec{F}$ no es constante, se puede aproximar la curva $\Gamma$ por un número infinito de desplazamientos rectos:
![[Pasted image 20250828113241.png]]

Dada una parametrización de $\Gamma$ dada por $\vec{\gamma}:[a,b]\to \mathbb{R}^{n}$, si $\mathcal{f}$ varía en un intervalo pequeño de tiempo $[t_{i},t_{i}+\Delta t]$, la partícula se moverá entre $\vec{\gamma}(t_{i})$ y $\vec{\gamma}(t_{i}+\Delta t)$ en un **desplazamiento vectorial** dado por:
$$
\Delta  \vec{d}=\vec{\gamma}(t_{i}+\Delta t)-\vec{\gamma}(t_{i})
$$
y multiplicando por un 1 conveniente $= \frac{\Delta t}{\Delta t}$, queda término similar a derivada.
Por definición de derivada:
$$
\Delta  \vec{d}\approx  \vec{\gamma}'(t)\Delta t
$$
por lo tanto el trabajo realizado al ir desde $\vec{\gamma}(t_{i})$ hasta $\vec{\gamma}(t_{i}+\Delta t)$ es aproximadamente:
$$
\vec{F}(\vec{\gamma}(t_{i}))\Delta  \vec{d} \approx  \vec{F}(\vec{\gamma}(t_{i}))·\vec{\gamma}(t_{i})\Delta t
$$
Es posible tener el trabajo realizado para cada intervalo y luego sumarlos para obtener el trabajo total realizado. En efecto, si se divide $[a,b]$ en $n$ partes iguales: $a=t_{0}<t_{1}<t_{2}<\dots<t_{n}=b$, con $\Delta t=t_{i+1}-t_{i}$ entonces el trabajo realizado es aproximadamente:
$$
\mathbb{W}=\sum_{i}^n \vec{F}(\vec{\gamma}(t_{i})) \cdot  \vec{\gamma}(t_{i})\Delta t
$$
y, finalmente, tomando $n\to \infty$, queda:
$$
\mathbb{W}=\int_{a}^{b} \vec{F}(\vec{\gamma (t}))·\vec{\gamma}'(t)dt
$$
que corresponde a la **integral de línea**.


# 
Dada $\Gamma$ curva suave en $\mathbb{R}^n$ y $\vec{F}$ un campo vectorial continua y definido en $\text{tr}(\Gamma)$, entonces la integral de línea de $\vec{F}$ a lo largo de $\Gamma$ está definida como:
$$
\int_{\Gamma}\vec{F} d \vec{x} = \int_{a}^{b}\vec{F}(\vec{\gamma}(t))\vec{\gamma}'(t)dt
$$
donde $\vec{\gamma}:[a,b]\to \mathbb{R}^{n}$ es una parametrización de $\Gamma$
	es similar al teorema de cambio de variable, porque se pasa de un dominio 'raro' $\Gamma$ a uno en $\mathbb{R}$, y el término de la derivada es análogo al Jacobiano del cambio de variable.
***Es integral de línea pues el dominio de integración ($\Gamma$ en este caso) es una curva.

## con campo escalar:
si $\mathcal{f}$ es un campo escalar, se define la integral de línea de $\mathcal{f}$ sobre $\Gamma$ como:
$$
\int_{\Gamma}\mathcal{f} d \vec{x} = \int_{a}^{b}\mathcal{f}(\vec{\gamma}(t))·||\vec{\gamma}(t)||dt
$$

*Ejemplo*: si $\mathcal{f}$ es la densidad de masa de un alambre $\Gamma$, la integral representa la masa total de $\Gamma$


# Clase 12/08

## Integral de Línea
Si se tiene una curva seccionalmente suave $S:\Gamma=\Gamma_{1}+\Gamma_{2}+\dots+\Gamma_{n}$ y un campo vectorial $\vec{F}$ definido y contino sobre $\text{tr}(\Gamma)$, entonces
La integral de línea se define como:
$$
\int_{\Gamma}\vec{F} d \vec{x}=\sum_{i=1}^{n}\int_{\Gamma_{i}}\vec{F}d \vec{x}
$$
### teorema:
Si $\Gamma$ es una cuerva suave seccionalmente y $\vec{F}$ un campo vectorial definido y continuo sobre $\text{tr}(\Gamma)$, entonces se cumple que:
$$
\int_{-\Gamma}\vec{F} d \vec{x} = -\int_{\Gamma}\vec{F} d \vec{x}
$$
* esto es similar a que $\int_{a}^{b}fdx=-\int_{b}^{a}fdx$

*obs:* se puede ser menos riguroso en la notación de las integrales de línea,
	por ejemplo, si $n=2$, usualmente se escribe:
	$\int_{\Gamma}P\ dx+a\ dy$, o bien $\int_{\Gamma}P(x,y)dx+a(x,y)dy$ para referise a la integral de línea: $\int_{\Gamma}\vec{F} d \vec{x}$, con $\vec{F}=(P,Q)$
	ya que: $\int_{\Gamma}\vec{F} d \vec{x}= \int_{P}(P,Q)\cdot(dx,dy)=\int_{P}Pdx+Qdy$

### teorema: Linealidad de integral de línea
Si $\Gamma$ es una curva seccionalmente suave, y $\vec{F}$ y $\vec{G}$ son campos vectoriales continuos sobre $\text{tr}(\Gamma)$. Si $a,b$ son constantes, entonces:
$$
\int_{\Gamma}(a\vec{F}+b\vec{G})d\vec{x} = a\int_{\Gamma}\vec{F}d\vec{x}+b\int_{\Gamma}\vec{G}d\vec{x}
$$

### Caso para curvas cerradas
Dada $\vec{\alpha}:[a,b] \to \mathbb{R}^{n}$ una parametrización de $\Gamma$, la cual es una curva cerrada. Sean $a<c<b$, y $\vec{\beta}:[c,c+b-a]\to \mathbb{R}^{n}$ definida por:

$$
\vec{B}(t) = 
\left\{
	\begin{array}{ll}
		\vec{\alpha}(t) &  , \text{si } c\leq t<b \\
		\vec{\alpha}(t-b+a)  & , \text{si } b\leq t\leq c+b-a
	\end{array}
\right.
$$
así $x_{1}=\vec{\beta}(c)=\vec{\alpha}(c)$ es el punto inicial y final de $\Gamma$,
*** ejercicio, ver que $\text{tr}(\Gamma)=\text{tr}(\Gamma_{1})$

Si $\vec{F}$ es un campo vectoral continuamente definido en $\text{tr}(\Gamma)$ y $\Gamma$ es suave seccionalmente, entonces:
$$
\begin{align}
\int_{\Gamma_{1}}\vec{F}d\vec{x} = & \int_{c}^{c+b-a}\vec{F}(\vec{\beta}(t))\vec{\beta}'(t)dt \\
=\int_{c}^{b} \vec{F}(\vec{\alpha}(t)) \vec{\alpha}'(t)dt= & \int_{b}^{c+b-a} \vec{F}(\vec{\alpha}(t-b+a))\vec{\alpha}'(t-b+a)dx
\end{align}
$$
y, haciendo el cambio de variable $\tau=t$ en la primera integral y $\tau=t-b+a$ en la segunda:
$$
\vdots
$$
por lo tanto ***para curvas cerradas, no importa el punto final e inicial que se elija, así, no es necesario especificar estos puntos.***

* *observación 1*: La integral de línea sobre una curva cerrada se suele denotar por:
$$
\oint_{\Gamma}=\vec{F} d\vec{x}
$$
* *observación 2*: la que sí hace cambiar el valor de la integral a lo largo de una curva cerrada $\Gamma$, es cuando se cambia el **número de veces que se recorre la curva y cuando se cambia el sentido de recorrido.**

## Integrales de línea independientes del camino (o curva)
### Campos Vectoriales Conservativos
Si se considera el ejemplo: dos curvas que unen los puntos $(0,0)$ con $(1,1)$ de la forma:
$\Gamma_{1}$: La parte de la parábola $y=x^{2}$
$\Gamma_{2}$: El segmento de recta
![[Pasted image 20250814112231.png]]
considerando el campo vectorial $\vec{F}(x,y)=(x+y^{2},x^{2})$ y calcular: $\int_{\Gamma_{1}}\vec{F}d\vec{x}$ y $\int_{\Gamma_{2}}\vec{F}d\vec{x}$
si se tienen las parametrizaciones
$$
\vdots
$$

*def:* 
Si $\vec{F}$ es un campo vectorial continua en un abierto $\Omega \subseteq \mathbb{R}^{n}$ y $\int_{\Gamma_{1}}\vec{F}d\vec{x}=\int_{\Gamma_{2}}\vec{F}d\vec{x}$ para todo par de curvas $\Gamma_{1},\Gamma_{2}\subseteq \Omega$ con el mismo punto inicial y final, 
entonces se dice que:
Las integrales de línea son independientes del camino en $\Omega$

*obs:* Hay casos en que los anterior se denota por:
$$
\int_{x_{0}}^{x_{1}} \vec{F} d\vec{x}
$$
para cualquier curva seccionalmente desde $x_{0}$ a $x_{1}$

### teorema
Supongamos que $\vec{F}$ es un campo vectorial continuo en un conjunto abierto $\Omega$. Entonces,
Las integrales de líneas son independientes del camino si se cumple que:
$$
\oint_{\Gamma}\vec{F}d\vec{x}=0
$$
para toda curva cerrada $\Gamma \subseteq \Omega$

# clase 14/08
## Campo Escalar Conservativo

*def:* **Campo Vectorial Conservativo**
Dado $\vec{F}:\Omega \subseteq \mathbb{R}^{n}\to \mathbb{R}^{n}$ se dice conservativo si existe un campo escalar diferenciable $f:\Omega \subseteq \mathbb{R}^{n}\to \mathbb{R}$ tal que:
$$
\forall x \in \Omega,\;\vec{F}(x)=\nabla f(x)
$$
en este caso, a $f$ se le llama **potencial** de $\vec{F}$

## Conjunto Conexo

*def:* **Conjunto Conexo**
Dado conjunto $\Omega \subseteq \mathbb{R}^{n}$ abierto,
$\Omega$ es conexo si todos los puntos de $\Omega$ pueden unirse mediante una curva seccionalmente suave en $\Omega$.
Gráficamente:
![[Pasted image 20250815192136.png]]

### teorema
Si se tiene un campo vectorial $\vec{F}$ continuo en $\Omega$ y $\Omega$ es un conjunto conexo, entonces:
Las integrales de línea son independientes del camino $\iff$ $\vec{F}$ es conservativo.

* *observación 1:* si $\vec{F}=\nabla F$ se cumple que cualquier curva seccionalmente suave, con punto inicial $x_{0}$ y final $x_{1}$:
  $$
  \int_{\Gamma}\vec{F}d\vec{x}=f(x_{1})-f(x_{0})
  $$
  O sea, se tiene un campo vectorial conservativo, no es necesario saber la parametrización, sino que sólo importa el valor del potencial en los extremos.
* *Observación 2:* Si se tiene un campo vectorial $\vec{F}:\Omega \subseteq \mathbb{R}^{n}\to \mathbb{R}^{n}$ que es continuo y $\Omega$ es conexo, entonces son equivalentes:
  1. Las integrales de línea son independientes del camino.
  2. $\oint_{\Gamma}\vec{F}d\vec{x}=0$ con $\Gamma$ seccionalmente suave.
  3. $\vec{F}$ es conservativo.

### propiedades
Para un conjunto $\Omega \subseteq \mathbb{R}^{n}$ abierto y un campo vectorial $\vec{F}:\Omega \subseteq \mathbb{R}^{n}\to \mathbb{R}^{n}$ de clase $\mathcal{C}^{1}$, si $\vec{F}$ es conservativo, entonces:
Su matriz derivada $\vec{F}_{n\times n}'$ es simétrica, es decir:
$$
\forall x \in \Omega,\forall i,j \in \{ 1,\dots,n \}:\frac{\partial}{\partial x_{j}}F_{i}(x)=\frac{\partial}{\partial x_{i}}F_{j}(x)
$$
* *observación:* Si $n=3,\; \vec{F}(x,y,z)=(P(x,y,z),Q(x,y,z),R(x,y,z))$, el resultado anterior se reduce a:
  $$
  \frac{\partial}{\partial y}P=\frac{\partial}{\partial x}Q,\;\frac{\partial}{\partial z}Q=\frac{\partial}{\partial y}R,\;\frac{\partial}{\partial x}R=\frac{\partial}{\partial z}P
  $$
para este caso existe una forma equivalente al teorema anterior, en términos del rotacional de $\vec{F}$

## Rotacional o Rotor
*def:* **Rotacional de un campo vectorial**
Dado un campo vectorial $\vec{F}=(P,Q,R)$ definido en un conjunto abierto conexo $\Omega \subseteq \mathbb{R}^{3}$, se define el *rotacional o rotor* de $\vec{F}$, denotado como $\text{rot}(\vec{F})$, como un campo vectorial $\text{rot}(\vec{F}):\Omega \subseteq \mathbb{R}^{3}\to \mathbb{R}^{3}$, de la forma:
$$
\text{rot}(\vec{F})=\left( \frac{\partial}{\partial y}R-\frac{\partial}{\partial z}Q,\;\frac{\partial}{\partial z}P-\frac{\partial}{\partial x}R,\;\frac{\partial}{\partial x}Q-\frac{\partial}{\partial y}P \right)
$$
es más fácil de recordar si se escribe de la forma:
$$
\text{rot}(\vec{F})=\det
\left( \begin{matrix}
\hat{\imath} & \hat{\jmath} & \hat{k} \\
\frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\
P & Q & R
\end{matrix} \right)
=\nabla \vec{\times}F
$$
Luego, el teorema anterior se reduce a:
$$
\begin{align}
\text{rot}(\vec{F})=\text{rot}(\nabla F)=(0,0,0) \\
\text{rot}(\nabla F)=\vec{0}
\end{align}
$$
	Ejemplo: Si se considera $\vec{F}:\mathbb{R}^{2}\setminus \{(0,0)\}\to \mathbb{R}^{2}$
	$$
	\vec{F}(x,y)=\left( -\frac{y}{x^{2}+y^{2}},\frac{x}{x^{2}+y^{2}} \right)
	$$
	es de clase $\mathcal{C}^{1}$ y $\vec{F}'$ es simpetrica.
	$\vdots$

La condición para $\vec{F}'$ es suficiente en cierta clase de dominio que incluyen, por ejemplo: $\{ (x,y)|x\geq 0 \}$ pero no a $\mathbb{R}^{2}\setminus \{ (0,0) \}$

## Conjunto Estrellado
*def:* **Conjunto Estrellado**
Dado un conjunto $\Omega \subseteq \mathbb{R}^{n}$ se dice estrellado si $\exists x_{0}\in \Omega, \forall x \in \Omega$, el segmento:
$$
\left[ x_{0},x \right] : \{ x_{0}+t(x-x_{0}) |t\in \left[ 0,1 \right]  \}
$$

* *observación:* Intuitivamente, un dominio estrellado no tiene 'agujeros'. Graficamente:
  ![[Pasted image 20250815201217.png]]

### teorema: Lema de Poincaré
Dado un conjunto $\Omega \subseteq \mathbb{R}^{n}$ abierto y estrellado y sea un campo vectorial $\vec{F}:\Omega\to \mathbb{R}^{n}$ de clase $\mathcal{C}^{1}$ tal que $\forall x \in \Omega,\vec{F'(x)}$ es simétrico, entonces $\vec{F}$ es conservativo.

Otra forma de definir conjuntos sin agujeros en $\mathbb{R}^{2}$ es considerar que el conjunto $\Omega$ es **simplemente conexo**. Para ello, se considera una curva de joran $\Gamma \in \mathbb{R}^{2}$ divide a $\mathbb{R}^{2}\setminus \Gamma$ en dos dominios con frontera común $\Gamma$, la región interior a $\Gamma$ y la región exterior a $\Gamma$. Gráficamente:
![[Pasted image 20250815201806.png]]

## Simplemente Conexo
*def:* **Simplemente Conexo**
Un conjunto $\Omega \subseteq \mathbb{R}^{2}$ abierto y conexo, se llama *simplemente conexo* si,
para cada curva de jordan $\Gamma \in \Omega$, la región interior a $\Gamma$ también está contenida en el conjunto $\Omega$. Gráficamente:
![[Pasted image 20250815201955.png]]

### teorema
Dado un conjunto $\Omega \subseteq \mathbb{R}^{n}$ simplemente conexo y $\vec{F}:\Omega\to \mathbb{R}^{n}$ es de clase $\mathcal{C}^{1}$ tal que:
$$
\forall x \in \Omega,\forall i,j \in \{ 1,\dots,n \}:\frac{\partial}{\partial x_{j}}F_{i}(x)=\frac{\partial}{\partial x_{i}}F_{j}(x)
$$
entonces $\vec{F}$ es conservativo.


# 
***
clase 19/08

Para calcular el potencial $f$ de un campo vectorial $\vec{F}$, si $\vec{F}=\nabla f$ en un $\Omega$ abierto y conexo, entonces:
$$
\begin{align}
 \vec{F}·d\vec{x}= & F_{1}dx_{1}+F_{2}dx_{2}+\dots+F_{n}dx_{n} \\
 =& \frac{\partial f}{\partial x_{1}}dx_{1}+\dots+\frac{\partial f}{\partial x_{n}}dx_{n} \\
= & df
\end{align}
$$
Luego, la integral de línea 
$$
\int \vec{F} d\vec{x}=\int_{\Gamma}df
$$
Una manera de encontrar el potencial $f$ es escogiendo un punto conveniente $x_{0}\in \Omega$ y evaluando, de la forma:
$$
f(x)=\int_{x_{0}}^{x}\vec{F}d\vec{x}
$$
para una curva $\Gamma$ que está en un conjunto $\Omega$, que une $x_{0}$ con $x$.
Si se considera un segmento de recta que una $x_{0}$ con $x$, (por $\Omega$ ser conexo) se puede parametrizar $\Gamma$ como:
$$
\vec{\gamma}(t)=tx+(1-t)x_{0},\ t\in[0,1]
$$
así
$$
f(x)=\int_{0}^{1}F\left( tx+(1-t)x_{0} \right) (x-x_{0})dt
$$
##### Ejemplo:
Sea $\vec{F}:\mathbb{R}^{2}\to \mathbb{R}^{2}$ definido como $\vec{F}(x,y)=(e^{x}+y,x+2y)=\left( P(x,y),Q(x,y) \right)$:
$\vec{F}$ es de clase $\mathcal{C}^{1}$ en $\mathbb{R}^{2}$ y además:
$$
\frac{\partial Q}{\partial x}=1=\frac{\partial P}{\partial y}
$$
por lo que $\vec{F}$ es conservativo, es decir, existe un potencial asociado $f:\mathbb{R}^{2}\to \mathbb{R}$ tal que:
$$
\nabla f=\vec{F}
$$
como $\mathbb{R}^{2}$ es conexo, tomamos el punto convecniente $x_{0}=(0,0)$, luego:
$$
\begin{align}
f(x,y)= & \int_{0}^{1}\vec{F(t(x,y)+(1-t)(0,0))\ ((x,y)-(0,0))} \\
  & \vdots \\
= & 
\end{align}
$$

# Teorema de Green
Se va a trabajar sólo en $\mathbb{R}^{2}$, osea, tomando sólo el caso $n=2$.
Sea $\Omega$ un conjunto abierto y $\vec{F}:\Omega\to \mathbb{R}^{2}$ de clase $\mathcal{C}^{1}$, definido por: $\vec{F}(x,y)=(P(x,y),Q(x,y))$, 
la simetría (o asimetría) de $\vec{F}$ está dado por la diferencia:
$$
\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}
$$
si $=0$ , entonces es simétrico.
Y se puede relacionar con el valor de la integral de línea $\oint_{\Gamma}\vec{F}d\vec{x}$ sobre una curva $\Gamma$ de jordan $\Gamma \subseteq \Omega$

## Teorema de Green: 1° Forma
Dados $P,Q:\Omega \subseteq \mathbb{R}^{2}\to \mathbb{R}$ campos escalares de clase $\mathcal{C}^{1}$ con $\Omega$ abierto. 
Sea $\Gamma$ una curva de jordan seccionalmente suave, se representa por $\mathcal{R}$ a la unión de $\Gamma$ con su región interior.
Si $\mathcal{R}\subseteq \Omega$, entonces:
$$
\int \int_{\mathcal{R}} \left( \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y} \right)dxdy =\oint_{\Gamma}Pdx+Qdy
$$
con $\Gamma$ en sentido antihorario.
##### ejemplo:
Calcular $\oint_{\Gamma}y^{2}dx+xdy$, donde $\Gamma$ es el cuadrado de vértices $(0,0),(2,0),(2,2),(0,2)$, si:
$P(x,y)=y²,Q(x,y)=x$

$$
\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}=1-2y\neq 0 \implies \text{asimetrica}
$$
calculando:
$$
\oint_{\Gamma}y^{2}dx+xdy=\int_{0}^{2}\int_{0}^{2}(1-2y)dxdy
$$
### Corolario
Si $\Gamma$ es una curva de Jordan seccionalmente suave en $\mathbb{R}^{2}$ y $\mathcal{R}$ es la región interior a $\Gamma$ junto con la misma curva $\Gamma$, entonces:
$$
A(\mathcal{R})=\oint_{\Gamma}xdy=-\oint_{\Gamma}ydx=\frac{1}{2}\oint-ydx+xdy
$$

## Teorema de Green: 2° Forma

Dadas $\Gamma_{1},\Gamma_{2},\dots,\Gamma_{k}\subseteq \mathbb{R}^{2}$, k-curvas de Jordan seccionalmente suaves que cumplen:
1. Dos cualesquiera de las k-curvas no se intersectan
2. $\Gamma_{2},\dots,\Gamma_{k}$ están en la región interior de $\Gamma_{1}$
3. para cada $i>1,j>1,i\neq j$, la curva $\Gamma_{i}$ está en la región exterior de $\Gamma_{j}$

Se le designa con $\mathcal{R}$ a la región que está en la unión de $\Gamma_{1}$ con su propio interior que NO está en el interior de las otras curvas.

Dadas $P,Q\subseteq \mathbb{R}^{2}\to \mathbb{R}$ de clase $\mathcal{C}^{1}$ en un conjunto abierto $\Omega \supset \mathcal{R}$, entonces:
$$
\int \int_{\mathcal{R}} \left( \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y} \right)dxdy =\oint_{\Gamma}Pdx+Qdy -\sum_{i=2}^{k}\oint_{\Gamma_{i}}Pdx+Qdy
$$
con $\Gamma_{i}, i \in \{ 1,\dots,k \}$ en sentido antihorario.

> Si no se tomaran los 'agujeros' al interior de las otras curvas se tendría la 1° forma de Green, así que en este caso se le restan los agujeros.


***
# 
Clase 21/08
### Corolario
Sea $\Omega \subseteq \mathbb{R}^{2}$ un abierto [[#Simplemente Conexo]], y $\vec{F}=(P,Q)$ de clase $\mathcal{C}^{1}$ tal que:
$$
\frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y}=0 \text{ en } \Omega
$$
entonces $\vec{F}$ es conservativo:

## Teorema: Invarianza de una integral de línea al deformar un camino
Sea $\Omega \subseteq \mathbb{R}^{2}$ abierto y conexo; $P,Q:\Omega\to \mathbb{R}$ de clase $\mathcal{C}^{1}$, y supongamos que $\frac{\partial Q}{\partial x}=\frac{\partial P}{\partial y}$ en todo $\Omega$.
Sean $\Gamma_{1},\Gamma_{2}$ dos curvas de Jordan seccionalmente suaves en $\Omega$ que cumplen que:
1. $\Gamma_{2}$ está en la región interior de $\Gamma_{1}$,
2. Los puntos de la región de $\Gamma_{1}$ que están en la región exterior de $\Gamma_{2}$ pertenecen a $\Omega$
entonces:
$$
\oint_{\Gamma_{1}}Pdx+Qdy=\oint_{\Gamma_{2}}Pdx+Qdy
$$
recorriendo las curvas en el mismo sentido.

fin de curvas
***
# Integrales sobre superficies

def básica de superficie:
## Superficie
Una superficie es el lugar geométrico de un punto que se mueve en $\mathbb{R}^{3}$ con dos [[Grado de Libertad|grados de libertad]].

Hay tres métodos para representar una superficie:
1. Representación Implícita
2. Representación Explícita

### Representación Implícita
$$
S=\{ (x,y,z)\in \mathbb{R}^{3}:F(x,y,z)=0 \}
$$
se puede decir que se tienen tres grados de libertad, pero el proceso es 'despejar' una variable en función de la otra, pero en estos casos no es sencillo.

##### ejemplo
sea 
$$
S=\{ (x,y,z)\in \mathbb{R}^{3}:x^{2}+y^{2}+z^{2}-4=0 \}
$$
 es una esfera de radio 2


### Representación Explícita
Cuando se puede despejar en la ecuación una de las coordenadas..

##### ejemplo
del ejemplo anterior, si se tiene:
$$
S=\{ (x,y,z)\in \mathbb{R}^{3}:x^{2}+y^{2}+z^{2}-4=0 \}
$$
se puede despejar $z$ como:
$$
z=\pm \sqrt{ 4-x^{2}-y^{2} }
$$
se tiene entonces el conjunto:
$$
S=\{ (x,y,z)\in \mathbb{R}^{3} :z=\pm \sqrt{ 4-x^{2}-y^{2} }\}
$$
y se tiene entonces que $z$ es una función que depende de dos variables: $z=f(x,y)$

### Representación Paramétrica
Cuando se puede parametrizar la superficie mediante una función $\vec{r}$.
De ahora en adelante se va a utilizar la representación paramétrica.

## Superficie Parámetrica
*def:* sea $T\subseteq \mathbb{R}^{2}$ un conjunto abierto y acotado, y sean $X,Y,Z: T\to \mathbb{R}$ funciones continuas. El conjunto 
$$
S=\{ (X(u,v),Y(u,v),Z(u,v)):(u,v)\in T \}\subseteq \mathbb{R}^{3}
$$
se llama superficie parámetrica; donde las ecuaciones $x=X(u,v),y=Y(u,v),z=Z(u,v) \in T$ son las ecuaciones parámetricas de la superficie $S$
> se llaman superficies parámetricas porque son las que parametrizan a la superficie


### Parametrización de la Superficie
Si introducimos el radio vector $\vec{r}$ que une el origen a un punto $(x,y,z)\in S$, se puede escribir:
$$
\vec{r}(u,v)= \left(  X(u,v),Y(u,v),Z(u,v) \right), (u,v)\in T
$$
es la parametrización de la superficie.

*obs:* $S=\vec{r}(T)$
***grafico***

##### ejemplo
si una superficie viene dada explícitamente por:
$$
z=f(x,y),\ (x,y)\in T
$$
entonces
$$
\vec{r}(x,y)=(x,y,f(x,y)),\ (x,y)\in T
$$

## derivada de superficie 
En curvas se podía tener la 'velocidad' de la curva como $\Gamma'$. Viendo para superficies:
Consideremos la superficie parametrizada por
$$
\vec{r}(u,v)=\left( X(u,v),Y(u,v),Z(u,v) \right)
$$
si $X,Y,Z$ son variables en $T$, se puede considerar:
$$
\frac{\partial \vec{r}}{\partial u}=\left( \frac{\partial X}{\partial u},\frac{\partial Y}{\partial u},\frac{\partial Z}{\partial u} \right) =\vec{t}_{u}
$$

$$
\frac{\partial \vec{r}}{\partial v}=\left( \frac{\partial X}{\partial u},\frac{\partial Y}{\partial v},\frac{\partial Z}{\partial v} \right) =\vec{t}_{v}
$$



> los vectores $\vec{t}$ son los vectores tangentes a la superficie.

### Producto Vectorial Fundamental
El producto vectorial
$$
\frac{\partial \vec{r}}{\partial u}\times \frac{\partial \vec{r}}{\partial v}
$$
que es una función que depende de $(u,v)$, se denomina producto vectorial fundamental de $\vec{r}$

### Puntos regulares y singulares
*obs:* Si $(\bar{u},\bar{v})\in T$ es tal que
$$
\frac{\partial \vec{r}}{\partial u},\frac{\partial \vec{r}}{\partial v}
$$
 son continuas, y el producto vectorial es no nulo, entonces:
 $$
\vec{r}(u,v)
$$
se llama **punto regular** de $\vec{r}$.
Y los puntos no regulares se llaman puntos singulares.

### Superficie regular

Una superficie $S=\vec{r}(T)$ se llama regular si todos sus puntos son **regulares**.

> es análogo a las curvas suaves

*obs:* en cada punto regular, los vectores:
$$
\frac{\partial \vec{r}}{\partial u},\frac{\partial \vec{r}}{\partial v}
$$
determinan un plano que tiene vector $\frac{\partial \vec{r}}{\partial u}\times \frac{\partial \vec{r}}{\partial v}$ como normal.

### Plano Tangente
El plano determinado por los vectores $\frac{\partial \vec{r}}{\partial u},\frac{\partial \vec{r}}{\partial v}$ se llama **plano tangente** a la superficie.

### Superficie Suave
Una superficie será suave si admite una parametrización $\vec{r}$ de clase $\mathcal{C}^{1}$ 

# Campos de Normales
Una esfera tiene infinitos vectores normales, por ello, se habla de campos.

Si $S\subseteq \mathbb{R}cb$ una superficie regular y sea $\vec{r}:T\subseteq \mathbb{R}^{2}\to \mathbb{R}^{3}$ una parametrización de $S$,
entonces se define el campo de normales sobre $S$ como:
$$
\hat{n}=\frac{\vec{t}_{u}\times \vec{t}_{v}}{||\vec{t}_{u}\times \vec{t}_{v}||}
$$

# Superficie Regular Orientable
Una superficie regular $S$ está orientada según $\hat{n}:S\to \mathbb{R}^{3}$ cuando la normal está bien definida globalmente como una función continua sobre $S$.
> gráfico


# Área de Superficie
El área de una superficie regular se define como:
$$
A(S)=\iint_{\Gamma}\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u}\times \frac{\partial \vec{r}(u,v)}{\partial v}  \right|   \right|\ du\ dv
$$
esta definición es independiente de la parametrización.

*obs:* si $S$ está definida explíciatemente por $z=f(x,y),\ (x,y)\in T$, se tiene que:
$$
\vec{r}(x,y)=(x,y,f(x,y)),\ (x,y)\in T
$$
y con esto:
$$
\frac{\partial \vec{r}(u,v)}{\partial u}\times \frac{\partial \vec{r}(u,v)}{\partial v}=\left( -\frac{\partial f}{\partial x},-\frac{\partial f}{\partial y},1 \right)
$$
y así
$$
A(S)=\iint_{T}\sqrt{ 1+\partial f() }
$$
>se parece al área de un sólido de revolución 

***
*def*
Si $S_{1},\dots,s_{k}$ son superficies suaves que satisfacen:
1. Cada uno de los bordes $\partial S_{1},\dots,\partial S_{k}$ intersectan al menos uno de los otros bordes en una curva seccionalmente suave.
2. Ningún par de puntos entre las superficies $S_{1},\dots,S_{k}$ tiene puntos en común que no son bordes.
entonces se dice que:
$S_{1},\dots,S_{k}$ forman una superficie seccionalmente suave $S$ y se escribe:
$$
S=S_{1},S_{2}+\dots+S_{K}
$$
y además:
$$
A(S)=A(S_{1})+A(S_{2})+\dots+A(S_{k)})
$$

# 
*def*
Sea $S$ una superficie suave representada (parametrizada) por $\vec{r}:T\to \mathbb{R}^{3}$, y supongamos que $f$ es una función real y continua en $S$. Entonces la integral de superficie de $f$ sobre $S$ se representa por el símbolo:
$$
\iint_{S}f(x)dA=\iint_{S}f(x,y,z)dS
$$
y está definida por
$$
\iint_{S}f(x)dA=\iint_{T}f(\vec{r}(u,v))\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}\right|  \right| du\ dv
$$
*obs:* 
1. si $S_{1}+\dots+S_{k}$,
   $$
\iint_{S}f(x)dA=\iint_{S_{1}}f(x)dA+\dots+\iint_{S_{k}}f(x)dA
$$
2. Si $f=1$, entonces:
   $$
\iint_{S}f(x)dA=\iint_{S}1·dA=A(S)
$$

# 
*def*
Sea $\vec{F}=(P,Q,R)$ un campo vectorial continuo sobre la superficie suave y orientable $S$, supongamos que $\hat{n}$ es una orientación de $S$. 
Entonces la integral de superficie de $\vec{F}$ sobre $S$ está definida como la integral de superficie del campo escalar $\vec{F}·\hat{n}$, es decir:
$$
\iint_{S}\vec{F}·\hat{n}dA
$$

*obs:* si $\hat{n}$ es inducido por la superficie $S$ mediante $\vec{r}(u,v)$ se tiene:
$$
\hat{n}=\frac{\frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}}{\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}\right|  \right|}
$$
por lo tanto:
$$
\iint_{S}\vec{F}·\hat{n}dA=\iint_{T}\vec{F}(\vec{r}(u,v))•\hat{n}(\vec{r}(u,v))·\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}\right|  \right|dudv
$$
$$
=\iint_{T}\vec{F}(\vec{r}(u,v))·\frac{\frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}}{\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}\right|  \right|}·\left| \left| \frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v}\right|  \right|dudv
$$
$$
\iint_{T}\vec{F}(\vec{r}(u,v))·\left(\frac{\partial \vec{r}(u,v)}{\partial u} \times \frac{\partial \vec{r}(u,v)}{\partial v} \right)du\ dv
$$

Físicamente si F es una velocidad de un fluido, entonces la expresión es el volumen que se mueve.

# 
*def*
Sea $S=S_{1}+\dots+S_{k}$ una superficie seccionalmente suave con orientaciones $\hat{n}_{1},\hat{n}_{2},\dots,\hat{n}_{k}$ (osea se divide en superficies chicas y cada una tiene su orientación).
Si $\vec{F}:S\to \mathbb{R}^{3}$ continuo, se tiene que:
$$
\iint_{S}\vec{F}\hat{n}dA=\sum_{i=1}^{k} \iint_{S_{i}}\vec{F}\hat{n}_{i}dA
$$

# Teorema de la Divergencia

*def:*
La divergencia de un campo vectorial $\vec{F}:\Omega \subseteq \mathbb{R}^{n}\to\mathbb{R}^{n}$ está definido por lo siguiente:
$$
\text{div}(\vec{F})=\sum_{i=1}^{n}\frac{\partial F_{i}(x)}{\partial x_{i}}=\text{tr}(\vec{F}'(x))
$$
 > cada componente se deriva por su variable

## Terorema de la Divergencia
Sea $\Omega$ una región acotada en $\mathbb{R}^{3}$ cuya frontera se parametriza como una superficie $S$ seccionalmente suave, orientable y cerrada (osea no puede ser, por ej. un plano).
Supongamos que $\vec{F}$ es de clase $\mathcal{C}^{1}$ y $\hat{n}$ es la orientación de $S$ que apunta hacia el exterior. 
Entonces:
$$
\iint_{S}\vec{F}·\hat{n}\ dA=\iiint_{\Omega}\text{div}(\vec{F})\ dx\ dy\ dz
$$
*obs:* el teorema de la divergencia es la generalización del teorema de green para 3 dimensiones.


***
Estudiando operaciones diferenciales, escribamos:
$$
\nabla=\left( \frac{\partial}{\partial x_{1}},\dots, \frac{\partial}{\partial x_{n}} \right) =\sum_{i=1}^n e_{i} \frac{\partial}{\partial x_{i}}
$$
el teérmino dentro de la sumatoria se llama notación de einstein

Con esta notación, operamos $\nabla$ de la misma forma como lo haríamos con un vector.
De este modo, para $f:\Omega \subseteq \mathbb{R}^{n}\to \mathbb{R}$, se hace:
$$
\nabla f=\sum_{i=1}^n e_{i} \frac{\partial f}{\partial x_{i}}
$$
y para $\vec{F}:\Omega \subseteq \mathbb{R}^n \to \mathbb{R}^n$, se tiene:
$$
\text{div}(\vec{F})=(\nabla \vec{F})=\dots
$$

un operador importante es el **laplaciano**, y lo podemos escribir con esa notación:
$$
\begin{align}
\Delta f & =\nabla^{2}f=\nabla·\nabla f \\
 & =\sum_{i=1}^n \frac{\partial^{2}f}{\partial x_{i}^{2}} \\
 & =\text{tr}(f''(x))
\end{align}
$$

para el caso del **rotacional**, recuperamos la notación anterior:
$$
\text{rot}(\vec{F})=\nabla \times \vec{F}
$$
que mide la asímetría de la matriz $\vec{F}'(x,y,z)$

Podemos extender lo anterior al caso de tensores:
Notemos que
$$
e_{i}·e_{j}=\delta_{ij}=
\left\{
	\begin{array}{ll}
		1\; , \text{si } i=j \\
		0\; , \text{si } i\neq j
	\end{array}
\right.
$$
donde $\delta_{ij}$ se llama delta de Kronecker

Analicemos el producto cruz. Para ello,
sea $a\times b=c$,
donde 
$$
\begin{align}
a=e_{i}·a_{i} \\
b=e_{i}·b_{i} \\
c=e_{i}·c_{i}
\end{align}
$$
entonces, usando la notación de einstein:
$$
C_{k}=(a\times b)_{k}=\epsilon_{ijk}a_{i}b_{i}
$$
donde
$$
\epsilon_{ijk}=
\left\{
	\begin{array}{ll}
		1\; , \text{ordenamientos par }i\to j\to k \\
		-1\; , \text{ordenamientos impar }i\to k\to j \\
        0\;, \text{dos o mas terminos repetidos}
	\end{array}
\right.
$$

*obs:*
1) $\epsilon_{ijk}=-\epsilon_{ijk}$
2) $\epsilon_{ijk}\epsilon_{\alpha \beta k}=\delta_{i\alpha}\delta_{i\beta}-\delta_{i\beta}\delta j\alpha$

## teorema: Fórmulas de Green o I.P.P.
Sea $\Omega \subseteq \mathbb{R}^{3}$ abierto, acotado con frontera $\partial \Omega$ de clase $\mathcal{C}¹$. 
Entonces, si $u,v \in C²(\Omega)$:
$$
\frac{\partial u}{\partial n}=\nabla u·\hat{n}
$$
donde $\hat{n}$ es la normal unitaria exterior, se tiene:
1
$$
\iiint_{\Omega}u\Delta v=\iint_{\partial \Omega}u \frac{\partial v}{\partial n}dA-\iiint_{\Omega}\nabla u·\nabla v
$$
2.
$$
\iiint_{\Omega}(u\Delta v-v\Delta u)=\iint_{\partial \Omega}\left( u \frac{\partial v}{\partial n}-v \frac{\partial u}{\partial n} \right) dA
$$

## Teorema de Stokes (Forma Restringida)
Supongamos que S es una superficie orientable suave, definida por $\vec{r}:T\subseteq \mathbb{R}^{2}\to \mathbb{R}^{3}$, donde T es convexo y cerrado, acotado por una curva de jordan $\Gamma$.
Supongamos también que $\vec{r}$ es de clase $C 2$ en T y que $\vec{F}=(P,Q,R)$ es de clase $C 1$ en S.
Sea $\hat{n}$ la orientación de S inducida por $\vec{r}$, y que $\vec{r}(u,v)$ recorre el borde de S, denotado por $\partial S$ exactamente una vez cuando $(u,v)$ recorre $\Gamma$. Entonces:
$$
\iint_{S}\text{rot}(\vec{F})\hat{n}dA=\oint_{\partial S}\vec{F}d\vec{x}
$$
donde el sentido recorrido de $\partial S$ es aquel en el cual $\vec{r}(u,v)$ la recorre cuando $(u,v)$ recorre a $\Gamma$ en el sentido antihorario.
*obs:* si $S\subseteq \mathbb{R}^{2}$ acotado por una curva de Jordan $\partial S$, considerando $\vec{r}(x,y)=(x,y,0),\ (x,y)\in S$  (es en el plano $XY$). Entonces, la normal va a ser $\hat{n}=(0,0,1)$ y la fórmula se reduce para $\vec{F}=(P,Q,R)$
$$
\iint_{S}\left( \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y} \right) dxdy=\oint_{\partial S}Pdx+Qdy
$$

> Es un caso particular del teorema de green para un caso plano

## Teorema de Stokes
Sea $S$ una superficie seccionalmente suave, orientable y acotada, con borde consistente de curvas seccionalmente suaves $\Gamma_{1},\dots,\Gamma_{K}$, cada una de ellas positivamente dirigidas con respecto a $\hat{n}$. Sea $\vec{F}$ de clase $C 1$, entones:
$$
\iint_{S}\text{rot}(\vec{F})\hat{n}dA=\sum_{i=1}^K \int_{\Gamma_{i}} \vec{F}d\vec{x} 
$$

***
# Clase 02/09

## Operadores diferenciales en otros sistemas de coordenadas
Las coordenadas cartesianas no siempre son las más adecuadas (o correctas) para describir objetos geométricos y campos escalares o vectoriales.

Un sistema de coordenadas es una transformación invertible "suficientemente" diferenciable $\vec{r}:\Omega \subseteq \mathbb{R}^{3}\to \mathbb{R}^{3}$ donde
$$
\vec{r}(u,v,w)=x(u,v,w)\hat{i}+y(u,v,w)\hat{j}+z(u,v,w)\hat{k}
$$
donde supondremos que $\vec{r}'(u,v,w)$ es no singular, es decir, invertible para cada $(u_{0},v_{0},w_{0})$ en $\Omega$

En cada punto se define un triedro (una 3-tupla) de vectores unitarios de la siguiente manera:
Fijamos $(u_{0},v_{0},w_{0})\in \Omega$ y consideramos:
$$
u \to \vec{r}(u,v_{0},w_{0})
$$
> Me paro en un punto y varío sólo una de las coordenadas (en este caso $u$)

como $\vec{r}'$ es invertible, se tiene:
$$
\left| \left| \frac{\partial}{\partial u}\vec{r}(u_{0},v_{0},w_{0}) \right|\neq 0  \right| 
$$
y por tanto, el vector tangente a la curva $\vec{r}(u,v_{0},w_{0})$ en $\vec{r}(u_{0},v_{0},w_{0})$ está bien definido y se expresa como:
$$
\hat{u}=\frac{\frac{\partial}{\partial u}\vec{r}(u_{0},v_{0},w_{0})}{\left| \left| \frac{\partial}{\partial u}\vec{r}(u_{0},v_{0},w_{0}) \right|  \right| }
$$
y se puede hacer el mismo proceso para $v,w$: de la misma manera, los vectores $\hat{v},\hat{w}$ definidos $v\to \vec{r}(u_{0},v,w_{0})$ y $w\to \vec{r}(u_{0},v_{0},w)$ están bien definidos.

> mono1

como $\vec{r}'$ es invertible en todo punto, $\{ \hat{u},\hat{v},\hat{w} \}$ es linealmente independiente, por lo que es una base ortonormal de $\mathbb{R}^{3}$

## Sistema Ortogonal
*def:*
Se dice que el sistema de coordenadas $\vec{r}=\vec{r}(u,v,w)$ con $(u,v,w)\in \Omega$ es ortogonal si los vectores $\{ \hat{u},\hat{v},\hat{w} \}$ definidos por:
$$
\hat{u}=\frac{\frac{\partial \vec{r}}{\partial u}}{\left| \left| \frac{\partial \vec{r}}{\partial u} \right|  \right| }
$$
$$
\hat{v}=\frac{\frac{\partial \vec{r}}{\partial v}}{\left| \left| \frac{\partial \vec{r}}{\partial v} \right|  \right| }
$$
$$
\hat{w}=\frac{\frac{\partial \vec{r}}{\partial w}}{\left| \left| \frac{\partial \vec{r}}{\partial w} \right|  \right| }
$$

son mutuamente ortogonales, pero cada $(u,v,w)\in \Omega$, donde:
$$
h_{u}=\left| \left| \frac{\partial \vec{r}}{\partial u} \right|  \right| 
$$
$$
h_{v}=\left| \left| \frac{\partial \vec{r}}{\partial v} \right|  \right| 
$$
$$
h_{w}=\left| \left| \frac{\partial \vec{r}}{\partial w} \right|  \right| 
$$
y se llaman factores escalares.

> Se está haciendo un cambio de base, equivalente a cambiar la forma de expresar el mismo vector 'con otro idioma'
##### Ejemplo de Coordenadas Polares.
>monos


## Operadores Diferenciales
Primero estudiando el gradiente en 2D.
Para ello, consideremos:
$$
\begin{align}
\vec{r}=x \hat{i}+y\hat{j} \\
\nabla f=\frac{\partial f}{\partial x}\hat{i}+\frac{\partial f}{\partial y}\hat{j}
\end{align}
$$
está en base $\{ \hat{i},\hat{j} \}$
Sabemos que 
$$
\frac{\partial f}{\partial x}=\nabla f·\hat{\imath}\ ,\ \frac{\partial f}{\partial y}=\nabla f·\hat{\jmath}
$$
con esto:
$$
\nabla f=(\nabla f·\hat{\imath})\hat{\imath}+(\nabla f·\hat{\jmath}\hat{\jmath})\hat{\jmath}
$$
que pasa si generalizamos a la base ortonomal $\{ \hat{u},\hat{v} \}$

Escribiendo:
$$
\nabla f=(\nabla f·\hat{u})\hat{u}+(\nabla f·\hat{v})\hat{v}
$$
y considerando
$$
\hat{u}=\frac{1}{h_{u}}\frac{\partial \vec{r}}{\partial u}\ ,\ v=\frac{1}{h_{v}}\frac{\partial \vec{r}}{\partial v}
$$
podemos escribir:
$$
\nabla f·\hat{u}=\frac{1}{h_{u}}\left[ \frac{\partial f}{\partial x}\hat{i}+\frac{\partial f}{\partial y}\hat{j} \right] \left[ \frac{\partial f}{\partial u}\hat{i}+\frac{\partial f}{\partial u}\hat{j} \right] 
$$
$$
= \frac{1}{h_{u}}\left[ \frac{\partial f}{\partial x}\frac{\partial x}{\partial u}+\frac{\partial f}{\partial y}\frac{\partial y}{\partial u} \right] 
$$
(por regla de la  cadena)
$$
=\frac{1}{h_{u}}\frac{\partial f}{\partial u}
$$

Análogamente 
$$
\nabla f·\hat{v}=\frac{1}{h_{v}}\frac{\partial f}{\partial v}
$$
por lo tanto
$$
\nabla f=\frac{1}{h_{u}}\frac{\partial f}{\partial u}
$$