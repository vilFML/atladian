Materia: Electromagnetismo
	Fecha cátedra: 05/08/25
	Fecha digitalización: 06/08/25
	*tags:* #Educación #Física/Electromagnetismo

El electromagnetismo estudia cómo interactúan los campos eléctricos y magnéticos con cargas eléctricas.

La materia esta compuesta por cargas, entonces estas interactúan con los campos eléctricos y magnéticos.

1. Existen dos tipos de carga: positivo y negativo
La carga de una partícula está **cuantizada**. Esto es, las magnitudes de las cargas de las partículas son múltiplos enteros de la carga del electrón.

La carga del electrón y del protón son opuestas pero aproximadamente iguales en módulo:
$$
|e| \approx|p|\approx 1,62·10^{-19}\; [C]
$$
Como notación se utiliza:
- $-e$, para electrón.
- $+e$, para protón.


2. Existen dos tipos de fuerzas: de atracción o de repulsión

3. Existen dos tipos de materiales: Conductores o aislantes.
	Para los materiales aislantes no es posible mover cargas eléctricas en su interior.

# Fuerza de Coulomb
El módulo de la carga de un electrón es:
$$
|e|=1,62·10^{-19}\;[C]
$$
Así, no es simple determinar cuántos electrones hay en 1 Coulomb, por lo que para obtener la medición experimental se realiza con el concepto de [[corriente eléctrica]].

Si se tienen 2 cargas puntuales positivas, existe una fuerza atractiva o repulsiva entre ellas según sus cargas, dada por:
$$
\vec{F}=\kappa \frac{ q_{1}q_{2}}{r^{2}} \hat{u}_{r}
$$
donde:
- $q_{i}$ es la carga de la i-ésima partícula,

- $r$ es la distancia entre las partículas

- $\kappa$ es la constante $=\frac{1}{4\pi \varepsilon_{0}}$ con $\varepsilon_{0}\approx 8,85·10^{-12}\;\left[ \frac{C^{2}}{Nm^{2}} \right]$ la constante dieléctrica del vacío. Esta se utiliza para contextualizar las cargas en el vacío, para evitar la interacción con otras partículas (Si se cambia de material, ésta se modifica).

- **Versor $\hat{u}_{r}$** es el vector que apunta en la dirección del campo eléctrico que provoca la presencia de la carga estática:
	  *convención*: para una carga eléctrica el vector es 'entrante' a la carga y para una positiva es 'saliente'.
	  ***DIBUJO***


Se realiza la 'creación' de una partícula aparte de las iniciales. Se asume que esta no afecta a las cargas iniciales y que es estática; pero ésta si es afectada por las demás. Así, se puede obtener la expresión de la fuerza que es ejercida por la presencia de las cargas iniciales:
***DIBUJO 3 cargas***
La fuerza total sobre la carga $q$, $F_{\text{tot}}$ es la suma vectorial de cada fuerza que ejercen las otras partículas:
$$
F_{\text{tot}}=F_{1}+F_{2}
$$
donde, además el versor $\hat{u}_{r}$ :
$$
\hat{u}_{r}=\frac{x-x_{0}}{r},\frac{y-y_{0}}{r},\frac{z-z_{0}}{r}
$$

Si se instala una partícula $q_{0}$ en un sistema con una partícula $q_{2}$ **negativa**, 
$$
\vec{F}_{i}=\frac{1}{4\pi\varepsilon_{0}}·-\frac{q_{0}·q_{2}}{r_{2}^{2}}\hat{u}_{r_{2}}
$$
de la partícula $q_{2}$ negativa, el versor $\hat{u}_{r_{2}}$ está entrando a la partícula, por lo que la fuerza $F_{i}$ invierte su sentido???????????????????????????????????? (ver dibujo)

se debe ver que la asignación del signo ya fue realizada y, en este caso, $q_{i}$ se refiere a las magnitudes de las cargas.

Luego, la fuerza total es
$$
\begin{align}
\vec{F}_{\text{tot}}=q_{0}\left( \frac{1}{4\pi\varepsilon_{0}}·\frac{q_{1}}{r_{1}^{2}}\hat{u_{r_{1}}} + \frac{1}{4\pi\varepsilon_{0}}·\frac{q_{2}}{r_{2}^{2}}\hat{u_{r_{2}}}+\dots \right) =\\
 \\
= q_{0}\sum_{i=1}^{N} \frac{1}{4\pi\varepsilon_{0}}·\frac{q_{i}}{r_{i}²} \hat{u}_{r_{i}}
\end{align}
$$
El término de la sumatoria corresponde a la acción de todas las partículas del sistema sobre la carga $q_{0}$, este corresponde al [[Campo Eléctrico]] generado por el sistema de cargas.
Si se instala una carga $q_{0}$, se mueve según el sistema de carga inicial.
$$
\vec{E}=\frac{\vec{F}}{q_{0}} \iff  \vec{F}=\pm q_{0} \vec{E}
$$
Para una carga $q$ ,si la fuerza es
$$
\vec{F}=\frac{1}{4\pi\varepsilon_{0}}·\frac{q}{r²}\hat{u}_{r}
$$
entonces, el campo eléctrico de a carga $q$ es:
$$
\vec{E}=\frac{1}{4\pi\varepsilon_{0}}·\frac{q}{r²}\hat{u}_{r}
$$
# Campo Eléctrico
Cuando se instala una carga de prueba a una distancia $r$ de otra, existe 'algo' que le afecta: El Campo eléctrico generado por la carga.
***dibujo carga de prueba a distancia de carga q***
$$
\vec{E}=\frac{1}{4\pi\varepsilon_{0}}·\frac{q}{r²}\hat{u}_{r}
$$
donde $r$ es la distancia a la que se instala la carga de prueba.
Para la unidad de medida del campo eléctrico: si $\vec{F}=q_{0}\vec{E} \iff  \vec{E}=\frac{\vec{F}}{q_{0}} \implies \frac{[N]}{[C]}$
* Para una carga positiva, se puede ver que el campo eléctrico es:
***dibujo1***
* y para una carga negativa:
***dibujo2***

