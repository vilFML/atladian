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
es una pametrización de la curva $\Gamma$, de la forma:
$$
\Gamma=\Gamma_{1}\cup\Gamma_{2}
$$
y se denota como la suma de ambas:
$$
\Gamma=\Gamma_{1}+\Gamma_{2}
$$
	*obs:* una curva $\Gamma$ se dice seccionalmente suave si $\Gamma=\Gamma_{1}+\Gamma_{2}+\dots+\Gamma_{n}$, donde $\Gamma_{i}$ son suaves.
		osea una curva es seccionalmente suave si se puede escribir como unión de curvas suaves.