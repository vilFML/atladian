Materia: Termodinámica
	Fecha cátedra: 04/08/25
	Fecha digitalización: 06/08/25
	*tags:* #Educación #Física/Termodinámica

# Orígenes de la termodinámica

En la revolución industrial, se pidió estudiar la eficiencia de una máquina de vapor.

La termodinámica tiene su origen en la sustentabilidad, pues se busca asegurar las necesidades del presente sin comprometer las futuras. Así, se busca optimizar los recursos.

**La física impone límites a la eficiencia de uso energético**, según las [[leyes de la termodinámica]]:
1. La energía no se crea ni se destruye, se transforma; *No podemos ganar*.
2. No se puede usar toda la energía disponible, sólo en el cero absoluto; *condición de empate.*
3. No es posible alcanzar el cero absoluto. *No se puede empatar.*

***
# Información

En mecánica, para describir el movimiento de una partícula, se tienen la [[posición]] y [[velocidad]]. Donde cada una tiene 3 números: $r=(x,y,z)\;;\;\dot{r}=(r_{x},r_{y},r_{z})$.
Luego, se necesitan 6 números para informar acerca del movimiento de una sola partícula en un instante.
- En computación, para representar un número real, asumiendo una cierta precisión, se necesitan aproximadamente **400 bits**. Entonces, para los 6 números reales se necesitan 2,4 kBits
- 
En termodinámica se considera un número mayor de partículas, por ejemplo, para la cantidad de partículas en 1 centímetro cúbico de materia gaseosa, se tendrían $3\cdot 10^{19}$ átomos y, para un sólido, aproximadamente $10^{23}$ átomos. Así, para especificar su estado en cierto instante de tiempo se requieren alrededor de $10^{23}$ bits. Esto supera en la cantidad de información que se puede almacenar en todos los discos duros existentes. Aparte, si se quiere describir la trayectoria de las partículas, se necesitarían alrededor de $10^{40}$ términos. No existe capacidad computacional para almacenar ni para el proceso de estos datos.

## Ejemplo: Rebote de pelota en superficie

Se considera el estado inicial (punto desde donde se suelta) y final (punto máximo de altura luego de rebotar) de la situación.
1. Estado inicial: Evidentemente, la energía total del sistema corresponde a la energía potencial gravitatoria.
2. Estado final: La energía del sistema ya no es tan evidente. Se tiene una energía potencial gravitatoria, pero hay una pérdida de ella debido a la menor altura que alcanza la pelota.
Entonces, ***en dónde se encuentra esa diferencia de energía?***

# Factores de Peso o Probabilidad

En el sistema, al pasar desde el estado inicial al final, hubo una **pérdida de información**. 
- ***Un sistema con información permite que se pueda generar energía con él.***

El ***factor de peso (o probabilidad)*** es una magnitud real, que cumple:
$$
0 \leq x_{i}\leq_{1}
$$
y
$$
\sum x_{i}=1
$$