viendo que $\vec{F}=\pm q_{0}\vec{E}$ es similar a $\vec{F}=m \vec{a}$, se puede notar que $\vec{a}$ tendrá la misma dirección que el campo eléctrico $\vec{E}$.
* Si la carga tienen el mismo signo, entonces se mueve en el mismo sentido que el campo eléctrico, y si son distintos, se mueve en sentido contrario al campo eléctrico.

Los vectores visualizados corresponden a las [[líneas de fuerza]].
## Líneas de Fuerza

Son líneas radiales que salen o entran a la carga. Determinan cómo se dibuja e campo eléctrico de una carga.
1. Son tangentes a cada punto del campo eléctrico.
2. Entran en carga positiva y salen en carga negativa.
3. Son **más densas** en donde el campo es más fuerte.
4. Son líneas que 'empiezan' en cargas positivas y 'terminan' en negativas.
	Si se instala una carga de prueba en una zona 'sin líneas', ésta estará en un equilibrio inestable: Si se desplaza un poco la carga, caerá en una línea.
	***dibujo***

***
# clase 07/08

Si se tiene una carga positiva $q$ que genera un campo eléctrico $\vec{E}$ de la forma:
$$
\vec{E}=\frac{1}{4\pi\varepsilon_{0}}·\frac{q}{r²}\hat{u}_{r}
$$
en coordenadas cartesianas, si la posición de $q_{0} = P(x,y,z)$, donde $r=\sqrt{ (x-x_{0})^{2}+(y-y_{0})^{2}+(z-z_{0})^{2} }$, entonces el campo eléctrico en cada eje es:
$$
\begin{align}
\vec{E_{x}}=\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{x-x_{0}}{r} \right) \\
\vec{E_{y}}=\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{y-y_{0}}{r} \right) \\
\vec{E_{z}}=\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{z-z_{0}}{r} \right)
\end{align}
$$

por la condición 1 de tangencialidad de las líneseas de fuerza, y utilizando la derivada en forma de diferencial:
$$
dr=dx \hat{u}_{x}
$$
donde $dr$ es un movimiento infinitesimal, se busca que las líneas sean paralelas, entonces todas las componentes deben ser iguales:
$$
\begin{align}
\frac{dx}{E_{x}}=\frac{dy}{E_{y}}=\frac{dz}{E_{z}} \\ \\

\iff \frac{dx}{\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{x-x_{0}}{r} \right)} = \frac{dy}{\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{y-y_{0}}{r} \right)} = \frac{dz}{\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{2} } \left( \frac{z-z_{0}}{r} \right)}
\end{align}
$$
se simplifican los términos $\frac{1}{4\pi \varepsilon_{0}} \frac{q}{r^{3} }$ por ser constantes, quedando:
$$
\frac{dx}{x-x_{0}}=\frac{dy}{y-y_{0}}=\frac{dz}{z-z_{0}}
$$
si se expresa el diferencial como una diferencia de posición, desde la posición de la carga inicial $(x_{1},y_{1},z_{1})$, para $dx = x_{1}-x_{0}$, entonces:
$$
\frac{x_{1}-x_{0}}{x-x_{0}}=\frac{y_{1}-y_{0}}{y-y_{0}}
$$
osea que para la carga, las líneas que salen son rectas.
***dibujo líneas saliendo y entrando de cargas***
si una carga tiene más carga, la otra podría no tener la suficiente para recibir todas las líneas de fuerza, entonces no necesariamente todas las líneas de fuerza llegan a la otra.

Para el campo eléctrico, se vé que
$$
\vec{E}=\frac{1}{4\pi\varepsilon_{0}}·\frac{q}{r²}\hat{u}_{r}
$$ 
el término $\frac{q}{4\pi\varepsilon_{0}}$ es constante y $\frac{1}{r^{2}}$ depende del radio, así si dos partículas de prueba se encuentran en puntos distintos del espacio, pero a la misma distancia de la carga inicial, sentirán la misma magnitud de campo eléctrico.

## múltiples cargas
Si se tienen múltiples cargas $q_{i}, i\in \{ 1,\dots n \}$ con su propio campo eléctrico $\vec{E_{i}}$ cada una, el campo eléctrico total es la suma del campo eléctrico de todas las cargas del sistema:
$$
\vec{E}_{\text{tot}}=\sum_{i=1}^{n} \vec{E_{i}}
$$
así, para una distribución continua de cargas en el espacio, la sumatoria pasa a ser una integración.

Para integrar en un cuerpo y obtener el campo eléctrico, se utiliza el diferencial del campo eléctrico $d \vec{E}$ para un diferencial de carga $dq$:
$$
d\vec{E}=\frac{1}{4\pi\varepsilon_{0}}·\frac{dq}{r²}\hat{u}_{r}
$$
donde el término del diferencial de carga pasa a ser la **densidad de carga**, que corresponde a la forma en que la carga se distribuye en el cuerpo: $\rho(x,y,z)$
Para el caso de un cuerpo con volumen:
$$
dq \to \rho d\tau
$$
Así
$$
\vec{E}=\frac{1}{4\pi\varepsilon_{0}}\int_{\tau}\frac{\rho d\tau}{r²}\hat{u}_{r}
$$
1. Densidad de carga volumétrica $\rho (x,y,z)$, medida en $\frac{C}{m^{3}}$: se tiene que 
   $$dq=\rho d\tau$$
2. Densidad de carga superficial $\sigma(x,y,z)$, medida en $\frac{C}{m^{2}}$: se tiene que 
   $$dq=\sigma d\Sigma$$
3. Densidad de carga lineal $\lambda(x,y,z)$, medida en $\frac{C}{m}$ se tiene que:
   $$dq=\lambda d \mathcal{l}$$
***Cuando se habla de campo electrostático, éste no cambia en el tiempo (no depende del tiempo)***
El campo electrostático es conservativo, entonces para integrar sólo importa el punto inicial y final.


