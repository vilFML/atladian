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



