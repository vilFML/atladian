# Máquinas

*nomenclatura:*
1. **[[Motor]]:** Sistema que realiza trabajo mecánico.
   - Para el estudio de máquinas interesa el trabajo $\mathbb{W}'$ que la máquina ejerce sobre el medio.
   - Se cumple que: $\mathbb{W}'=-\mathbb{W}_{\text{sist}}$.
   - El motor ejerce un trabajo al medio y $\mathbb{W}'<0$, que se interpreta como que el sistema (la máquina) pierde energía.
1. Máquina frigorífica o refrigerador: Máquina que enfría un recinto.
2. Generador: Máquina que entrega corriente eléctrica.
3. Estufa: Máquina que sólo calienta.


Una máquina es cíclica cuando vuelve al estado inicial:
$$
\begin{align}
\Delta E_{\text{ciclo}}=0 \\
\Delta S_{\text{ciclo}}=0
\end{align}
$$
pero el estado final del medio **no es igual a su estado inicial:**
Si por conservación de energía se cumple que: $\Delta E_{\text{medio}}=0$, la entropía del medio no disminuye: $\Delta S_{\text{medio}}\geq 0$

## Máquina Térmica
Cuando la fuente de energía es una fuente térmica. (Se 'quema' algo).

No es posible convertir la totalidad de calor en trabajo, pues la temperatura está relacionada con el movimiento o vibración de las partículas **de forma aleatoria**. El aumento de temperatura implica un movimiento aleatorio de las partículas, pero para ejercer un trabajo se requiere realizar un movimiento en una dirección bien definida, lo que es de extremadamente baja probabilidad. 

### Funcionamiento Reversible:
Si se tiene una máquina con una fuente térmica $T_{2}$ que transfiere un calor $Q$ a la máquina, y ella realiza un trabajo $\mathbb{W}'$
![[Pasted image 20251003201117.png]]

Suponiendo un funcionamiento reversible:
$$
\begin{align} \\
\Delta E_{\text{ciclo}} & =0 \\
\Delta E_{\text{ciclo}} & =Q+\mathbb{W}
\end{align}
$$
y se quiere que la máquina sea un motor (ejerza un trabajo), o sea:
$$
\mathbb{W}'> 0
$$
y el trabajo del medio es negativo: $\mathbb{W}<0$, lo que, para mantener la diferencia de energía en 0, se necesita que el medio ceda calor: $Q>0$

entonces la diferencia de entropía queda: $\Delta S=\frac{Q}{T_{2}}=0$
entonces el calor $Q=0$ y el trabajo $\mathbb{W}=0$
O sea, se genera una **contradicción.**


### Funcionamiento Irreversible
Se deben consideran los procesos irreversibles en el interior de la máquina, que tienen una entropía$\delta s_{irr}$ asociada.
La entropía de los procesos irreversibles es positiva: $\delta s_{irr}>0$
entonces, si se tuviese un funcionamiento reversible: $\Delta S=0$. Luego, la variación de entropía para todo el sistema máquina es:
$$
\Delta S_{\text{ciclo}}=\frac{Q}{T_{2}}+\delta s_{\text{irr}}=0
$$
pero $\frac{Q}{T_{2}}>0,\ \delta s_{\text{irr}}>0$, lo que contradice el hecho de que sea reversible.

Por lo tanto, el funcionamiento de una máquina es inherentemente irreversible.

## II° Ley según Kelvin-Plank

No es posible un proceso cíclico cuyo único resultado sea la "extracción de calor" de una única fuente y la realización de una cantidad equivalente de trabajo.

*Interpretación estadística:* Es estadísticamente imposible que las vibraciones aleatorias se organicen para generar un único desplazamiento macroscopico.

Pero, sí es posible realizar trabajo generando solo calor.

El problema surge del hecho de que cerrar el ciclo requiere ceder la entropía (recibida y generada) a otro sistema.


## Límite de carnot $\eta_{\text{carnot}}$