***
# 
Clase 12/08
## Trabajo y Potencial Eléctrico
Si se tiene una carga de prueba $q_{0}$ moviéndose desde un punto A hasta un punto B, bajo la existencia de un campo eléctrico externo $\vec{E}$, hay un trabajo $\mathbb{W}$ ejercido por la fuerza de coulomb $\vec{F}_{c}$ ejercida sobre la carga de prueba, y, por lo tanto, se puede relacionar con el campo eléctrico mediante la expresión $\vec{F}_{c}=q_{0}\cdot  \vec{E}$
Gráficamente, se tiene la figura:
![[Pasted image 20250813194828.png]]

Si el trabajo que ejerce una fuerza cualquiera se define como la fuerza multiplicada por el desplazamiento, es posible *encontrar el trabajo realizado por la fuerza de coulomb* ejercida sobre la carga de prueba. De la forma:
$$
\begin{align}
 & d\mathbb{W}=\vec{F} d \vec{s} \\
\text{usando que }\vec{F}=\pm q_{0} \vec{E}\implies   & \;d\mathbb{W}=q_{0} \vec{E} \cdot d\vec{S} \\
\text{usando el producto punto} \implies  & d\mathbb{W} = q_{0}E\ ds\ \cos \theta
\end{align}
$$
donde $\theta$ es el ángulo entre el campo eléctrico $\vec{E}$ y el desplazamiento infinitesimal $d \vec{s}$. Luego, para obtener la suma de todos los fragmentos de desplazamiento infinitesimal, se realiza una integración desde el punto $A$ hasta el punto $B$ a través del camino $\mathcal{C}_{1}$
$$
\begin{align}
\mathbb{W}=\int_{\mathcal{C}_{1}}q_{0}\vec{E}\ d \vec{s}  \\
\iff \mathbb{W} = q_{0} \int_{\mathcal{C_{1}}} \vec{E} d \vec{s}
\end{align}
$$
así se tiene ***la integral de línea*** del campo $\vec{E}$ por el camino $\mathcal{C}_{1}$.

Si se toma un camino distinto $\mathcal{C}_{2}$ para ir desde los mismos puntos $A$ hasta el punto $B$, en general no se tiene el mismo trabajo.

De la integral de línea del campo $\vec{E}$, osea:
$$
\mathbb{W}=q_{0}\int_{\mathcal{C}_{1}}\vec{E}\ d \vec{s}
$$
aislando la integral de línea:
$$
\int_{\mathcal{C}_{1}} \vec{E}\ d \vec{s} = \frac{\mathbb{W}}{q_{0}}
$$
donde el término $\frac{\mathbb{W}}{q_{0}}$ corresponde a la **tensión eléctrica entre los puntos $A$ y $B$ a través del camino $\mathcal{C}_{1}$**
Se define la tensión eléctrica entre dos puntos $A$ y $B$ a través del camino $\mathcal{C}_{1}$ de la forma:
$$
T(A \to B \text{ en }\mathcal{C}_{1}) = \int_{\mathcal{C}_{1}}\vec{E}\ d \vec{s}
$$

Al igual que para el trabajo, en general tomar otro camino $C_{2}$ entrega una distinta tensión eléctrica. 

El sentido en el que se recorre un camino $\mathcal{C}_{i}$ es relevante. Desde ello, es posible expresar el trabajo correspondiente al camino $\mathcal{C}_{2}$ expresándolo como el opuesto de la integral de línea, a través del camino $-\mathcal{C}_{2}$, osea:
$$
\mathbb{W}_{2}=-q_{0}\int_{-\mathcal{C}_{2}}\vec{E}\ d \vec{s}
$$
aparte, si esto se suma con el trabajo asociado al camino 1 $\mathcal{C}_{1}$, $\mathbb{W}_{1}=\int_{\mathcal{C}_{1}}\vec{E}\ d \vec{s}$, esto es:
$$
\mathbb{W}_{1}+\mathbb{W}_{2}=q_{0}\int_{\mathcal{C}_{1}}\vec{E}\ d \vec{s}-q_{0}\int_{-\mathcal{C}_{2}}\vec{E}\ d \vec{s}
$$
factorizando por $q_{0}$, queda la expresión 
$$
q_{0}\cdot \varepsilon
$$
donde
$$
\varepsilon = \oint_{\mathcal{C}}\vec{E}\ d \vec{s}
$$
se conoce como **fuerza electromotriz (f.e.m.)**, la cual no es una fuerza pues no tiene dimensiones de fuerza.

### Fuerzas electrostática conservativa
Para las fuerzas conservativas se cumple que el trabajo realizado por ellas es independiente del camino y sólo se considera la posición inicial y final, siendo el trabajo igual a través de todos los caminos: $\mathbb{W}(\mathcal{C}_{1})=\mathbb{W}(\mathcal{C}_{2})=\dots=\mathbb{W}(\mathcal{C}_{n})$
entonces, se puede ver que, como el trabajo desde el punto inicial $A$ hasta el punto final $B$ es el opuesto al trabajo realizado desde $B$ hasta $A$, se concluye que ***el trabajo realizado en camino cerrado es nulo***
$$
\text{Campo electrostatico conservativo }\iff \varepsilon=0
$$

Si bien, no todas las fuerzas eléctricas son conservaticas, esto sí se cumple para la fuerza electrostática, que es generado por un campo electrostático. Entonces se dice que un campo electrostático es conservativo, entonces el trabajo (equivalente a la integral de línea) del campo electrostático se puede expresar como una diferencia de alguna función entre los puntos:
$$
\int_{A}^{B} \vec{E}\ d \vec{s} = f(B)-f(A)
$$

## Potencial Electrostático
desde la expresión:
$$
\int_{A}^{B} \vec{E}\ d \vec{s} = f(B)-f(A)
$$
de funciones $f$ desconocidas, se define el **la diferencia de potencial entre el punto A y B**. del campo $\vec{E}$, expresado como:
$$
V_{A}-V_{B}=\int_{A}^{B}\vec{E}\ d \vec{s}
$$

