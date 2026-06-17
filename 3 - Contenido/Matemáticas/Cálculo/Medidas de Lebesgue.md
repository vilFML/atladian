
La integración de Riemann es imprecisa y también hay muchas funciones que no son Riemann Integrables, por ello, actualmente se utiliza la Integración de Lebesgue.
	
Para realizar la integración de Lebesgue se requiere construir la **medida de Lebesgue**:

## 1. Intervalos de dimensión 'd'

si para 1 dimensión d = 1: $[a,b] = \{x \in \mathbb{R}: a\leq x  \leq b\}$
para 2 dimensiones, d = 2: $[a,b] \times [c,d]$
para 3 dimensiones, d = 3: $[a_1,b_2] \times [a_3,b_3] \times [a_3,b_3]$

entonces para 'd' dimensiones:
$$\prod_{i=1} ^{d} [a_i,b_i] $$
y la **medida** de los intervalos,
para dimensión 1, d = 1: $\mu_1 ([a,b]) = b-a$
para 2 dimensiones, d = 2: $\mu_2 ([a,b] \times [c,d]) = (b-a)(d-c)$

y la medida para 'd' dimensiones:
$$\mu_d(I) = \prod_{i=1}^d (b_i-a_i)$$


## 2. Reticulado
Es un conjunto finito de hiperplanos perpendiculares a los ejes.
Para cada dimensión 'i', se tiene una partición $\rho^i$:
$$\rho^i = \{x_1^i<x_2^i<x_3^i<...<x_{m_i}^i\}$$
así para cada $1\leq i \leq d \:, 1 \leq j \leq m_1^i$

*definición:* ***Hiperplano***
$$H_j^i = \{ (x^1,\cdots,x^d) \in \mathbb{R}^d,x^i=x_j^i \}$$
Así, un reticulado divide $\mathbb{R}^d$ en dos zonas: Los intervalos de dimensión 'd' y las zonas no acotadas.

	-***grafico** 

## 3. Figuras
Es una unión finita de intervalos d-dimensionales de un reticulado.
$$F = \cup_{i=1}^n \:I_i$$
y la **medida** de la figura esta dada por:
$$\mu(F)=\sum_{i=1}^n \: \mu(I_i)$$
	*observación:* Una figura puede estar determinada por infinitos reticulados, pero la medida de la figura es invariante del o los reticulados que la definen.
la medida de una figura es igual a la medida de su interior, ya que si no se consideran sus bordes, la diferencia es mínima:$$ \mu(F) = \mu(\;Int(F)\;)$$
*dem en notas.*

***propiedad:*** Si $F_1, F_2 \subseteq \mathbb{R}^d$ dos figuras, entonces $F_1 \cup F_2$ es una figura, y:
- Cumple que la medida de la unión de las figuras, es menor o igual que la suma de la medida de cada figura, osea: $$\mu(F_1 \cup F_2) \leq \mu(F_1)+\mu(F_2)$$
- y si son figuras disjuntas, entonces la medida de la unión de las figuras es la suma de las medidas de cada una: $$F_1 \cap F_2 = \phi \Rightarrow \mu(F_1 \cup F_2) = \mu(F_1)+\mu(F_2)$$
***propiedad***: si una figura está contenida en otra, entonces la medida de la contenida es menor o igual a la que la contiene: $$F_1 \subseteq F_2 \Rightarrow \mu(F_1) \leq \mu(F_2)$$
### Medida de Conjuntos Abiertos Acotados
Sea $U \subseteq \mathbb{R}^d$ abierto y acotado, su medida es: $$\mu(U) = sup\{\:\mu(F): F\subseteq U \: \}$$
*recuerdo*: para que tenga supremo:
1. U debe tener elementos, osea distinto de vacío: $U \neq \phi$
2. U tiene que ser acotado: *dem. en notas*


## 4. Conjuntos Compactos
Sea $K \subseteq \mathbb(R)^d$ un conjunto compacto, su medida estará dada por: 
$$\mu(K) = inf \{\:\mu(F):K\subseteq int(F)\;\}$$
	***observación***: Existe ínfimo por:
	1. Estar acotado: Ya que toda medida tiene como cota inferior el 0.
	2. Ser no vacío.


## 5. Conjunto Acotado
Sea $A \subseteq \mathbb(R)^d$ un conjunto acotado, diremos que A es **medible** si cumple que:
$$\forall \epsilon > 0, \exists \:  U_{\epsilon} \supseteq A, \exists K_{\epsilon} \text{ compacto} \subseteq A$$
y la **medida** del conjunto compacto A es:
$$\mu(U_{\epsilon}\backslash K_A) < \epsilon \equiv U_{\epsilon} \cap K_{\epsilon}^C$$
Así, se tiene un conjunto A y se acota superiormente por un conjunto abierto e inferiormente por un conjunto compacto:
$$ K_{\epsilon} \subseteq A \subseteq U_{\epsilon}$$
así su medida está acotada por un epsilon:
$$\mu(U_{\epsilon} \backslash K_{\epsilon}) < \epsilon$$
entonces, la **medida** de A es:
$$ \mu(A) = sup \{\; \mu(K):K\subseteq A\; \} = inf \{\; \mu(U):A\subseteq U \;\}$$
Por lo tanto, ==A es medible si el supremo de la medida de K y el ínfimo de la medida de U son iguales.==

***propiedad: monotonía de la medida***
Dados $A,B \subseteq \mathbb(R)^d$ medibles:
$$ A\subseteq B \Rightarrow \mu(A) \leq \mu(B) $$
