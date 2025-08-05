04/08, Clase 1: Introducción

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
   