Así, se puede expresar el trabajo entre los puntos $A$ y $B$ con la diferencia de potencial, reemplazando $\int_{A}^{B}\vec{E}\ d \vec{s}=V_{A}-V_{B}$ en la ecuación del trabajo $\mathbb{W}=q_{0}\int_{\mathcal{C}_{1}}\vec{E}\ d \vec{s}$, quedando:
$$
\begin{align}
 & \mathbb{W}_{AB}=q_{0}(V_{A}-V_{B}) \\
\text{expresando diferencia con delta: } & \mathbb{W}_{AB}=-q_{0}\Delta V 

\end{align}
$$

## Trabajo Electrostático
A cada fuerza conservativa se le puede asociar una energía potencial, y el trabajo entre dos puntos se puede obtener de la forma $\mathbb{W}=-\Delta U$, si se utiliza el potencial eléctrostático, denotado como $U_{e}$, entonces el trabajo electrostático se puede obtener como:
$$
\mathbb{W}_{AB}=-\Delta U_{e}=U_{e}(A)-U_{e}(B) = q_{0}V_{B}\cdot q_{0}V_{A}
$$

## Energía Cinética
El teorema de la energía cinética dice que la variación del trabajo desde un punto $A$  un punto $B$ es la variación de energía cinética $E_{c}$, osea:
$$
\begin{align}
\mathbb{W}_{AB} =  & \Delta E_{c}=\frac{1}{2}mV_{b}^{2}-\frac{1}{2}mV_{A}^{2} \\
\mathbb{W}_{AB} =  & -\Delta U_{e}=Ue(A)-U_{e}(B) \\
 & =q_{0}(V_{A}-V_{B})  \\