Se busca una magnitud que mida la información faltante: Se tendría una función $f$ que describa la incertidumbre (o ignorancia), que cumpla:
- $f(x)\geq 0$
- $f(x)=0 \leftrightarrow \text{certeza}$
- $f(pq)=f(p)+f(q)$
Se puede ver que la función logaritmo natural cumple estos puntos.
Si se busca matemáticamente la función:
$$
\begin{align}
f(xy)f(x)+f(y)\;  /\frac{\partial}{\partial x}\\ \\
f'(xy)y = f'(x)\; / \frac{\partial}{\partial y} \\ \\
f''(xy)xy+f'(xy)=0 \\ \\
\text{si }w=xy, \\ \\
f''(w)w+f'(w)=0 \\ \\
(f'w)'=0 \implies f'w = \text{cte} \iff f'=\text{cte} \\ \\
\implies f(w)=A+\text{cte }\ln(w) \\ \\
\text{si } f(1)=0 \implies A=0 \\ \\
\therefore f(w)=-K\ln (w), K>0
\end{align}
$$

***
Se usa el promedio de la información del error. Así, info faltante prom $\bar{f} = <f>$, se usa función $I(\cdot)$
$$
I=\sum_{i=1}^{\Omega}f(x_{i})x_{i}
$$
y como $f(x_{i})=-K\ln(x_{i})$, entonces:
$$
I=-K\sum_{i=1}^{\Omega}x_{i}\ln(x_{i})
$$
que cumple que $0\ln(0)=0$, por l'Hopital, para evento de certeza.
- $I(·)$ se anula si alguno de los $i$ eventos se conoce con certeza:
$$
I=0, \text{ si }x_{i}=1
$$
- $I(·)$ es máxima si $x_{i}=\text{cte}$ (no depende del número de evento $i$), osea ***$I(·)$ es máxima si los eventos son equiprobables.
$$
I_{\text{máx}}=K\ln(\Omega)
$$

K determina la unidad en la que se está midiendo $I(·)$, 
1. Si $K=1 \implies I_{2}=$, se mide en 'neps'.
2. Si $K=\frac{1}{\ln(2)} \implies I=-\sum x_{i}\log_{2}(x_{i})$, se mide en **bits**. Ejemplo, la memoria computacional:
   La memoria es un conjunto de compartimientos que almacena un '0' o un '1', entonces se tienen 2 configuraciones en una sola casilla. Entonces para 'n' casillas se tienen $2^n$ configuraciones.

***
# Compactación
Es el proceso de eliminar información que no es completamente relevante.
	Ejemplo: '¿Qué?' -> Q?

***
## $I_{2}$ como número de mediciones

La función $I_{2}(·)=\sum_{i=1}^{\Omega}x_{i}\log_{2}(x_{i})$ se puede interpretar como el número promedio de opciones binarias.

Ejemplo: Algoritmo de búsqueda de guía telefónica:

| Numero de mediciones | Opciones             |
| -------------------- | -------------------- |
| 0                    | 0                    |
| 1                    | $\frac{\Omega}{2}$   |
| 2                    | $\frac{\Omega}{2·2}$ |
| $\vdots$             | $\vdots$             |
| n                    | $\frac{\Omega}{2^n}$ |
y se llega al final si el número de opciones es 1 o aproximadamente 1.
$$
\begin{align}

\frac{\Omega}{2^n} \approx 1  \\ \\

\therefore \log_{2}(\Omega)=n
\end{align}
$$
es posible obtener la información desconocida máxima como:
$$
S = k_{b}\ln(\Omega)
$$
con $\Omega$ el número de configuraciones posibles.

# Clase 08/08
No es posible describir el sistema viendo el comportamiento de cada partícula, entonces se usa una capa de abstracción del sistema de forma que se representa a nivel macro como una "caja negra". Al hacer esto se dice que se pierde información acerca del sistema, pero en realidad hay una información que nunca se tuvo.

# Microestado y Macroestado
## Microestado, Configuración o Estado microscópico
Es especificar las variables de cada partícula que compone el sistema.

## Macroestado
Es la descripción del sistema a mayor escala, con variables macroscópicas: Estas son relativamente pocas y en general son manejables.
* Un mismo macroestado puede estar dado por distintos microestados, osea existen muchas configuraciones que corresponden al mismo macroestado, pero no son infinitas.

	Ejemplo: Vacante (espacio vacío) en un sólido:
	Un sólido puede tener un espacio vacío entre sus partículas. Este espacio puede cambiar de posición a cualquier partícula que compone el objeto, entonces:
	sólido con $n$ espacios $\implies n$ configuraciones para 1 mismo macroestado (la misma manifestación del sólido).
		\* las vacantes si se manifiestan visualmente, ejemplo: irradiar a un gas con una cantidad creciente de vacantes varía su color.

Una configuración no puede corresponder a más de un macroestado.
	Ejemplo: Velocidad de partículas dentro de un gas.
	Múltiples posibles velocidades para las partículas que componen el gas, pero éstas resultan la misma presión.

## Configuraciones Accesibles ($\Omega$)
Dado un macroestado, las configuraciones que lo entregan se dicen **configuraciones accesibles** del macroestado.
El número de configuraciones accesibles se denota con $\Omega$
### propiedades:
1. El número de configuraciones accesibles $\Omega$ es multiplicativo:
   $\Omega_{(A\cup B)}=\Omega_{A}\cdot \Omega_{B}$
	   Ejemplo: Tener dos dados:
	   1. se tiene un 1 y en el sig pueden ser 6
	   2. se tiene un 2 y en el sig pueden ser 6
	$\vdots$
	entonces se tienen $6 \cdot 6

2. Crece rápidamente con la energía disponible del sistema.
	   Ejemplo: Cuántas cosas se pueden comprar con $2000 versus $4000 pesos: No es necesariamente el doble, si no que las posibilidades se pueden combinar

Si se tiene un sistema de $N$ átomos $\to N!$
con $m$ configuraciones equivalentes $\implies m!$
$N+m$ objetos $\to (N+m)!$

entonces:
$$
\Omega=\frac{(N+m)!}{m!N!}=\left( \begin{matrix}
N+m \\
m
\end{matrix} \right)
$$
esto corresponde a un sistema discreto. Para un sistema continuo:
***dibujjo de curva***
cada curva tiene infinitos puntos, pero también tienen **medida**, la cual varía según se tenga una línea, una superficie o volumen.


## Información faltante

### Equilibrio
Es un concepto que se asocia solamente al nivel macro, pues en el nivel micro las partículas vibran o se mueven constantemente.
	Ej: Equilibrio Mecánico
	existen puntos de equilibrio estable e inestable
	Ejs: Químico, electro y térmico.

Cuando se tienen equilibrios mecánico, químico, eléctrico y térmico, se dice que se tiene **equilibrio termodinámico**.
El equilibrio en macro no depende del tiempo, en micro sí existe variación en el tiempo.

### Axioma de Equiprobabilidad
"***En el equilibrio, todas las configuraciones accesibles son equiprobables.***"
* Si las configuraciones accesibles no son equiprobables, entonces no se está en equilibrio.
	  Ejemplo:  Tener 2 compartimientos gaseosos separados.
	  En un instante se tiene la compuerta cerrada, y se está en equilibrio
	  En otro instante se abre la compuerta y el gas se mueve (no está en equilibrio)
	  En el instante final el gas llena ambos compartimientos y se llegó a otro equilibrio.

Si las configuraciones son equiprobables, **la información faltante es máxima.**

La información faltante es una medida, que en física es denominada **Entropía**.

## Entropía

 La información que le falta a un observador que conoce el macroestado de un sistema, pero desconoce la configuración (microestado) en la que se encuentra.
Está dada por:
$$
S=k_{b}\ln \Omega
$$
se puede ver que, recordando que:  si $\Omega_{A},\Omega_{B}$ son independientes $\implies \Omega_{(A\cup B)}=\Omega_{A}\cdot \Omega_{B}$
así, para la entropía de dos sistemas $A,B$:
$$
\begin{align}
S(A\cup B)  & = k_{b}\ln(\Omega _{A\cup B}) \\
 & = k_{b}\ln(\Omega_{A}\cdot \Omega_{B}) \\
 & =S_{A}+S_{B}
\end{align}
$$
	*observaciones de clase:* 
	1. Clausius: dice que la entropía es una magnitud que determina la capacidad transformadora de un sistema.
	2. Landauer: Borrar memoria toma energía 'útil' y la disipa en forma de **calor**.

# 
Clase 11/08

Se puede obtener la entropía absoluta de un sistema, pero se va a trabajar con la variación de ella $\Delta S$, osea, para un sistema, se calcula la diferencia de configuraciones final y la inicial.
Por ejemplo, para la expansión de un gas contenido en un solo contenedor a dos:
![[Pasted image 20250815105607.png]]
si se propone que, para 1 molécula, $\Omega_{1} \propto V$, así:
$$
\begin{align}
\Omega_{1}=k\cdot V \\
\Omega_{2}=k\cdot V \\
\vdots \\
\Omega_{n}=\Omega
\end{align}
$$
así, iniclal $\Omega_{i}=(k\cdot V)^{n}$ y final $\Omega_{f}=(k\cdot V)^{n}$, entonces:
$$
\begin{align}
 & \Delta S=k\cdot \ln(\Omega_{f})-k\cdot \ln(\Omega_{i})=k\cdot \ln\left( \frac{\Omega_{f}}{\Omega_{i}} \right) \\
\iff & \Delta S=k\cdot \ln\left( \frac{V_{f}}{V_{i}} \right)^{n}=nk\cdot \ln\left( \frac{V_{f}}{V_{i}} \right) \\
\text{si suponemos que: }V_{f}=,N=N_{A}: &  \Delta S=N_{A}k\ln(2) \\
\text{si } k=\frac{R}{N_{A}}\implies & \Delta S_{mol}=R\ln (2) \\
 & \Delta S_{mol}=5,8 \left[ \frac{J}{K\cdot mol} \right]
\end{align}
$$

La entropía se conoce coloquialmente como el ´desorden' de un sistema, pero es más formal decir que hay más entropía en un sistema cuando la cantidad de configuraciones posibles es muy alta para el sistema.

## Sistema
***def: Sistema***
Es una región acotada del espacio bajo estudio.
- Se denota con $\partial V$ como el contorno del sistema $V$.

## Medio
***def: Medio***
Es el conjunto de todos los otros sistemas que interactúan con un sistema determinado.

## Universo Local
***def: Universo local***
El universo local es la unión del sistema con el medio. Por construcción, es un sistema.

## Estado
Es la condición o caracterización se un sistema mediante las medidas $E,P,N,M,T,S$.
- Si el sistema no está en equilibrio, los números son dependientes del tiempo.

## Proceso
Es la transición de un sistema desde un estado a otro (inicial a final), mediante estados intermedios.

![[Pasted image 20250815183503.png]]

Dados dos estados, hay un número indeterminado de procesos diferentes que conectan el mismo estado inicial con el mismo final.
La fuerza y torque no son variables de estado, sino que se consideran como flujos de momento y momento angular, respectivamente.
	Ejemplo:
	micro: masa, posición, momento lineal
	macro: presión, energía, masa

## Sistema Aislado
Es un sistema que cuya interacción con otros sistemas es menor de lo que se puede medir.
- El universo local es un sistema aislado.

## Ligadura
Es una restricción que le impide evolucionar a un sistema.
	Ejemplo: Evitar la expansión libre de un gas con una llave entremedio de dos contenedores.
- Relajar una ligadura desencadena un proceso.
- Casi todo proceso puede ser interpretado como **la relajación de una ligadura.**
- Cuando se relaja una restricción **se están agregando posibles configuraciones del sistema.**
Así, al relajar la restricción:
$$
\Omega_{f}=\Omega_{i}+\text{Config. adicionales}
$$
de donde
$$
\begin{align}
\Omega_{f}\geq \Omega_{i} \\
\therefore S_{f}\geq S_{i}
\end{align}
$$
La entropía $S$ puede ser igual ($\Delta S=0$) si el proceso desencadenado es trivial, osea que no hay efecto.
## II° Ley de Termodinámica
**AXIOMA:** ***En un sistema aislado, la entropía nunca decrece***, o bien, la entropía del universo local nunca decrece.
- No es correcto decir que la entropía siempre crece, sino que la entropía de un sistema no decrece.
- No es correcto decir que la entropía nunca puede disminir, sino que la entropía *de un sistema aislado* no disminuye. Pero la entropía de un sistema que interactúa con el medio sí puede disminuir.
	Ejemplo: comprimir un gas con un émbolo, o los seres vivos.

## Reversibilidad
En un sistema aislado, un proceso es reversible es reversible si el sistema puede retornar por sí mismo al estado anterior.
- Sólo tiene sentido **macroscópico**, los processos microscópicos son inherentemente reversibles.
	Ejemplo: La expansión de una partícula gaseosa desde un contenedor a otro, sí es posible que ésta vuelva a su contenedor original.

## Irreversibilidad y probabilidad de retorno
Para tener probabilidad de retorno: 
$$
\frac{\text{casos favorables}}{\text{casos posibles}}
$$
$$
=\frac{\Omega_{1}}{\Omega_{2}}\leq 1 \text{ siempre y, en general } \ll 1
$$
***
Clase 18/08
# Segunda Ley: Sistema No Aislado

En el caso de un sistema no aislado, este interactúa con el medio. Y juntos conforman el universo local, el cual corresponde a un sistema aislado, gráficamente:
![[Pasted image 20250819111513.png]]
si el universo es un sistema aislado, se le aplica la segunda ley de la termodinámica: La entropía no decrece,
$$
S_{U_{f}}\geq S_{U_{0}}
$$
además, por la razón de ser sistema aislado cumple que:
$$
\begin{align}
 & S_{u_{i}}=S_{sist_{i}}+S_{medio_{i}} \\
\text{si } & S_{U_{f}}\geq S_{U_{0}}: \\
\implies & S_{sist_{f}}+S_{medio_{f}}\geq S_{sist_{0}}+S_{medio_{0}} 
\end{align}
$$
el sistema no es aislado ya que interactúa con el medio, esto provoca que el sistema puede ir de un estado de mayor entropía a uno de menor entropía, osea:
$$
S_{sist_{f}}\leq S_{sist_{0}}\iff S_{sist_{f}}=S_{sist_{0}} - \Delta S
$$
entonces se tiene que:
$$
\begin{align}
\text{si } & S_{sist_{f}}+S_{medio_{f}}\geq S_{sist_{0}}+S_{medio_{0}} \\
\iff & S_{medio_{f}} \geq S_{sist_{0}}+S_{medio_{0}}-S_{sist_{f}} \\
\text{si } S_{sist_{f}}=S_{sist_{0}}-\Delta S: \\
\implies & S_{medio_{f}}=S_{sist_{0}}+S_{medio_{0}}-(S_{sist_{0}}-\Delta S) \\
\iff & S_{medio_{f}}=S_{sist_{0}}+S_{medio_{0}}-S_{sist_{0}}+\Delta S \\
\iff & S_{medio_{f}}=S_{medio_{0}}+\Delta S
\end{align}
$$
Esto se puede interpretar como que, si el sistema disminuye su entropía, entonces la entropía del medio aumentará.
> No se puede limpiar algo sin ensuciar otra cosa y es posible ensuciar todo sin limpiar.

## Sentido del tiempo

Los sistemas microscópicos son descritos por leyes simétricas temporalmente: El sistema puede ir desde un primer estado a un segundo estado y viceversa. En cuanto a sistemas con muchas partículas (nivel macroscópico) la experiencia nos dice que la simetría temporal no sucede, si no que *el tiempo siempre fluye en una dirección: del pasado al futuro, y no al revés.*
El problema al asignar estado final e inicial viene de que un sistema puede interactuar con el medio, pudiendo disminuir su entropía.

### El Tiempo en Sistema Microscópico
Para un sistema microscópico, se puede considerar un sistema microscópico aislado compuesto por una partícula gaseosa confinada en un contenedor dividido por un tabique en dos cámaras, teniendo así la expansión libre de la partícula en una de las dos cámaras:
![[Pasted image 20250823132806.png]]
El tabique actúa como una [[#Ligadura|ligadura]], y ,en un instante de tiempo, se **relaja** dicha ligadura provocando que la partícula pueda moverse libremente por todo el contenedor:
![[Pasted image 20250823132943.png]]
un observador de sólamente la última situación, no puede determinar cuál de las dos situaciones fue primero que la otra: Si comenzó en la derecha o la izquierda para moverse a la otra posición, así, para el observador: ***ambas situaciones son igual de posibles y entonces equiprobables*** con probabilidad $P=\frac{1}{2}$.

¿Se puede determinar el orden de las situaciones con las leyes de Newton? las leyes de newton establecen que:
$$
\begin{align}
\vec{F}= & m\vec{a} \\
\vec{F}= & m\frac{d^{2}\vec{x}}{dt^{2}} \\
\vec{F}= & m \frac{d\vec{v}}{dt}
\end{align}
$$
en la velocidad $\vec{v}=\frac{d\vec{v}}{dt}$ reemplazando el tiempo $t'$ como $-t$:
$$
\begin{align}
\vec{v}'= & \frac{d\vec{v}'}{dt'}=-\frac{d\vec{v}}{dt} \\
\iff & \vec{v}'=-\vec{v}
\end{align}
$$
osea se invierte la velocidad cuando el tiempo es negativo, dicho de otro modo, cuando el tiempo va en reversa, la velocidad va 'hacia atrás' viéndose como el efecto de rebobinar una película.
Ahora, viendo qué le sucede a la aceleración si se reemplaza el tiempo por uno negativo $t'=-t$:

$$
\begin{align}
\vec{a}'= & \frac{d\vec{v}'}{dt'} \\
\iff\vec{a}'= & \frac{d(-\vec{v}')}{d(-t)} \\
\iff\vec{a}'= & -\frac{d(-\vec{v})}{dt} \\
\iff \vec{a}'= & \frac{d\vec{v}}{dt} \\
\iff \vec{a}'=\vec{a}
\end{align}
$$
la aceleración no se invierte, osea que la tasa en la que crece la velocidad (en módulo) es la misma, así la fuerza queda igual:
$$
\vec{F}'= m\vec{a}'=m\vec{a}=\vec{F}
$$
por lo tanto las leyes de newton no distinguen entre futuro y pasado y son invertibles en términos temporales.
> Para sistemas microscópicos (de pocas partículas) no es posible determinar cuál es el orden temporal de sucesos.

### El Tiempo en Sistema Macroscópico
Si se tiene la misma situación anterior pero con una mayor cantidad de partículas:
![[Pasted image 20250823150156.png]]
se muestran dos situaciones y se tiene una mayor intuición en cuanto a la temporalidad de sucesos: Se puede afirmar que la situación en donde las partículas están confinadas a la izquierda (luego de relajar la ligadura) es anterior a la situación en donde las partículas están repartidas por el contenedor.
Considerando un gas con una cantidad de partículas de $\approx 10^{20}$:
![[Pasted image 20250823150721.png]]
se puede intuir que, luego de relajar la ligadura, el gas comenzará a expandirse por todo el contenedor. Así, es fácil decir cuál es el estado anterior y posterior del gas, ya que es muy poco probable que el gas se comprima de vuelta a la cámara en donde estaba confinado, por mucho tiempo que pase.
Utilizando la física mecánica para la i-ésima partícula de las $N$ partículas que componen el gas, en la 2° Ley de Newton:
$$
\begin{align}
\vec{F}_{i}= & m_{i}\vec{a}_{i} \\
\text{si }\vec{a}_{i}=\frac{d\vec{v}}{dt}=\frac{d^{2}x_{i}}{dt^{2}}
\end{align}
$$
tiene las mismas propiedades que para una partícula, ya que se está haciendo el cálculo para cada partícula singularmente. Por lo tanto, para la física mecánica, un sistema compuesto de muchas partículas también es reversible. Pero esto contradice a la experiencia cotidiana.

#### Distribución Binomial
La física mecánica es determinista: Dado un estado inicial, se puede conocer siempre el estado final, dado por la leyes de Newton. Pero en la realidad el estado inicial de un sistema nunca es completamente determinado: Existen errores experimentales y también la **predicibilidad** del sistema, esto es, dados dos estados iniciales próximos, ello no garantiza que los estados finales lo sean. Condiciones iniciales con una pequeña diferencia pueden llevar a estados finales radicalmente diferentes.
Luego, cabe preguntarse: Dado el estado inicial aproximado de un sistema, ¿Cuál es la *probabilidad* de encontrarlo en un estado final determinado, después de un largo intervalo de tiempo? Para simplificar, se toma el ejemplo del gas ideal compuesto de varias partículas, en donde el estado final de las partículas es estar en la cámara de la derecha o de la izquierda, sin importar la posición exacta de ellas:
Considerando un total de $N$ partículas y que, si en una cámara hay $m$ partículas entonces hay $m!$ maneras de ordenarlas en su cámara, y para la cámara restante, hay $(N-m)!$ maneras de que estén las partículas en su interior. Luego, la manera en que las partículas pueden estar repartidas en el contenedor está dada por una combinación de ellas: $\frac{N!}{m!(N-m)!}$ maneras de que estén las partículas en el interior.
Para una cámara, y para cada partícula hay sólo dos posibilidades: Que esté en ella o que no esté, así la probabilidad para cada partícula es de $\frac{1}{2}$, así la probabilidad de estar, para cada cámara es:
$$
\frac{1}{2}\cdot \frac{1}{2}\cdot \frac{1}{2}\dots N \text{ veces} \implies =\left( \frac{1}{2} \right)^{N} 
$$
y para cada manera de repartir las $N$ partículas, se tiene entonces las probabilidades de que hayan $m$ a un lado y $m-n$ en el otro:
$$
P_{N}[m]=\frac{N!}{m!(N-m)!}\cdot \frac{1}{2^{N}}
$$
que se denomina la distribución binomial de probabilidades.


# Sistemas Modelos
Un gas real está compuesto por $n$ partículas iguales y puntuales, por lo que no tienen volumen y no chocan entre ellas.
Si las partículas no interactúan entre ellas entonces sus posiciones no alteran sus energías, así las posibles configuraciones del sistema es tal que:
$$
\Omega(x\text{ y vel})=\Omega(x)·\Omega(vel)
$$
## Omega como Medida Bidimensional
Si se tiene una circunferencia 
![[Pasted image 20250825162137.png]]
donde $\Omega$ es el perímetro, entonces
$$
\Omega=2\pi R
$$
y para tres dimensiones: $x^{2}+y^{2}+z^{2}=R^{2}$ donde $\Omega$ es el perímetro, entonces:
$$
\Omega=4\pi R^{2}
$$
y en cuatro dimensiones:
$$
\Omega=k·R^{4-1}
$$
Luego, para un gas ideal de N-dimensiones:
$$
\Omega=k·R^{N-1}
$$
en donde la energía esta dada por la suma de la energía cinética de todas las partículas:
$$
E=\sum_{i=1}^{n} \frac{1}{2}m\vec{v}_{i}^{2}
$$
si $\vec{v}_{1}=(v_{x_{1}},v_{y_{1}},v_{z_{1}})\implies n=3N\text{ terminos}$ y $\Omega=\Omega_{pos}·\Omega_{vel}=cte·V^{N}·E^{\frac{3N}{2}}$
Si $S=k\ln \Omega=cte''+Nk\ln V+\frac{3Nk}{2}\ln E$ y sean estados de referencia $V_{0},E_{0}$ de entropía $S_{0}$:
$$
\begin{align}
 & S_{0}=cte''+Nk\ln V_{0}+\frac{3Nk}{2}\ln E_{0} \\
\implies & S-S_{0}=Nk\ln\left( \frac{V}{V_{0}} \right)+\frac{3}{2}Nk\ln\left( \frac{E}{E_{0}} \right)
\end{align}
$$
# Procesos
1. Reversibles (Isentrópicos): Es una sucesión ordenada de estados de equilibrio de igual entropía. Son isentrópicos pues para ser reversibles no deben crear entropía.
2. Cuasiestáticos: Sucesión ordenada de estados de equilbrio.
3. Real: Sucesión ordenada temporal de estados de equilbrio y de no equilibrio.

Real -> No cuasiestático -> Irreversible


***
# 22/08
# Trabajo Macroscópico

Se va a llamar trabajo $\mathbb{W}$ al trabajo realizado por **el medio sobre el sistema**. Así, lo que entra al sistema es positivo, y se denota al trabajo realizado por el sistema como $\mathbb{W}'=-\mathbb{W}$
Para un proceso muy próximo al otro (infinitesimalmente) se va a denotar con $w$ (minúscula)
![[Pasted image 20250825163619.png]]
se sabe ya que el trabajo está dado por:
$$
\mathbb{W}=\vec{F}·d\vec{s}
$$

## Trabajo Volumétrico
Es el trabajo en el cual el sistema cambia su volumen por un agente externo.
	Ejemplo: Gas confinado en una cámara que se contrae por la fuerza aplicada con un émbolo.

$w=\vec{F}d\vec{x}$, si $F=\rho A\implies w=\rho Ad\vec{x}$ y la variación de volumen es $|dV|=A|dx|$.
Si se comprimió: $dV<0\implies d=-Adx \implies w=-PdV$ y el signo se opone a la compresión.
Deben estar en equilibrio el medio y el sistema ($P_{medio}=P_{sist}=P$) sino, no se puede usar fórmula.

## Trabajo Extendido
Requiere especificar el camino $\mathcal{C}$ recorrido. En general, el trabajo realizado por un camino es diferente al realizado por otro camino distinto y no son conservativos (en general).
> Un camino es sinónimo de curva y éstos representan a un proceso.
![[Pasted image 20250825164353.png]]
entonces:
$$
\mathbb{W}_{\mathcal{C}}=\int_{i}^{f}-PdV,\ \mathbb{W}_{\mathcal{C}'}=\int_{i}^{f}-PdV
$$
*obs:* $w$ no es variable de estado, osea no depende del estado del sistema (en otras palabras: El sistema no 'posee' trabajo en un estado)

##### Ejemplo: Ciclo Cuadrado
Cuál es el $\mathbb{W}$?
![[Pasted image 20250825164910.png]]
*obs:* Proceso en donde no varía presión: Expansión/Compresión isobárica.
1. Construir tabla de vértices (columnas = variables, filas = puntos del gráfico).
2. Ingresar datos en celda correspondiente.
3. Construir tabla con columnas como el valor que se pide y filas como los procesos (e.g. 1->2).

El área entre las curvas es el trabajo realizado por el camino cerrado, ya que el trabajo es el área bajo una curva. Si se calcula el de una curva y luego se suma con la complementaria, se restarán las áreas (por uno de esos caminos devolverse).

### Trabajo Eléctrico
Existen otros tipos de trabajo, como el trabajo eléctrico dado por un flujo de cargas y la carga:
$$
\mathbb{W}=\phi d\Theta
$$


# 1° Ley de la Termodinámica: Conservación de la Energía
Es un axioma: No se demuestra, pero la historia en datos empíricos lo a
vala. Y se basa en la información física recolectada.
Es  posible enunciarla como:
- En un sistema aislado la energía se conserva
- La energía del universo local es constante
- La energía no se crea ni se destruye
- El incremento de energía en un sistema es igual a:
  1. La energía que ingresa
  2. Menos la que sale
  3. a través de la superficie del sistema

### Calor
Provisionalmente, es energía transferida cuando no es está realizando trabajo sobre el sistema, así:
$$
dA,dV,d\Theta = 0
$$
El calor es una transferencia de energía asociada a una transferencia de entropía.

*obs:* El calor no es variable de estado (un sistema no lo posee)

## Expresión 1° Ley
Así, la primera ley de la termodinámica se puede expresar como:
$$
\begin{align}
 & dE_{A}=q_{A}+w_{A} \\
 & dE_{B}=q_{B}+w_{B} \\
dE_{U}=0 &  \\
 & \iff dE_{U}=dE_{A}+dE_{B} \\
 & \iff dE_{U}=(q_{A}+q_{B})+(w_{A}+w_{B})
\end{align}
$$
si $w_{A}=-w_{B}$ el trabajo que ejerce A sobre B es igual al opuesto que ejerce B sobre A:
$$
\implies q_{B}=q_{A}
$$


***
# 25/08
### Teoría del Calórico
Explicación hecha por Lavoisier: El calórico es una sustancia que se transmite de un cuerpo a otro.
Experimento de rumford:
- 1er exp: Botella con agua fria y caliente pesan lo mismo
- 2° Exp: Taladrar cañón produce virutas que no conservan el calórico
	- No hay otra fuente de calor que la fricción de los golpes: El trabajo puede 'convertirse' en calor.

### Joule
Aún en el siglo, se pensaba que trabajo y calor eran independientes.

James Prescott Joule, s.XIX: 
Muestra que trabajo y calor son ambas energías y que había alguna relación entre ellas.
Experimento:
- Cilindro con agua aislado con lana.
- Paletas fijas dentro del cilindro (estatores) y un eje veritcal conectado a paletas móviles
- Un termómetro
- Una masa cuelga afuera y al subir y bajar, subía la temperatura del agua en el interior. Mientras mayor masa, más subía la temperatura.

# Trabajo y Calor
El **trabajo** esta asociado a la transferencia de energía por medio de magnitudes macroscópicas (visibles)
El **calor** es la transferencia de energía a través de variables microscópicas en forma de vibraciones atómicas, por lo que se puede relacionar con los microestados.

Si se tienen dos sistemas aislados entre sí de forma que no se pueden ejercer trabajo el uno al otro,  el sistema que contiene mayor energía la transfiere a otro de baja energía a través de calor.

## Propiedades del Calor
1. El calor al i-ésimo sistema se denota como $Q_{i}$
2. Empiricamente, se cumple que $Q_{A}+Q_{B}=0\iff Q_{A}=-Q_{B}$, osea se cumple la ley de la conservación de la energía.
3. El calor no se asocia a la transferencia de una magnitud extensiva visible.
   Se postula: $E_{q}-E_{i}=Q+\mathbb{W}$

## Transferencia Cuasiestática de Energía
Si se tiene un universo local B y el sistema A dentro de él.
La transferencia es cuasiestática si la frontera entre el medio y el sistema se encuentra en equilibrio dentro de la precisión experimental que se tenga.

* Diferencia entre cuasiestático y real:
poca fuerza en émbolo mantiene la presión estable
golpe provoca ondas

La *interacción* es cuasiestática cuando la frontera está en equiilibrio.
Un *proceso* es cuasiestático si todos los estados intermedios son de equilibrio.

## Trabajos

Siempre se puede expresar el trabajo como la transferencia de una magnitud ext multiplicada por otra magnitud extensiva que no depende del tamaño del sistema.
> El trabajo siempre se puede expresar como transferencia.

### Tensión Superficial
Se origina en la interacción de las moléculas en la superficie de un líquido: Las moléculas en el interior interactúan con moléculas en todo su alrededor, mientras que las superficiales sólo con las inferiores, minimizando el área del líquido.
> Es necesario realizar un trabajo para inflar una burbuja de jabón 

Si se tiene una superficie un poco profunda y abierta en uno de sus lados, se puede ampliar la superficie del líquido:
![[Pasted image 20250825174650.png]]
Si se busca aumentar el área:
$$
dA=2L\ dx
$$
el '2' ya que, si se mira transversalmente, se aprecian dos capas (aunque minimamente separadas) asi que se debe calcular el aumento para ambas caras superior e inferior.
Si se necesita aplicar una fuerza F y ésta tiene un trabajo asociado:
$$
\begin{align}
 & w_{A}=F dx \\
\text{si }dx=\frac{dA}{2L} \implies & w_{A}=F\frac{dA}{2L}\\
\end{align}
$$
#### Definición
Si se define la tensión superficial $\alpha$ como:
$$
\alpha=\frac{F}{2L}
$$
si $2L=L_{tot}$ es el largo total del borde dela película, entonces
$$
\alpha=\frac{F}{L_{tot}}
$$
por lo tanto:
> **La tensión superficial se puede interpretar como fuerza por unidad de longitud**,

La tensión superficial tiene unidades de $\frac{N}{m}$, pero se mide en $\frac{J}{m^{2}}$ comúnmente:
> La tensión superficial también se puede ver como *la energía necesaria para incrementar el área de un sistema*.

 Y el trabajo ejercido por el medio sobre la película para expandir la película es:
$$
\mathbb{W}_{A}=\alpha\ dA
$$

- como la tensión superficial $\alpha>0\implies \mathbb{W}_{A}>0$ osea, el medio le ejerce un trabajo a la película, minimizando su área
- La tensión superficial es una función de la temperatura y se anula en la temperatura crítica.
# Ecuación Fundamental
Se denomina ecuación fundamental de un sistema a la ecuación que relaciona todas sus magnitudes extensivas, osea, es una función de la forma:
$$
F(E,x_{1},x_{2},\dots,x_{n)})=0
$$
permitiendo así expresar una magnitud extensiva en función de todas la demás. Esta ecuación contiene toda la información de los estados de equilibrio del sistema.
No siempre se tiene y se puede tratar de construir con mediciones experimentales y un formalismo.
## Ecuación Fundamental en la Representación de Energía
Si se elige expresar la energía en términos de las demás, la función de la forma:
$$
E=E(x_{1},x_{2},\dots,x_{n})
$$
se denomina *ecuación fundamental en la representación de energía* y se usa habitualmente en termodinámica.
# Magnitud
Una **magnitud** es una propiedad de un sistema que puede ser expresada cuantitativamente. En termodinámica se pueden clasificar en dos grupos: Magnitudes Extensivas y Magnitudes Intensivas.
## Magnitudes Extensivas
Se denotan con $X$ (mayúscula) y se pueden reconocer como similares a la masa. Estas *existen* o *hay* en el sistema, osea, **están contenidas en el sistema**. Entonces es posible establecer su localización espacial en el interior de una superficie cerrada

1. Están contenidas en un sistema
2. Son aditivas
3. Tienen densidad
4. Se pueden transferir
Ej: Masa, Energía, Entropía, Volumen y Dimensiones (se aceptan).

> Un estado de equilibrio está completamente determinado por los valores de las magnitudes extensivas

Cualquier interacción entre el medio del sistema se puede interpretar como una transferencia de magnitudes extensivas.
Una relación entre magnitudes extensivas tiene toda la información entre estados de equilibrio:
sean $X_{1},X_{2},\dots X_{n}$ magnitudes extensivas, se puede expresar una magnitud extensiva como una función que depende de las otras:
$$
F(X_{1},X_{2},\dots,X_{n)})=0
$$
es la relación fundamental.
	Ejemplo: Gas ideal:
	1. Para monoatómico: $S-S_{0}=Nk\ln\left( \frac{V}{V_{0}} \right)+\frac{3}{2}Nk\ln\left( \frac{E}{E_{0}} \right)$

