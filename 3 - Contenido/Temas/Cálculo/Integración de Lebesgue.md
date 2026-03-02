#Educación #Cálculo 
Se definen las 'integrales simples', que tienen integrales fáciles de calcular, y para el resto, se hará una aproximación a ellas.

# Teoría
## *def:* función simple
Sea $f:\mathbb{R} \rightarrow \mathbb{R}^d$ una función, f es **simple** si:
	hay una cantidad finita de números y conj. medibles tq:$$	\exists (a_i)_{i=1}^p \subseteq \mathbb{R}, \: \exists(A_i)_{i=1}^P\subseteq \mathbb{R}^d$$
	$$
	\forall x \in \mathbb{R}^d,\: f(x)=a_i\: \leftrightarrow\: x\in A_i
	$$
## *def:* Indicatriz o función característica
Para un conjunto $A \subseteq \mathbb{R}^d$, se define su **indicatriz o función característica** a la función que es igual a 1 dentro de A y 0 fuera de él:
$$
1_A(x) = 
\left\{
	\begin{array}{ll}
		1\; , \text{si } x\in A \\
		0\; , \text{si } x\notin A
	\end{array}
\right.
$$
Entonces, $f$ es ***simple*** si tiene la forma:
$$
f(x) = \sum_{i=1}^p a_i\; 1_{A_i}
$$
Por lo tanto,
si $f$ es una función simple:
$$
\int_{\mathbb{R}^n}f\; du = \sum_{i=1}^p a_i \; \mu (A_i)
$$

donde $a_i$ representa la altura de un área y $\mu (A_i)$ representa su base.

Para denotar una integral en varias variables:
$$
\int_{[a,b]}f(x)dx \rightarrow \text{pasa a ser}\rightarrow \int_{A}f\:d\mu
$$
- A es el conjunto en donde se integra.
- $f$ es la función que se integra, osea el *qué*.
- $d\mu$ representa el cómo se integra (con respecto a qué variable).

## Aproximación de funciones no simples

Para funciones no simples se realiza una aproximación:

***def:*** Soporte de función.
Se define el conjunto de los puntos donde la función **es distinta de cero**.
Sea $f:\mathbb{R}^d \rightarrow \mathbb{R}$ una función, el soporte de la función:
$$
\text{Supp}(f) = \{x \in \mathbb{R}^d, f(x)\neq 0 \}
$$
*se va a restringir al caso de funciones acotadas con soporte compacto.*

Se definen los conjuntos:
$$
\xi_{+}=\{ g:\mathbb{R}^d \rightarrow \mathbb{R}\; \text{simples}:f\leq g \}
$$
	las funciones simples $g$ que mayoran a $f$
$$
\xi_{-}=\{ g:\mathbb{R}^d \rightarrow \mathbb{R}\; \text{simples}:f\geq g \}
$$
	las funciones simples $g$ que minoran a $f$
como $f$ es acotada, entonces $\exists m(f)=\text{inf}\{f(x):x \in \mathbb{R}^d\}$ y $\exists M(f)=\text{sup}\{f(x):x \in \mathbb{R}^d\}$
(existen ínfimo y supremo de la función). Así
$$
\forall x\in\mathbb{R}^d,\: m(f)\leq f(x)\leq M(f)
$$
y escribiendo con indicatriz:
$$
m(f)\mathbb{1}_{\text{supp}(f)} \leq f(x) \leq M(f)\mathbb{1}_{\text{supp}(f)}
$$
### Integrales
Los conjuntos de integrales inferiores y superiores:
$$
II(f)=\text{sup}\left\{ \int g\;d\mu:g \in \xi_{+}(f)  \right\}
$$
$$
IS(f)=\text{inf}\left\{ \int g\:d\mu:g \in \xi_{-}(f) \right\}
$$
Así, en general, se cumple que $II(f) \leq IS(f)$
Y ***una función será integrable según Lebesgue si:*** 
$$
II(f) = IS(f)
$$
Y su integral es 
$$
\int_{\mathbb{R}^d}f\: d\mu = II(f)=IS(f)
$$
entonces, ***la integral de f sobre el conjunto A será:***
$$
\int_{A}f\:d\mu=\int_{\mathbb{R}^d}f_{A}\:d\mu=\int_{\mathbb{R}^d}f(x)\:\mathbb{1}_{A}(x)
$$
**propiedades:**
Dadas $f,g:\mathbb{R}^d\rightarrow\mathbb{R}$ acotadas, con soporte compacto. Para $\lambda \in \mathbb{R}$:
1. $\int_{A}(\lambda f+g)d\mu=\lambda \int_{A}fd\mu + \int gd\mu$
2. $\int_{A}\mathbb{1}d\mu = \mu(A)$
3. Si $\forall x \in A,\;f(x)\leq g(x) \implies \int_{A}fd\mu\leq \int_{A}gd\mu$
4. Si $\exists c>0,\; |f(x)|\leq C \implies|\int_{A}fd\mu |\leq \int_{A}|f|d\mu\leq C\mu(A)$
5. Si $\mu(A)=0 \implies \int_{A}fd\mu=0$
6. Si $A,B \subseteq \mathbb{R}^d:\mu(A \cap B)=0 \implies \int_{A \cap U} fd\mu=\int_{A}fd\mu+\int_{B}fd\mu$

## Integral de Riemann

Sea $A \subseteq\mathbb{R}$, A tiene medida nula si $\mu(A)=0$, si $\mu(A)=0 \implies \forall \varepsilon>0,\exists U_{\varepsilon}>A:\mu(U_{\varepsilon})<\varepsilon$, entonces:
$$
\mu(A)=0 \leftrightarrow  \forall \varepsilon>0,\exists U_{\varepsilon}>A:\mu(U_{\varepsilon})<\varepsilon
$$
***teorema:***
Sea $U \subseteq \mathbb{R}^d\: \text{abierto} \implies \exists(I_{n})_{n\in \mathbb{N}}$ a lo más numerable, de intervalos d-dimensionales distintos, tal que: $U=\bigcup_{n\in \mathbb{N}}I_{n}$
$$
\mu(U_{\varepsilon})<\varepsilon
$$
$$
\mu\left( \bigcup_{n \in \mathbb{N}}I_{n} \right)<\varepsilon=\sum_{n\in \mathbb{N}}\mu(I_{n})<\varepsilon
$$
***teorema:***
Sea $f:\mathbb{R}^d \to \mathbb{R}$ y sea $A \subseteq \mathbb{R}^d$ Jordan-medible
y sean:
$$
C_{f}(A)=\{ x\in A:f\: \text{es continua en x} \}
$$
$$
D_{f}(A)=\{ x \in A:f\;\text{no es continua en x} \}
$$
Entonces $f$ es Riemann-integrable sobre A si y solo si $\mu(D_{f}(A))=0$

***teorema:***
Sea $A\subseteq \mathbb{R}^d$ acotado,
	A es Jordan-medible $\leftrightarrow\mathbb{1}_{A}$ es Riemann-integrable

## Integrales Impropias

Primero se va a suponer que función $f$ es positiva: $f(x)\geq 0$

### 1. Dominio no acotado
$$
\int_{A}fd\mu=\lim_{ R \to \infty } \int_{A\cap B(O,R)}fd\mu
$$
El límite existe o es infinito.
**f es integrable sobre A si el límite existe.**

### 2. Función no acotada

Se define la truncación de f a altura t como:
$$
f_{t}(x) =\text{min}\{ f(x),t \}
$$
si A es acotado:
$$
\int_{A}fd\mu=\lim_{ t \to \infty } \int_{A}f_{t}d\mu
$$
el límite existe o es infinito.
***$f$ es integrable si el límite existe.

### 3. Dominio y función no acotada
$$
\int_{A}fd\mu=\lim_{ t \to \infty } \int_{A\cap B(0,R)}f_{t}d\mu
$$
### Caso f no positiva:
se define la parte positiva y negativa de $f$:
La parte positiva:
$$
f^+(x)=\text{max}\{ f(x),0 \}
$$
La parte negativa:
$$
f^-(x)=\text{max}\{-f(x),0 \}
$$
Se cumple que $$
f(x)=f^+(x)-f^-(x)
$$
y que $$
f^+(x) \geq 0,\: f^-(x)\geq 0
$$
$f$ es integrable sobre A si $f^+\; \text{y}\;f^-$ son integrables sobre A, y su integral es:
$$
\int_{A}fd\mu=\int_{A}f^+d\mu-\int_{A}f^-d\mu
$$

# Teorema de Fubini
Si $f$ es integrables en $A\subseteq \mathbb{R}^d$, entonces:
$$
\int_{A}fd\mu=\int_{R_{1}(A)}\int_{A(x')}f(x',x'')\;d\mu_{d-s}(x'')\;d\mu_{s}(x')
$$
con $$
A(x'')=\{ x'\in \mathbb{R}^S:(x',x'')\in A \}
$$
$$
R_{2}(A)=\{ x''\in \mathbb{R}^{d-S}:A(x')=\phi \}
$$
### método para resolver:
1. Ver cuál es el conjunto A en donde se integra.
2. Ver cuál diferencial esta antes: Para la variable más al interior se debe ver cómo escribirla en función de las exteriores. Con ello, se tienen **los límites de integración**.

## Teorema de Cambio de Variable
Sean $f:\mathbb{R}^d \to \mathbb{R}\;,\; g:\mathbb{R}^d \to \mathbb{R}^{-d}$

### Transformaciones Lineales
cuando $g$ es una transformación lineal,

sea $f: \mathbb{R}^d \to \mathbb{R}$ una función integrable sobre un conjunto $A \subseteq \mathbb{R}^d,\; g:\mathbb{R}^d\to \mathbb{R}^d$ biyectiva y de clase $C^1$ en A, entonces:
$$
\int_{A}fd\mu=\int_{g^{-1}(A)}(f \circ g)\;|\text{det}(J_{g})|d\mu
$$