Considerando el caso de tener una fuente y sumidero térmicos y una máquina térmica de funcionamiento reversible:
![[Pasted image 20251003205626.png]]
en donde la temperatura del sumidero $T_{1}$ es mayor a la de la fuente $T_{2}$: $T_{1}<T_{2}$ .
Si la diferencia de energía para un ciclo es 0: 
$$\Delta E_{\text{ciclo}}=0 \iff Q_{1}+Q_{2}+\mathbb{W}=0$$
entonces, para el trabajo $\mathbb{W}'$ que realiza la máquina:
$$
\begin{align}
\mathbb{W}'=-\mathbb{W} \\
-\mathbb{W}=Q_{1}+Q_{2}
\end{align}
$$
Y la diferenciad de entropía sería 0: $\Delta S_{\text{ciclo}}=0$
reescribiendo la entropía:
$$
\begin{align}
\Delta S=\frac{Q_{1}}{T_{1}}+\frac{Q_{2}}{T_{2}}=0 \\
\text{si }Q_{1}=-Q_{2} \frac{T_{1}}{T_{2}}
\end{align}
$$
donde $Q_{1}$ es la pérdida,
$$
\begin{align}
\implies & -\frac{T_{1}}{T_{2}}Q_{2}+Q_{2}+\mathbb{W}=0 \\
 & \left( 1-\frac{T_{1}}{T_{2}} \right)Q_{2}+\mathbb{W}=0
\end{align}
$$
entonces $Q_{2}>0$ que corresponde a lo que se 'paga' literalmente.

Se busca minimizar la pérdida de $Q_{1}$, eso se puede lograr con:
1. Minimizar $T_{1}$, pero se tiene un límite de alrededor de $300K$
2. Maximizar $T_{2}$, pero hay límite por materiales.
para ello se introduce el concepto de [[rendimiendo]] $\eta$ como:
$$
\eta=\frac{\text{lo que se obtiene}}{\text{lo que se paga}}=\frac{\text{beneficio}}{\text{costo}}=\frac{\mathbb{W}'}{Q_{2}}
$$
con ello se tiene el límite de carnot $\eta_{\text{carnot}}$

Es un límite físico que depende solamente de las temperaturas de las fuentes, **no depende del diseño de la máquina.**
$$
\begin{align}
 & \eta_{\text{carnot}}  =\frac{\mathbb{W}'}{Q_{2}} \\
\text{si }\mathbb{W}' =-\mathbb{W}\\
 & =-\frac{\mathbb{W}}{Q} \\

 & \eta_{\text{carnot}} =1-\frac{T_{1}}{T_{2}}
\end{align}
$$

- Se aplica solamente a máquinas térmicas.
- No es predictivo, los rendimientos reales son mucho menores
- Es prohibitivo, pues **el rendimiento real nunca va a alcanzar $\eta_{\text{carnot}}$**

##  II° Ley según Kelvin

> No todo el calor proveniente de una fuente puede usarse para realizar trabajo; sino que parte de ese calor deberá cederse a una fuente a menor temperatura.

*Equivalente*: Todo proceso de la naturaleza por el cual se transforma calor, procedente de un foco caliente, en trabajo mecánico, requiere la cesión de una parte del calor absorbido a un foco frío.


## Máquina Frigorífica
Es una máquina térmica al revés (*ej: refrigerador*). Su funcionamiento consiste en extraer el calor de la fuente fría y llevarlo hacia la fuente caliente (atmósfera).

Si por primera ley: $\Delta E_{ciclo}=Q_{1}+Q_{2}+\mathbb{W}$ 
y la entropía en un ciclo (asumiendo reversible): $\Delta S_{ciclo}=\frac{Q_{1}}{T_{1}}+\frac{Q_{2}}{T_{2}}=0$ y entonces $Q_{2}=$

Se busca analizar $Q_{1}$,
$$
\begin{align}
 & Q_{2}=-Q_{1}\cdot \frac{T_{2}}{T_{1}} \\
\implies Q_{1}\left( 1- \frac{T_{2}}{T_{1}} \right)+\mathbb{W}=0 \\
Q_{1}= -\frac{\mathbb{W}}{1- \frac{T_{2}}{T_{1}}}=\frac{\mathbb{W}}{\frac{T_{2}}{T_{1}}-1}
\end{align}
$$
y se define la **eficiencia**

### Eficiencia
$$
E= \frac{\text{beneficio}}{\text{costo}}= \frac{Q_{1}}{\mathbb{W}}
$$
si de beneficio o utilidad se busca enfriar, entonces corresponde al calor que se extrae de la fuente fría $Q_{1}$ y el costo es el trabajo realizado $\mathbb{W}$

$$
E = \frac{1}{\frac{T_{2}}{T_{1}}-1}
$$
El rendimiento y eficiencia son conceptos diferentes, así no necesariamente se relacionan el valor número obtenidos para los casos de calentar o enfriar. 

## II° Ley según Clausius-Clapeyron

> El calor no pasa de manera espontánea de un cuerpo de menor temperatura a uno de mayor.

## Bomba Térmica (o Bomba de Calor)

![[Pasted image 20251003220845.png]]