Si se sabe la relación fundamental, se puede saber el estado del sistema.

*** 
# 
Clase

Por qué se conserva la energía?

Hay simetría de las leyes físicas:
1. Invariancia ante traslaciones (
2. Invariancia ante rotaciones
3. Invariancia temporal: Son siempre las mismas

¿Se conserva la energía?
Haciendo un experimento pensado de dos objetos  de $\frac{M}{2}$ de masa que van a chocar a una velocidad $V_{0}$ en sentidos opuestos:
La energía cinética entre ellas es la misma
Luego del choque se mantienen juntas con velocidad 0, la energía se esfumó?

Si se vé microscópicamente, se vé una grilla de partículas unidas por resortes, moviéndose con la misma velocidad y cada una sumando a la energía cinética del objeto.
Después del choque, las partículas se moverán aleatoriamente y vibran en torno al equilibrio. Osea la energía pasó a estar almacenada en vibraciones microscópicas.
- El proceso es irreversible pues la probabilidad de que las partículas vuelvan a moverse todas en la misma dirección para mover el objeto total, es mínima. Entonces el proceso es irreversile

# Temperatura Absoluta

Notación:
$$
\left( \frac{\partial F}{\partial x} \right) _{y}=\frac{\partial}{\partial x}F(x,y)
$$
la temperatura sale luego de combinar la primera y segunda ley
2° En un sist aislado no decrece la entropóa
1° la en. en un sist aislado es constante
0° dos sistemas en equilibrio térmico están a la **misma temperatura**

dos gases y en medio un émbolo están en eq si las presiones son iguales.
Si se considera un sistema:
- con dos cámaras recubiertas por una pared aislante térmica (pared adiabática),
- un metal conductor (pared diatérmica) que separa dos fluidos,
se llegará a equilibrio térmico (estado final en donde no hay más flujo térmico de un lado a otro)
Entonces, si en el equilibrio, los dos sistemas deben compartir una propiedad, esa propiedad se define como *temperatura* 

Considerando el sistema anterior:
la 1° ley dice que $E_{A}+E_{B}=E_{0}=cte$, pero no determina cuánta energía en específico
la ley 2 dice que la entropía nunca decrece, por lo tanto va a crecer en el tiempo hasta llegar a un máximo.
Entonces, cómo se puede determinar el equilibrio? 
Si en equilibrio: 
$$
\begin{align}
 & dS_{U}=0 \\
\iff & dS_{A}+dS_{B}=0 \\
\text{si }S_{A}=S_{A}(E_{A},V_{A}) & \text{ con }V_{A}=cte
\end{align}
$$

$$
\left( \frac{\partial S}{\partial E} \right)_{V} |_{A}= \left( \frac{\partial S}{\partial E} \right)_{V} |_{B}
$$
se define entonces:
$$
\frac{1}{T}=\left( \frac{\partial S}{\partial E} \right)_{V}
$$


- la unidad es el kelvin $K$
- la temperatura absoluta es no negativa $T\geq 0$, ya que $\=Omega$ crece con la energía $E$ luego $S$ crece con $E$, entonces $\frac{\partial S}{\partial E}\geq 0$

*def:* El sistema más caliente es el que cede energía (calor) en una interacción térmica.
Osea, el sistema más caliente está a mayor temperatura.

*dem:* sistema B está más caliente
Considerando un sistema justo en el punto anterior a estar en equilibrio, y pared rígida (vol. cte)
$$
\begin{align}
dS=\left( \frac{\partial S}{\partial E} \right)_{A}dE_{1}+\left( \frac{\partial S}{\partial E} \right)_{B}dE_{B} \\
dS=\frac{1}{T_{A}}dE_{A}+\frac{1}{T_{B}}dE_{B}>0 \\
dE_{A}=q_{A}+w_{A},\ w_{A}=0 \text{ por } dV=0 \\
\text{e igual para B} \\
dE_{U}=0=dE_{A}+dE_{B}=q_{A}+q_{B} \\
dS=\frac{q_{A}}{T_{A}}+\frac{q_{B}}{T_{B}}>0 \\
\frac{q_{A}}{T_{A}}+ -\frac{q_{A}}{T_{B}}>0 \\
\frac{1}{T_{A}}-\frac{1}{T_{B}}>0 \\
\iff \frac{1}{T_{A}}> \frac{1}{T_{B}} \\
\iff T_{B}> T_{A}
\end{align}
$$

Cómo se mide la temperatura con termómetros

termómetro mide el volumen de un líquido.
Si a $P=cte,\;V=V(T)$ haciendo taylor alrededor de $T_{0}$:
$$
V\approx V(T_{0})+ \frac{dv}{dT}|_{0} (T-T_{0}) + \frac{1}{2} \frac{d^{2}V}{dT^{2}}|_{0} (T-T_{0})^{2} +\dots
$$
así en la mayoría de los casos:
$$
V\approx V(T_{0})+ \frac{dV}{dT}|_{0}\;(T-T_{0})
$$
