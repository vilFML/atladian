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


***
# 22/08