\implies & \frac{1}{2}m(V_{B}²-V_{A}²)=q_{0}(V_{A}-V_{B})
\end{align}
$$
si se quiere acelerar la carga: $V_{B}²>V_{A}²$, y, como la masa es positiva $m>0$, entonces:
$$ 
\left\{
	\begin{array}{ll}
		\text{si } q_{0}>0 \implies V_{A}>V_{B} \\
		\text{si } q_{0}<0 \implies V_{A}<V_{B}
	\end{array}
\right.
$$

la energía potencial obliga a la existencia de un campo eléctrico y una carga que lo genera.

Cuando una carga se aceera por la diferencia de potencial de 1[V], ésta adquiere una energía de 1 eV (electronvolt):
$$
eV=1,6\cdot 10^{-19} CV =1,6\cdot 10^{-19} J
$$
es la unidad de energía preferida para describir fenómenos en escalas atómicas.

***
# Clase 14/08
Se tiene que el campo eléctricostático es conservativo, entonces se le puede asociar un potencial:
$$
\mathbb{W}_{AB}=-\Delta U_{e} =q_{0}(V_{A}-V_{B})=-q_{0}\Delta V
$$
entonces, se tiene que la diferencia del potencial eléctrico:
$$
\Delta U_{e}=q_{0}\Delta V
$$
de ello, se vé que no existen cargas fijas. Ellas siempre están en movimiento.

Tomando que 
$$
\mathbb{W}_{AB}=-q_{0}\Delta V =\frac{q_{0}q}{4\pi\varepsilon_{0}}\left( \frac{1}{r_{A}}-\frac{1}{r_{B}} \right) =U_{e}(A)-U_{e}(B)
$$
considerando que $q_{0}q>0$ y $U_{e}(A)>0,\ U_{e}(B)>0\ \implies\ U_{e}(A)-U_{e}(B)>0$ entonces:
$$
\implies \frac{1}{r_{A}}-\frac{1}{r_{B}}>0\iff\frac{1}{r_{A}}>\frac{1}{r_{B}}
$$
si $q_{0}q<0$ entonces:
$$
\implies U_{e}(A)<0,U_{e}(B)<0
$$
y como
$$
\frac{q_{0}q}{4\pi\varepsilon_{0}}<0\implies \frac{1}{r_{A}}-\frac{1}{r_{B}}>0\iff\frac{1}{r_{A}}>\frac{1}{r_{B}}
$$

## Campo Eléctrico como Gradiente del Potencial
El campo electrostático es conservativo, entonces tiene un potencial eléctrico asociado y se puede obtener la diferencia de potencial entre el punto final e inicial. Existe una relación que permite calcular el campo electrostático conociendo el potencial.
Para un desplazamiento infinitesimal, que es el desplazamiento infinitesimal en cada coordenada: $d\vec{r}=dx\vec{u}_{x}+dy\vec{u}_{y}+dz\vec{u}_{z}$ que une dos puntos inicial $A(x,y,z)$ y final $B(x+dx,y+dy,z+dz)$, en donde cada punto tiene su potencial asociado: $V_{A}(x,y,z);V_{B}(x+dx,y+dy,z+dz)$, entonces la variación inifinitesimal de potencial es:
$$
\begin{align}
 & dV=V_{B}(x+dx,y+dy,z+dz)-V_{A}(x,y,z) \\
 & dV=-\vec{E}d\vec{r} \\
 & dV=-E_{x}dx-E_{y}dy-E_{z}dz \\
\end{align}
$$
Y, por el teorema del diferencial total, osea:
$$
\begin{align}
 & f(x+dx)=f(x)+\frac{\partial}{\partial x}fdx \\
 & f(x+dx)-f(x)=\frac{df}{dx}\cdot dx=df
\end{align}
$$
entonces:
$$
\begin{align}
 & dV=V_{B}(x+dx,y+dy,z+dz)-V_{A}(x,y,z) \\
\iff & dV=\frac{\partial}{\partial x}Vdx+\frac{\partial}{\partial y}Vdy+\frac{\partial}{\partial z}Vdz 
\end{align}
$$
Así, se tienen las relaciones por coordenadas del campo eléctrico con el potencial electrostático:
$$
E_{x}=-\frac{\partial}{\partial x}V,E_{y}=-\frac{\partial}{\partial y}V,E_{z}=-\frac{\partial}{\partial z}V
$$

### Relación campo electrostático y potencial
La relación de que la derivada parcial por componentes del potencial entrega cada componente del campo eléctrico, de la forma: $E_{x}=-\frac{\partial}{\partial x}V,E_{y}=-\frac{\partial}{\partial y}V,E_{z}=-\frac{\partial}{\partial z}V$, se puede resumir con el operador $\nabla$ como:
$$
\vec{E}=-\nabla V
$$
a través del cálculo de las derivadas parciales del potencial se puede tener cada componente del campo eléctrico.

### Teorema del Gradiente en potencial
Desde que el diferencial del potencial $dV=-\vec{E}d\vec{s}$, si se tiene que $\vec{E}=-\nabla V$, entonces:
$$
dV=\nabla Vd\vec{s}
$$
y también, si la diferencia de potencial se define como:
$$
\begin{align}
 & V_{A}-V_{B}=\int_{A}^{B}\vec{E}\ d \vec{s} \\
\text{usando }\vec{E} \text{ como }-\nabla V \\
 \implies & V_{A}-V_{B}=-\int_{A}^{B}\nabla V\ d \vec{s} \\
\text{ o bien }\iff  & V_{B}-V_{A}=\int_{B}^{A} \nabla V\ d\vec{s}
\end{align}
$$

Finalmente, es más sencillo calcular $\vec{E}$ con $-\nabla V$ ya que se requiere calcular una sola integral para obtener V y después aplicar el operador $-\nabla$ al potencial para obtener el campo eléctrico (Antes se requería integrar 3 veces). 

## Superficies Equipotenciales
Anteriormente se introdujeron las líneas de fuerzas para representar visualmente el campo eléctrico. Y para visalizar el potencial, se pueden utilizar entidades similares: Las Superficies Equipotenciales.
*def:* **Superficies Equipotenciales**
Una superficie tridimensional en cuyos puntos el potencial toma el mismo valor. El potencial $V$ en un punto en el espacio $(x,y,z)$ es constante:
$$
V(x,y,z)=\text{cte}
$$
al variar el valor de la constante, se obtiene una familia de puntos, que corresponden a la superficie equipotencial.
Gráficamente:
![[Pasted image 20250816112536.png]]
- Las superficies equipotenciales nunca se cruzan: En cada punto pasa solamente una superficie equipotencial.

Si $dV=\nabla V\ d\vec{s}$, por la  [[#Relación campo electrostático y potencial|relación del campo eléctrico y del potencial]] ($\vec{E}=-\nabla V$), entonces:
$$
dV=-\vec{E}\cdot d\vec{s}
$$
de esto se puede ver que para un movimiento $d\vec{s}$ ortogonal al campo eléctrico (y a lo largo de la superficie equipotencial), el producto punto entre $\vec{E}\cdot d\vec{s}$ es nulo. Y por ello, la variación del potencial $dV$ es nulo, correspondiendo así a una superficie equipotencial.

Para un desplazamiento $d \vec{\eta}$ paralelo al campo eléctrico y ortogonal a la superficie equipotencial, orientado en el sentido creciente del potencial, se tienen entonces dos superficies $V_{1},\ V_{2}=V_{1}+dV$:
$$
\begin{align}
 & V_{1}-V_{2}=-dV \\
\text{si }dV=-\vec{E}\ d\vec{s}\iff & -dV=\vec{E}\ d\vec{s} \\
\implies & -dV=-\nabla V\ d \vec{\eta} \\
 \iff & dV=\nabla V\ d \vec{\eta}
\end{align}
$$
definiendo así $dV=|\Delta V|\  d \vec{\eta} \iff|\Delta V|=\frac{dV}{d \vec{\eta}}$ esto indica que *el módulo del gradiente es igual a la derivada del potencial en la dirección ortogonal a la superficie equipotencial, indicando el sentido de crecimiento equipotencial.*
- Las superficies equipotenciales son ortogonales a las líneas de fuerza.

# Rotor del Campo Vectorial

Se considera un rectángulo infinitesimal en el plano $XZ$ denotado por $d\Gamma_{x}$, cuyos vértices son $A,B,C,D$, con largos infinitesimales $AB=dy, BC=dz paralélos a los ejes. Entonces, el área infinitesimal es $d\Sigma=dy\ dz$. Gráficamente:

***wea 3d***

calculando la integral de línea del camino cerrado:
$$
\mathcal{E}=\oint_{\mathcal{C}}\vec{E}\ d\vec{s}=\vec{E}_{AB}·\vec{AB}+\vec{E}_{BC}·\vec{BC}+\vec{E}_{CD}\vec{CD}+\vec{E}_{DA}\vec{DA}
$$
con $\vec{E}_{AB}$ el campo eléctrico en el segmento $\vec{AB}$.
Como $\vec{CD}=-\vec{AB},\ \vec{DA}=-\vec{BC}$:
$$
\begin{align}
 & \vec{E}_{AB}\vec{AB}+\vec{E}_{BC}\vec{BC}+\vec{E}_{CD}\vec{CD}+\vec{E}_{DA}\vec{DA} \\
= & \vec{E}_{AB}\vec{AB}+\vec{E}_{BC}\vec{BC}+\vec{E}_{CD}(-\vec{AB})+\vec{E}_{DA}(-\vec{BC}) \\
= & \vec{E}_{AB}\vec{AB}-\vec{E}_{CD}\vec{AB}+\vec{E}_{BC}\vec{BC}-\vec{E}_{DA}\vec{BC} \\
= & \vec{AB}\ (\vec{E}_{AB}-\vec{E}_{CD})+\vec{BC}\ (\vec{E}_{BC}-\vec{E}_{DA})
\end{align}
$$
los lados corresponden a un diferencial infinitesimal: $\vec{AB}=dy\ \hat{u}_{y},\ \vec{BC}=dz\ \hat{u}_{z}$, asi que se tiene:
$$
=dy\ \hat{u_{y}}(\vec{E}_{AB}-\vec{E}_{CD})+dz\ \hat{u_{z}} (\vec{E}_{BC}-\vec{E}_{DA})
$$
el vector unitario en cada dirección entrega el campo en dicha dirección:
$$ 
= dy\ (\vec{E}_{y}(AB)-\vec{E}_{y}(CD))+dz\ (\vec{E}_{z}(BC)-\vec{E}_{z}(DA))
$$
expresando los lados en coordenadas generales cartesianas, osea:
$$
\begin{align}
AB = z & \\
CD = z & + dz \\
BC = y & + dy \\
DA = y &  \\
\implies \mathcal{E} &  = dy\ (\vec{E}_{y}(AB)-\vec{E}_{y}(CD))+dz\ (\vec{E}_{z}(BC)-\vec{E}_{z}(DA)) \\
 & = dy\ (\vec{E}_{y}(z)-\vec{E}_{y}(z + dz))+dz\ (\vec{E}_{z}(y+dy)-\vec{E}_{z}(y)) 
\end{align}
$$
usando el siguiente desarrollo de taylor:
$$
E_{y}(z+dz)=E_{y}(z)+\frac{\partial E_{y}}{\partial z}dz
$$
entonces la integral de línea queda:
$$
\mathcal{E}=\oint_{\mathcal{C}}\vec{E}\ d\vec{s} =\left( \frac{\partial E_{y}}{\partial z} -\frac{\partial E_{z}}{\partial y} \right) dydz = \left( \frac{\partial E_{y}}{\partial z} -\frac{\partial E_{z}}{\partial y} \right)d\Sigma_{x}
$$
que corresponde al rectángulo en el plano $YZ$, y lo mismo se puede hacer para los otros planos.
El resultado no depende de la forma del contorno de la superficie $d\Sigma$ y para la circulación $d\Gamma$ se toman en cuenta las descomposiciones en cada coordenada $d\Gamma_{z},d\Gamma_{y},d\Gamma_{z}$ de las cuales sólo se toma en cuenta el contorno:
$$
d\Gamma=\left( \frac{\partial E_{y}}{\partial z} -\frac{\partial E_{z}}{\partial y} \right)d\Sigma_{x} + \left( \frac{\partial E_{x}}{\partial z} -\frac{\partial E_{z}}{\partial x} \right)d\Sigma_{y}+\left( \frac{\partial E_{y}}{\partial x} -\frac{\partial E_{x}}{\partial y} \right)d\Sigma_{z}
$$
$d\Gamma$ es un escalar y hay una igualdad a componentes de un vector, así que se introduce el *rotor*



## def: Circulación
> La circulación de $\vec{E}$ por un camino cerrado infinitesimal con una superficie $d\Sigma$ está dada por el flujo del rotor de $\vec{E}$ por la superficie $d\Sigma$

$$
\oint_{\mathcal{C}}\vec{E}\ d\vec{s} = \int_{\Sigma}\nabla \times \vec{E}\ d\Sigma\ \hat{u_{n}} = \int \int (\nabla \times \vec{E})\hat{u_{n}}\ d\Sigma
$$

Si el campo es conservativo entonces la circulación es nula, entonces el rotor es nulo, también dicho *irrotacional*:
$$
\oint_{\mathcal{C}}\vec{E}\ d\vec{s} =\int \int (\nabla \times \vec{E})\hat{u_{n}}\ d\Sigma =0 \iff \nabla \times \vec{E} =0
$$


En resumen, si un campo es conservativo, puede expresarse coo el gradiente de una función escalar y su rotor es cero


# Dipolo Eléctrico

Un dipolo eléctrico es un objeto compuesto por dos cargas opuestas de igual magnitud $q,-q$ separadas en una distancia $a$. Un átomo compuesto de 1 protón y un electrón puede ser un dipolo eléctrico.
A la distancia $a$ se le asigna la dirección desde la carga negativa a positiva, siendo así un vector $\vec{a}$.

Considerando el sistema de un electrón con un protón y que esté en presencia de un campo eléctrico, las cargas sentirán la fuerza asociada al campo eléctrico $\vec{F}_{c}=\pm q\ \vec{E}$. Por la segunda ley de newton, la aceleración es inversamente proporcional a la masa ($\vec{F}=m\vec{a}$), entonces el protón casi no acelera por su gran masa en comparación al electrón.

## Momento de Dipolo Eléctrico

Se define el momento de dipolo eléctrico al vector:
$$
\vec{p}=q\ \vec{a}
$$
este va en la misma dirección que el vector distancia $\vec{a}$, pero se define **saliendo de la carga positiva**.


## Potencial de Dipolo

Un sistema de dos cargas eléctricas genera un potencial eléctrico.
Sea $P(x,y,z)$ el punto en donde se quiere saber el potencial, para el sistema de dos cargas:
> El potencial en un punto no tiene sentido físico, pero sí entre dos puntos. Entonces, tomando el segundo punto en el infinito.

$$
\begin{align}
V(P)-V(\infty)= & \int_{P}^{\infty}\vec{E}\ d\vec{s} \\
\text{por sistema de 2 cargas:} \\
V(P)-V(\infty)= & \sum_{i}^{n} \frac{q}{4\pi\mathcal{E}_{0}r_{i}}=\frac{q}{4\pi\mathcal{E}_{0}r_{1}}+\frac{q}{4\pi\mathcal{E}_{0}r_{2}} \\
\text{si } V(\infty)\to 0, \text{entonces}: \\
V(P)= & \frac{q}{4\pi\mathcal{E}_{0}}\left( \frac{1}{r_{1}}-\frac{1}{r_{2}} \right) \\
V(P) = &  \frac{q}{4\pi\mathcal{E}_{0}}
\left( \frac{r_{2}-r_{1}}{r_{1}r_{2}} \right) \end{align}
$$
considerando al punto $P$ muy lejano al dipolo: $r_{2}-r_{1}=a\cos \theta,\ \ r_{1}r_{2}=r^{2}$, entonces:
$$
\begin{align}
V(P)= & \frac{qa\cos \theta}{4\pi\mathcal{E}_{0}r^{2}} \\
V(P)= & \frac{p\cos \theta}{4\pi\mathcal{E}_{0}r^{2}} \\
V(P)= & \frac{\vec{p} \hat{u_{r}}}{4\pi\mathcal{E}_{0}r^{2}}
\end{align}
$$
donde $\hat{u_{r}}$ es el versor que va desde el punto medio entre las cargas $O$ y el punto de interés $P$.
Desde la última expresión:
$$
V(P)= \frac{\vec{p} \hat{u_{r}}}{4\pi\mathcal{E}_{0}r^{2}}
$$
se vé que el potencial en el punto $P$ generado por el dipolo eléctrico depende sólamente del momento del dipolo eléctrico. Así, si se tienen cargas de mayor o menor magnitud, generan el mismo potencial.

## Campo Eléctrico de Dipolo
 Se pueden calcular las componentes del campo eléctrico en coordenadas esféricas como:
 $$
\begin{align}
  &  E_{r}=  -\frac{\partial V}{\partial r}  \\
 \iff & E_{r}= \frac{2p\cos \theta}{4\pi \varepsilon_{0}r^{3}} \\

E_{\theta}= & -\frac{1}{r}\frac{\partial V}{\partial \theta} \\
\iff  &  E_{\theta} = \frac{p \sin \theta}{4\pi\varepsilon_{0}r^{3}} \\

E_{\phi}= & -\frac{1}{r\sin \theta}\frac{\partial V}{\partial \phi} \\
 & E_{\phi}=0
\end{align}
$$
entonces el campo eléctrico está en el plano $\{ \vec{p},\hat{u_{r}} \}$, vectorialmente:
$$
\begin{align}
 & \vec{E}=E_{r}\hat{u}_{r}+E_{\theta}\hat{u}_{\theta} \\
\iff & \vec{E}= \frac{2p\cos \theta}{4\pi \varepsilon_{0}r^{3}}\hat{u}_{r} + \frac{p \sin \theta}{4\pi\varepsilon_{0}r^{3}} \hat{u}_{\theta} \\
\iff & \vec{E}=\frac{p}{4\pi\varepsilon_{0}r^{3}}(2\cos \theta\hat{u}_{r}+\sin \theta \hat{u}_{\theta})
\end{align}
$$
y el módulo del campo eléctrico será:
$$
E=\frac{p}{4\pi\varepsilon_{0}r^{3}}\sqrt{ 3\cos ^{2}\theta+1 }
$$
de esto se vé que el **campo eléctrico disminuye con el cubo de la distancia al dipolo**, y el ángulo $\alpha$ del campo eléctrico $\vec{E}$ con respecto a $\hat{u}_{r}$ es:
$$
\alpha=\frac{E_{\theta}}{E_{r}}=\frac{1}{2}\tan \theta
$$
## Fuerza sobre un dipolo
Si se tiene un dipolo en una región con un campo eléctrico, éste va a sentir una fuerza debido a la acción del campo eléctrico.
Dado un dipolo con una carga $-q$ en el punto $P_{1}(x,y,z)$ y otra carga $+q$ en el punto $P_{2}(x+a_{x},y+a_{y},z+a_{z})$ unidos por el vector $\vec{a}=a_{x}\hat{u}_{x}+a_{y}\hat{u}_{y}+a_{z}\hat{u}_{z}$, siendo el momento del dipolo $\vec{p}=q\vec{a}$, gráficamente:
![[Pasted image 20250823093021.png]]
Por la región del campo eléctrico, la energía potencial electrostática  será:
$$
U_{e}=qV(x+a_{x},y+a_{y},z+a_{z})-qV(x,y,z)
$$
y si las distancias $a_{x},a_{y},a_{z}$ son infinitesimales, pasan a ser $dx,dy,dz$, quedando la energía potencial como
$$
U_{e}=(x+dx,y+dy,z+dz)
$$
usando desarrollo de Taylor:
$$
U_{e}=V(x,y,z)+\frac{\partial V}{\partial x}a_{x}+\frac{\partial V}{\partial y}a_{y}+\frac{\partial V}{\partial z}a_{z}
$$
> ???

así la energía electrostática del dipolo es
$$
\begin{align}
U_{e}= & q \frac{\partial V}{\partial x}a_{x}+ q\frac{\partial V}{\partial y}a_{y}+\frac{\partial V}{\partial z}a_{z} \\
\text{si } \nabla V·\vec{p}=-\vec{E}·\vec{p}: & \\
U_{e}= & -\vec{p}·\vec{E} \\
U_{e}= & -p·e·\cos \theta
\end{align}
$$
con $\theta$ el ángulo entre el campo eléctrico $\vec{E}$ y el momento del dipolo $\vec{p}$.

## Torque (Momento) en Dipolo
Si se tiene un campo eléctrico $\vec{E}$ uniforme, la fuerza sobre las cargas serán iguales en magnitud pero opuestas por el signo de su carga. Pero sí habrá un torque ejercido por las fuerzas **que llevará al dipolo a la posición de mínima energía potencial, que corresponde al dipolo en paralelo al campo eléctrico**, alinéandose el momento dipolar $\vec{p}$ con el campo eléctrico $\vec{E}$ de forma paralela.

Considerando un campo eléctrico horizontal de $\theta=0$ y el dipolo fuera de su posición estable, en un ángulo $\theta$, este está sujeto a un torque (o momento) $\vec{M}$ ejercido por las fuerzas para que el dipolo vuelva a una posición de equilibrio $\theta=0$ en donde la energía potencial sea la mínima; viendo los valores de la energía potencial para distintos $\theta$:
$$
\begin{align}
\text{si }U_{e}=-\vec{p}·\vec{E}·\cos \theta: \\
\theta=0\implies &  U_{e}=-pE \\
\theta=\frac{\pi}{2}\implies & U_{e}=0 \\
\theta=\pi \implies & U_{e}=pE
\end{align}
$$
osea, para $\theta=0$ se tiene que la energía potencial es la menor posible.

Para obtener el torque con respecto al centro del dipolo:
$$
\begin{align}
\text{si }\vec{\tau}=\sum_{i}^{n} r_{i}\times \vec{F}_{i}: \\
\vec{\tau}= & \vec{r}_{1}\times \vec{F}_{c_{1}}+\vec{r}_{2}\times \vec{F}_{c_{2}} \\
\text{si } \vec{F}_{c_{i}}=q_{i}·\vec{E}:\\
\implies\vec{\tau}= & \vec{r}_{1}\times (q\vec{E})+\vec{r}_{2}\times((-q)·\vec{E}) \\
\vec{\tau}= & \vec{r}_{1}\times (q\vec{E}) - \vec{r}_{2}\times (q\vec{E}) \\
\vec{\tau}= & (\vec{r}_{1}-\vec{r}_{2})\times q\vec{E} \\
\text{donde }(\vec{r}_{1}-\vec{r}_{2})=\vec{a}: \\
\implies \vec{\tau}= & \vec{a}\times q\vec{E} \\
\iff \vec{\tau}= & q\vec{a}\times \vec{E} \\
\text{y el momento del dipolo }\vec{p}= q\vec{a}: \\
\implies \vec{\tau}= & \vec{p}\times \vec{E}
\end{align}
$$
de donde se vé que el torque $\vec{\tau}$ sale del plano, y explicitando el producto punto:
$$
\begin{align}
\tau=-pE\cos \theta \\
\tau=-\frac{dU_{e}}{d\theta}
\end{align}
$$
no es derivada parcial pues la energía sólo depende del ángulo.

## Campo eléctrico No Uniforme

Si el campo no es uniforme, hay una resultante de las fuerzas sobre el dipolo $\vec{F}$ no nula por ser las fuerzas sobre cada carga distintas.
Expresando esta diferencia de fuerzas por la diferencia en el campo eléctrico:
$$
\begin{align}
\vec{F}_{1}= & -q\vec{E} \\ \\

\vec{F}_{2}= & q(\vec{E}+d\vec{E}) \\
\text{usando  taylor:} \\
\vec{F}_{2}= & q\left( \vec{E}+\frac{\partial \vec{E}}{\partial x}a_{x}+\frac{\partial \vec{E}}{\partial y}a_{y}+\frac{\partial \vec{E}}{\partial z}a_{z}  \right) 
\end{align}
$$
así la fuerza total es:
$$
\vec{F}=\vec{F}_{1}+\vec{F}_{2}= q \frac{\partial \vec{E}}{\partial x}a_{x}+ q\frac{\partial \vec{E}}{\partial y}a_{y}+\frac{\partial \vec{E}}{\partial z}a_{z}
$$
donde $q·a_{x}=p_{x}$:
$$
\vec{F}=p_{x}\frac{\partial \vec{E}}{\partial x}+ p_{y}\frac{\partial \vec{E}}{\partial y}+p_{z}\frac{\partial \vec{E}}{\partial z}
$$
que es **válida tambien para campos no conservativos**, y de forma compacta:
$$
\vec{F}=(\vec{p}·\nabla)\vec{E}
$$

Como en un campo conservativo se debe cumplir que:
$$
\begin{align}
\vec{F}= & -\nabla U_{e} \\
\vec{F}= & -\nabla(-\vec{p}\vec{E}) \\
\vec{F}= & \nabla(\vec{p}\vec{E}) \\
\vec{F}= & \nabla(p_{x}E_{x}+p_{y}E_{y}+p_{z}E_{z})
\end{align}
$$
viendo las componentes por separado:
$$
\begin{align}
F_{x}= & \frac{\partial}{\partial x}(\vec{p}\vec{E}) \\
F_{x}= & p_{x}\frac{\partial \vec{E}_{x}}{\partial x}+ p_{y}\frac{\partial \vec{E}_{x}}{\partial x}+p_{z}\frac{\partial \vec{E}_{x}}{\partial x} \\
 \\
F_{y}= & \frac{\partial}{\partial y}(\vec{p}\vec{E}) \\
F_{y}= & p_{x}\frac{\partial \vec{E}_{x}}{\partial y}+ p_{y}\frac{\partial \vec{E}_{y}}{\partial y}+p_{z}\frac{\partial \vec{E}_{x}}{\partial y} \\
 \\
F_{z}= & \frac{\partial}{\partial z}(\vec{p}\vec{E}) \\
F_{z}= & p_{x}\frac{\partial \vec{E}_{x}}{\partial z}+ p_{y}\frac{\partial \vec{E}_{y}}{\partial z}+p_{z}\frac{\partial \vec{E}_{x}}{\partial z}
\end{align}
$$

## Interacción entre Dipolos
Dos dipolos de momentos $p_{1},p_{2}$ a una distancia $r$ interactúan por estar sometidos cada uno al campo eléctrico del otro.

$$
U_{e}=\frac{p_{1}p_{2}}{4\pi\varepsilon_{0}r^{3}}(\sin \theta_{1}\sin \theta_{2}-2\cos \theta_{1}\cos \theta_{2})
$$
donde $\theta_{1},\theta_{2}$ son los ángulos formados por los vectores $\vec{p}_{1}-\hat{u}_{r},\vec{p}_{2}-\hat{u}_{r}$ respectivamente.

Y la fueza de un dipolo sobre otro es
$$
\vec{F}_{2}=-\nabla U_{e}=-\frac{\partial U_{e}}{\partial r}\hat{u}_{r}=\frac{3p_{1}p_{2}}{4\pi\varepsilon_{0}r^{4}}\hat{u}_{r}
$$
para dipolos de momentos paralelos:
$$
\vec{F}=-\frac{6p_{1}p_{2}}{4\pi\varepsilon_{0}r^{4}}\hat{u}_{r}
$$