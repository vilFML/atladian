
$$
f(x,y)
$$
- [ ] pasar en blanco pol. de taylor catedra

$$
df=\left( \frac{ \partial f }{ \partial x }  \right) _{y}dx+\left( \frac{ \partial f }{ \partial y } _{x} \right) dy
$$
otro razonamiento:



# Estados próximos conectados por un proceso reversible



*** 
# 22-09

## Máquina Térmica
La fuente de energía es una fuente térmica.

> Se 'quema' algo

Puede convertirse el 100% del calor en trabajo? No. Pues la temperatura está relacionado con el movimiento o vibración de las partículas **de forma aleatoria**, pero el movimiento q se busca hacer no es aleatorio, si no que se quiere ir en algún sentido definido. 
Hay una convención de la transformación.

### Suponiendo funcionamiento reversible:
***
***

si $\Delta E_{ciclo}=Q+\mathbb{W}=0$ y se quiere que sea un motor: $W'>0\iff \mathbb{W}<0 \implies Q>0$

entonces $\Delta S=\frac{Q}{T_{2}}=0 \implies Q=0\implies \mathbb{W}=0$

### caso irreversible
se tienen $\delta s_{irr}$ entropía generada por procesos irreversibles en el interior de la máquina.


# II° Ley según Kelvin-Plank

No es posible un proceso cíclico cuyo único resultado sea la "extracción de calor" de una única fuente y la realización de una cantidad equivalente de trabajo.

*interpretación estadística*
Es estadísticamente imposible que las vibraciones aleatorias se organicen para generar un único desplazamiento macroscopico.

Sí es posible realizar trabajo generando solo calor.

El problem surge del hecho que cerrar el ciclo requiere ceder la entropía (recibida y generada) a otro sistema.}}


# Límite de carnot
Es un llímite físico que depende solamente de las temperaturas de las fuentes, no depende del diseño de la máquina.
- Se aplica sólamente a máquinas térmicas.
- No es predictivo, los rendimientos reales son mucho menores y es prohibitivo: El rendimiento real nunca va a alcanzar $\eta_{carnot}$


# Enunciado II° Ley: Kelvin
+ No todo el calor proveniente de una fuente puede usarse para realizar trabajo; sino que parte de ese calor deberá cederse a una fuente a menor temperatura.
O también: 
+ Todo proceso de la naturaleza por el cual se transforma calor procedente de un foco caliente en trabajo mecánico requiere la cesión de una parte del calor absorbido a un foco frío.


# Máquina Frigorífica
Es una máquina térmica al revés (refrigerador)

Se extrae el calor de la fuente fría y se lleva hacia la fuente caliente (atmósfera)

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

# Eficiencia
$$
E= \frac{\text{beneficio}}{\text{costo}}= \frac{Q_{1}}{\mathbb{W}}
$$
si de beneficio o utilidad se busca enfriar, entonces corresponde al calor que se extrae de la fuente fría $Q_{1}$ y el costo es el trabajo realizado $\mathbb{W}$

$$
E = \frac{1}{\frac{T_{2}}{T_{1}}-1}
$$
# Enunciados IIa ley: Clausius -Clapeyron

El calor no pasa de manera espontánea de un cuerpo de menor temperatura a uno de mayor.

# ejemplo

El rendimiento y eficiencia son conceptos diferentes, así no necesariamente se relacionan el valor número obtenidos para los casos de calentar o enfriar. 


# Bomba Térmica (o Bomba de Calor)
