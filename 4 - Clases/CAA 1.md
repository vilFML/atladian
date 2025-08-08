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
***dIBUJO EJ DISCO GIRANDO***

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
  ***DIBUJO y=x²***

### [[Traza]]
*def:* 
diremos que un punto $x_{0}$ está sobre $\Gamma$ si existe 
$$
t_{0} \in [a,b]\text{ tq: }\vec{x_{0}}=\vec{\gamma}(t_{0})
$$ la colección de todos aquellos puntos se llama la **traza** de la curva $\Gamma$ y se denota $\text{tr}(\Gamma)$
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
	obs: $\vec{\gamma}'(a),\;\vec{\gamma}'(b)$ deben ser interpretadas como derivadas a la izquierda y derecha, respectivamente.
	***dibujo lim h->0***

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
***dibujo concatenación***
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
	*obs:* una curva $\Gamma$ se dice seccionalmente suave si $\Gamma=\Gamma_{1}+\Gamma_{2}+\dots+\Gamma_{n}$, donde $\Gamma_{i}$ son suaves.
		osea una curva es seccionalmente suave si se puede escribir como unión de curvas suaves.

***
# Clase 2, 07/08
#### Ejemplos curvas suaves
##### Ejemplo 1: Circunferencia
La circunferencia de centro (0,0) es una curva suave. En efecto, puede ser representada por:
$$
\begin{align}
\vec{\gamma}(t)=(\cos t,\sin t),\; 0\leq t\leq 2\pi \\
\text{donde }\vec{\gamma}'(t) = (-\sin t,\cos t), 0\leq t\leq 2\pi
\end{align}
$$
que es continua, y además $\vec{\gamma}'\neq(0,0),\; \forall t \in [0,2\pi]$

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
***dibujo semi circulos***
	se sacan las 'puntas' y se secciona en 2 curvas $\Gamma_{1},\Gamma_{2}$

# Recta tangente
Para una curva suave, en el punto $x_{0}=\vec{\gamma}(t_{0})$, se puede definir la recta tangente:
$$
x=x_{0}+s\;\vec{\gamma}(t_{0}),\;s \in \mathbb{R}^{n}
$$* es la recta tangente común que pasa por un punto.
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
***dibujo curva con particiones***
	cuando se agregan puntos, se acerca a la longitud de la curva completa.
Se dice que $\Gamma$ es **rectificable** si el conjunto $\{ L_{p}(\Gamma),P \text{ es una partición de }[a,b] \}$ es acotado superiormente.
*recuerdo:* si el conjunto es acotado superiormente, entonces tiene supremo. Y tiene ínfimo por norma ser no negativa.
Y en cuyo caso, la longitud de la curva (o del arco) se define como:
$$
L(\Gamma)=\text{sup}\{ L_{p}(\Gamma),\;P\text{ es una partición de }[a,b] \}
$$

para tener la longitud $L_{P}(\Gamma)$ sin calcular supremo:
si se multiplica $L_{p}(\Gamma)$ por un 1 conveniente $=\frac{||t_{i}-t_{i-1}||}{||t_{i}-t_{i-1}||}$, osea:
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
***dibujo curva con muchas lineas rectas***

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
$$ que corresponde a la **integral de línea**.


# 
Dada $\Gamma$ curva suave en $\mathbb{R}^n$ y $\vec{F}$ un campo vectorial continua y definido en $\text{tr}(\Gamma)$, entonces la integral de línea de $\vec{F}$ a lo largo de $\Gamma$ está definida como:
$$
\int_{\Gamma}\vec{F} d \vec{x} = \int_{a}^{b}\vec{F}(\vec{\gamma}(t))\vec{\gamma}(t)dt
$$
donde $\vec{\gamma}:[a,b]\to \mathbb{R}^{n}$ es una parametrización de $\Gamma$
	es similar al teorema de cambio de variable, porque se pasa de un dominio 'raro' $\Gamma$ a uno en $\mathbb{R}$, y el término de la derivada es análogo al Jacobiano del cambio de variable.
***Es integral de línea pues el dominio de integración ($\Gamma$ en este caso) es una curva.

## con campo escalar:
si $\mathcal{f}$ es un campo escalar, se define la integral de línea de $\mathcal{f}$ sobre $\Gamma$ como:
$$
\int_{\Gamma}\mathcal{f} d \vec{x} = \int_{a}^{b}\mathcal{f}(\vec{\gamma}(t))·||\vec{\gamma}(t)||dt
$$
	Ejemplo: si $\mathcal{f}$ es la densidad de masa de un alambre $\Gamma$, la integral representa la masa total de $\Gamma$

