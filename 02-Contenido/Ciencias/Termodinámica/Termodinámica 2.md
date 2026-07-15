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
![[Pasted image 20251003201117.png|200]]

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
![[Pasted image 20251003205626.png|150]]
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
para ello se introduce el concepto de [[rendimiento]] $\eta$ como:
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

Si se usa una máquina frigorífica para calentar, se cambia qué se busca maximizar.
![[Pasted image 20251003220845.png|200]]

$Q_{2}'=Q_{2}$ es el que ingresa a la habitación de temperatura $T_{2}$, luego:
$$
\begin{align}
Q_{1}+Q_{2}+\mathbb{W}=E\mathbb{W}-Q_{2}'+\mathbb{W}=0 \\
Q_{2}'=(1+E)\mathbb{W} \\
\dot{Q}_{2}=(1+E)\dot{\mathbb{W}}
\end{align}
$$
entonces
$$
\dot{Q}_{2}'=(1+E)\dot{\mathbb{W}}
$$

## Ciclo de Carnot
### Ciclo de Carnot Genérico
Para una fuente térmica $T_{2}$ y un sumidero $T_{1}$, en donde $T_{2}>T_{1}$: 
![[Pasted image 20251003223358.png|200]]
si el sistema de interés es la máquina misma, se tiene el ciclo de carnot genérico e imponiendo un proceso reversible:
![[Pasted image 20251003223558.png|200]]
La máquina realiza los siguientes procesos:
1. Toma calor a $T_{2}$: Isoterma superior
2. Enfría a $T_{1}$ (sin contacto con otros sistemas): Adiabática isentrópica.
3. Cede calor a $T_{1}$: Isoterma inferior.
4. Sube a $T_{2}$ (sin contacto con otros sistemas): adiabática isentrópica.

### Ciclo de Carnot para Gas Ideal

## Rendimiento Real
Considerando que en una máquina real los procesos son inherentemente irreversibles:
$$
\Delta S_{\text{ciclo}}=\frac{Q_{1}}{T_{1}}+\frac{Q_{2}}{T_{2}}+\delta S_{\text{irr}} \iff Q_{1}=-\left( \frac{T_{1}}{T_{2}}Q_{2}+T_{1}\delta S_{\text{irr}} \right)
$$
y $Q_{1}$ corresponde a la energía que se entrega a la fuente fría térmica fría.
Si $\mathbb{W}'=\mathbb{W}=Q_{1}+Q_{2}=Q_{2}-\left( \frac{T_{1}}{T_{2}}Q_{2}+T_{1}\delta S_{\text{irr}} \right)$, entonces el rendimiento $\eta$:
$$
\eta=\frac{\mathbb{W}'}{Q_{2}}=1-\frac{T_{1}}{T_{2}}-\frac{T_{1}\Delta S_{\text{irr}}}{Q_{2}}
$$
que corresponde al rendimiento real de la máquina:

$$
\eta_{\text{real}}=\underbrace{ 1-\frac{T_{1}}{T_{2}} }_{ \eta_{\text{carnot}} } - \underbrace{\frac{T_{1}\Delta S_{\text{irr}}}{Q_{2}} }_{ \text{Unidad de S por unidad de }Q_{2} }
$$
el rendimiento real puede llegar a ser 0, es cuyo caso, es equivalente a conectar un conductor de calor entre las fuentes.

Para minimizar $\Delta S_{\text{irr}}$ la máquina debe ser lo más cuasiestática posible, o sea estar lo más cercano al equilibrio posible: Extremadamente lento. Pero, en general, se quiere que la máquina realice el proceso relativamente rápido.

> Si se quiere más potencia, se sacrifica rendimiento.

### Comparación con Máquina Eléctrica
*Ejemplo:* Cargador con sólo 1 terminal: No hay flujo de cargas para que funcione.
> En una máquina térmica hay flujo de entropía.

Considerando el caso de una máquina eléctrica reversible: Se tienen dos fuentes de carga: 
![[Pasted image 20251003231418.png|250]]|
donde la ampolleta realiza un trabajo $\mathbb{W}'=-\mathbb{W}$.
Entra energía $d\Theta \phi_{2}$ y 'bota' energía $d\Theta \phi_{1}$.
Por conservación de energía:
$$
\mathbb{W}'=(\phi_{2}-\phi_{1})d\Theta
$$
y el rendimiento será:
$$
\eta_{\text{elec}}=\frac{\text{beneficio}}{\text{costo}}=\frac{(\phi_{2}-\phi_{1})d\Theta}{\phi_{2}d\Theta}\iff \eta_{\text{elec}}=1- \frac{\phi_{1}}{\phi_{2}}
$$
para un enchufe: $\phi_{1}=0,\ \phi_{2}=220[V_{\text{RMS}}]$, entonces el rendimiento $\eta_{\text{elec}}=1$. En la realidad $\phi_{1}\approx 3$, pero el rendimiento sigue siendo mayor al de la máquina térmica. Esto debido a que la máquina térmica nunca dispone de una fuente cuya temperatura se acerque al cero absoluto $T=0K$

## Modelo Chambadal-Navikov
Si se considera la situación de tener una fuente térmica a temperatura $T_{2}$ y un sumidero térmico a $T_{1}$, y una máquina de la forma:
![[Pasted image 20251003232331.png|200]]
Existe la situación en que la máquina esté a la misma temperatura $T_{2}$ de la fuente térmica, entonces no debiese haber flujo de calor $Q$.
Pero la fuente térmica 'vé' una temperatura $T_{2}'$ un poco menor que la suya, siendo suficiente como para que exista un flujo de calor. En este caso, se considera un proceso *endorreversible* (casi reversible), entonces:
$$
\begin{align}
 & \eta =1-\frac{T_{1}'}{T_{2}'} \\
\text{si }T_{1}'=T_{2}' \implies & \eta=0
\end{align}
$$
Gráficamente, se tiene:
![[Pasted image 20251003233252.png|300]]
1. La potencia es 0 cuando no hay rendimiento (No funciona la máquina).
2. En $\eta_{\text{carnot}}$ el proceso es cuasiestático, entonces es muy lento. Por lo tanto, la potencia $P=0$

Entonces se tienen:
1. $$
   \eta_{\text{real}}=\frac{\text{beneficio}}{\text{costo}}
   $$
2. $$
   \eta_{\text{carnot}}=\text{teorico ideal}
   $$
3. $$
   \eta_{\text{C-A}}=\text{nuevo modelo}
   $$

## Computador
Para un computador, la eficiencia corresponde a
$$
\eta =\frac{\text{proceso de bit}}{\text{energia usada}}
$$

La tendencia de Kooney dice que se duplica la eficiencia cada 4 años, pero existe un límite físico del orden de un procesamiento de $\approx 10^{34}$ bits por segundo por Joule.

*Landauer:* Cuando se borra 1 bit de memoria se está aumentando la entropía del medio en $k_{b}\ln 2$

Transferir la entropía al medio está asociada a un calor mínimo:
$$
Q_{\text{1bit}}=k\cdot T\cdot \ln 2
$$
y a $300K$:
$$
Q_{\text{1bit}}=kT\ln2 = 3\cdot 10^{-21} [J] = 0,02 [eV]
$$
es la energía mínima que se disipa al borrar un bit.

- La computación reversible es posible si se tiene una compuerta lógica que entrega la información suficiente como para tener los números iniciales. *Ejemplo: Compuerta que entrega suma debe además entregar la diferencia.*


***

# Formalismo Termodinámico

No se puede medir la entropía o energía directamente. Entonces se buscan expresiones para ellas en función de magnitudes medibles (Hasta hora se tienen sólo para gases ideales).

## Magnitudes Medibles
Se tienen:
1. Calores específicos: 
   - a presión constante $C_{p}$ 
   - a volumen constante $C_{v}$
1. Coeficientes de dilatación: 
   - Volumétrica: 
     $$
     \alpha_{V}=\frac{1}{V}\left( \frac{ \partial V }{ \partial T } \right)_{P} 
     $$
   - Lineal:
     $$
\alpha_{L}=\frac{1}{L}\left( \frac{ \partial L }{ \partial T }  \right) _{P}
     $$

1. Coeficiente de compresibilidad isotérmica:
   $$
   \beta=-\frac{1}{V}\left( \frac{ \partial V }{ \partial P }  \right)_{T}
   $$

## Funciones (o Potenciales) Termodinámicos
1. Energía Libre de Helmholtz $F$:
   $$
   F=E-TS
   $$
   \* es libre pues no toda la energía de un sistema está disponible para realizar trabajo.
2. Entalpía $H$:
   $$
   H=E-(-P)V=E+PV
   $$
   \* $(-P)$ pues se definen como la resta de la magnitud intensiva conjugada multiplicada por su extensiva. En este caso, $V$ es la extensiva y $-P$ es la intensiva conjugada correspondiente.
3. Energía Libre de Gibbs $G$
   $$
G=E+PV-TS
   $$

### Variables Naturales
Las variables naturales son las que se obtienen al derivar las funciones (o potenciales) termodinámicos. Entonces, se puede realizar el proceso para los tres potenciales:
Primero, si se deriva la energía $E$:
$$
\begin{align}
dE=dQ+d\mathbb{W} \\
dE=TdS-PdV
\end{align}
$$
luego, derivando los potenciales:
1. Para la energía libre de Helmholtz $F$:
   $$
   \begin{align}
dF & =dE-d(TS) \\
 & = (TdS-PdV)-(dT\cdot S+T\cdot dS) \\
 & =-PdV - SdT
\end{align}
   $$
   se obtienen las variables $P$ y $S$ que corresponden a las variables naturales de la energía libre de Helmholtz $F$

2. Para la entalpía $H$
   $$
   \begin{align}
dH & =dE+d(PV) \\
 & =dE+(dP\cdot V + P\cdot dV) \\
 & =TdS-\cancel{ PdV }+VdP+\cancel{ PdV } \\
dH=TdS+VdP
\end{align}
   $$
   entonces las variables naturales de la entalpía $H$ corresponden a la temperatura $T$ y el volumen $V$.

3. Para la enegría libre de Gibbs $G$:
   $$
   \begin{align}
dG & =dE+d(PV)-d(TS) \\
 & = \cancel{ TdS }\cancel{ -PdV } +VdP+\cancel{ PdV }-SdT\cancel{ -TdS } \\
 & =VdP-SdT
\end{align}
   $$
   luego, las variables naturales de la energía libre de Gibbs $G$ son el volumen $S$ y la entropía $S$

### Relaciones de Maxwell

Utilizando el teorema de Schwarz $\frac{ \partial  }{ \partial y }\left( \frac{ \partial f }{ \partial x } \right)=\frac{ \partial  }{ \partial x }\left( \frac{ \partial f }{ \partial y } \right)$ en los potenciales y relacionándolos las unas con las otras, se llegan a obtener las **relaciones de Maxwell**:
$$
\begin{align}
\left( \frac{ \partial S }{ \partial P }  \right)_{V}=-\left( \frac{ \partial V }{ \partial T }  \right) \\
\left( \frac{ \partial S }{ \partial V }  \right)_{S}=\left( \frac{ \partial P }{ \partial T }  \right)_{S}
\end{align}
$$
las cuales entregan *una relación de la entropía $S$ con magnitudes medibles experimentalmente de prácticamente cualquier sustancia.*

## Entropía y Capacidad Térmica $C_{p}$
La capacidad térmica $C_{p}$ se conoce como la capacidad de un sistema de 'almacenar calor', pero en formalmente es la capacidad de un sistema de almacenar **entropía**
si la capacidad térmica es:
$$
\begin{align}
C_{p}= \frac{q}{\Delta T} \Biggr|_{P=\text{cte}}
\end{align}
$$
y considerando un proceso cuásiestático a presión constante: $q_{p}=T\cdot \Delta S$, entonces:
$$
C_{p} =\frac{T\Delta S}{\Delta T}\Biggr|_{P=\text{cte}} \xrightarrow{\Delta t\to_{0}} T\left( \frac{ \partial S }{ \partial T }  \right)_{P}
$$
así, la capacidad térmica a presión constante es
$$
C_{P}=\left( \frac{ \partial S }{ \partial T }  \right)_{P}
$$
y la capacidad térmica a volumen constante: $C_{V}=\left( \frac{ \partial S }{ \partial T } \right)_{P}$

## Ecuaciones $TdS$
1. Entropía en función de temperatura y volumen: $S=S(T,V)$
   Primero, diferencial de S:
   $$
   \begin{align}
dS & =\underbrace{ \left( \frac{ \partial S }{ \partial T }U  \right)_{V} }_{ C_{V} }dT+\underbrace{ \left( \frac{ \partial S }{ \partial T }  \right)_{T} }_{ \left( \frac{ \partial P }{ \partial T } \right)_{V} }dV \\
dS & =C_{V}+\left( \frac{ \partial P }{ \partial T } \right)_{V}dV \Bigr /\cdot T \\
TdS &  =C_{V}dT+T\left( \frac{ \partial P }{ \partial T }  \right)_{V}dV
   \end{align}
$$
en donde $C_{V}$ es medible y $P,T$ estpan relacionadas, entonces se puede *integrar y obtener S.*
\* no confundir $TdS$ de proceso cuasiestático ($q=TdS$) ya que este caso es más general.

2. Entropía en función de temperatura y presión: $S=S(T,P)$, realizando el mismo proceso que antes:
   $$
\begin{align}
dS & =\underbrace{ \left( \frac{ \partial S }{ \partial T }  \right)_{P} }_{ C_{P} }dT+\underbrace{ \left( \frac{ \partial S }{ \partial P }  \right)_{T} }_{ \left( -\frac{ \partial V }{ \partial T }  \right)_{P} }dP \\
dS & = C_{P}-\left( \frac{ \partial S }{ \partial T }  \right)_{P}dP \Biggr /\cdot T \\
TdS & =TC_{P}-T\left( \frac{ \partial S }{ \partial T }  \right)_{P}dP
   \end{align}
$$

3. Entropía en función de la presión $P$ y el volumen $V$: $S=S(P,V)$ es consecuencia de 1. y 2.

***
1. En plano $T,V$: proceso adiabático: $dS=0\implies C_{V}dT=-T\left( \frac{ \partial P }{ \partial T } \right)_{V}dV$
2. En plano $T,P$: Proceso adiabático :$dS=0\implies C_{P}dT=T\left( \frac{ \partial V }{ \partial T } \right)_{P}dP$
3. Para plano $P,V$ se divide 2. en 1. y se tiene que
   $$
\frac{ d P }{ d V } =-\gamma \frac{\left( \frac{ \partial P }{ \partial T }  \right)_{V}}{\left( \frac{ \partial V }{ \partial T }  \right)_{P}}
$$ 
en donde $\gamma=\frac{C_{P}}{C_{V}}$

***
para el caso de un gas **no ideal**, la temperatura puede variar, entonces, buscando una expresión para la energía en función del volumen $V$ y temperatura $T$: $E=E(V,T)$:
Desde que $dE=dQ+d\mathbb{W}$
$$
\begin{align}
\dots\ \iff dE=C_{V}dT+\left( T\left( \frac{ \partial P }{ \partial T }  \right)_{V}-P \right)dV \\
\iff \left( \frac{ \partial E }{ \partial V }  \right)_{T} = T \left( \frac{ \partial P }{ \partial T }  \right)_{V}-P
\end{align}

$$
lo que permite obtener la energía de cualquier sustancia en función del volumen $V$ y temperatura $T$.
\* se puede verificar para el caso de un gas ideal usando que $PV=Nk_{b}T$

## Equilibrio de un Sistema
Es posible tener el equilibrio de un sistema con sus propiedades en casos particulares:
Imponiendo caso cuasiestático: $dS'=\frac{q'}{T}$ y proceso espontáneo $dS_{U}=dS+dS'>0$ y si $q'=-q\implies dS'=-\frac{q}{T}$ y luego $dS_{U}=dS-\frac{q'}{T}>0$ 
$$
\vdots
$$
$$
\iff q=dE+P'dV+\iff T'dS-dE-P'dV>0
$$
si se tiene un proceso a temperatura constante y considerando la función de Helmholtz
$$
\begin{align}
\vdots \\
\iff &  dF<0
\end{align}
$$
osea se obliga a que $F$ disminuya, por ello, **el equilibrio será cuando $F$ sea mínimo.**
Luego, se está en equilibrio si $F=E-TS$ es mínimo

## Auxiliar 7
lo que permite obtener la energía de cualquier sustancvia 
- Las propiedades **extensivas** varían al cambiar el tamaño del sistema (en el sentido de concatenar 'doblar' la cantidad).
- Las propiedades **intensivas** no cambian con el tamaño del sistema.


|Extensiva     |Intensivas     |
| --- | --- |
|S     |T     |
|$\Theta$|$\phi$|
|V|-P|
|A|$\alpha$ (tensión superficial)|
|M|$\mu$ (potencial químico)|


### Potenciales Termodinámicos
Relacionados mediante:
$$
\begin{matrix}
U &  & \xrightarrow{\big /-TS} &  & F \\ \\

\downarrow\big/+PV &  & &  &\downarrow \big/+PV   \\ \\

 H & & \xrightarrow{\big /-TS} &   & G
\end{matrix}
$$
- Los potenciales son energías.
- Dependen del estado del sistema (osea no del camino).
- El que se use depende del sistema a analizar.
- La energía del universo local $\mathbb{U}$ se conserva, pero los potenciales no se conservan.


## Ecuación de la Energía
Antes se tenía la ecuación $\left( \frac{ \partial E }{ \partial V }  \right)_{T} = T \left( \frac{ \partial P }{ \partial T }  \right)_{V}-P$, pero en la práctica se usan las ecuaciones:
$$
\begin{align}
\left( \frac{ \partial E }{ \partial V }  \right)_{T}=T\left( \frac{ \partial P }{ \partial T }  \right)_{V}-P=\left( \frac{ \partial u }{ \partial v }  \right)_{T} \\
\left( \frac{ \partial E }{ \partial T }  \right)_{V}=C_{v}\to\left( \frac{ \partial u }{ \partial T }  \right)_{V}=C_{V}
\end{align}
$$
en donde $u=\frac{E}{\text{\# moles}},\ v=\frac{V}{\text{\# moles}}$

##### Ej: Problema del Helio
si $P=\frac{RT}{V}+\frac{RTB}{V^{2}}$, entonces
$$
\begin{align}
 & \left( \frac{ \partial P }{ \partial T }  \right)_{V}=\frac{R}{V}+\frac{RB}{V^{2}}+\frac{RTB}{V^{2}} \\
\text{si } B'=\frac{ d B(T) }{ d T } \implies & T\left( \frac{ \partial P }{ \partial T }  \right)_{V}-P=\left( \frac{R}{V}+\frac{RBT}{V^{2}}+\frac{RT^{2}B'}{V^{2}} \right)-\frac{RT}{V}-\frac{RTB}{V^{2}} \\
\left( \frac{ \partial u }{ \partial v }  \right)_{T}=\frac{RT^{2}B'}{V^{2}} \text{ (integrando)}\implies & u=-\frac{RT^{2}B'}{V}+ \varphi(T)
\end{align}
$$
para determinar $\varphi(T)$, considerando un gas muy diluido, o sea sucede que $v\to \infty$ y suponiendo que se tiene Helio (gas ideal monoatómico) en donde $E=\frac{r}{2}NkT,r=3$, además que se trabaja con 1 mol: $u=\frac{3}{2}N_{A}kT\to u=\frac{3}{2}kT$, entonces:
$$
\begin{align}
u(v,T) & =-\frac{RT^{2}B'}{v}+\frac{3}{2}RT \\
U(v,T) &  =\frac{3}{2}RT\left( 1-\frac{2}{3} \frac{TB'}{V} \right)
\end{align}
$$
y para $C_{V}$:
$$
\left( \frac{ \partial u }{ \partial T }  \right)_{V}=\frac{3}{2}R-\frac{R}{V}(T^{2}B')'
$$
## Disponibilidad Termodinámica
Denotando $X'$ como las variables que el sistema le ejerce al medio, se tiene la ecuación:
$$
\begin{align}
-dA=T'dS-dE-P'dV>0  \\
\iff dA=dE+P'dV-T'dS<0
\end{align}
$$
donde $A$ es la **exergía.**
\* La exergía es la parte de la energía de un sistema,  que es utilizable para realizar trabajo útil sobre el medio. La exergía en el equilibrio es = 0, aunque el sistema sí puede tener energía.

Luego, la ecuación de **disponibilidad** es:
$$
T'dS-dE-P'dV>0
$$

### Caso: Proceso a Temperatura Constante
Considerando el caso particular de un proceso a **temperatura constante**, se puede obtener su función de Helmholtz $F$:
![[Pasted image 20251012100820.png]]
su disponibilidad es
$$
T'dS-dE-P'dV>0
$$
considerando $T$ constante y $V$ constante, entonces $dV=0$ y la disponibilidad queda:
$$
\begin{align}
T'dS-dE\cancel{ -P'dV }>0 \\
TdS-dE=d(TS-E)>0 \\
\end{align}
$$
luego $dF>0$ o $dF<0$ por condición de espontaneidad, entonces $dF=0$

> Para un proceso a temperatura constante, el equilibrio se alcanza minimizando la energía libre de Helmholtz $F$.
>  A $T=0$ se reduce a minimizar la energía

#### Helmholtz como $\mathbb{W}$ máximo
Considerando un proceso a temperatura constante $T=T'=\text{cte}$,
$$
\begin{align}
 & dE =dQ+d\mathbb{W}_{T} \\
T \text{ cte}\iff  & d\mathbb{W}_{T} =dE-TdS \\
\iff  & dW_{T}=d(E-TS)_{T}=dF
\end{align}
$$
si se tiene un proceso extendido: $\mathbb{W}_{T}=F_{2}-F_{1}$ y si interesa el trabajo $\mathbb{W}'_{T}$ que el sistema ejerce sobre el medio:
$$
\mathbb{W}_{T}'=-\mathbb{W}_{T}=F_{\text{inicial}}-F_{\text{final}}
$$
y el caso en que $F_{\text{final}}=0$:
$$
\mathbb{W}'=F_{\text{inicial}}=(E-TS)_{\text{inicial}}
$$
- El término $-TS$ hace que la energía esté 'menos disponible', entonces no toda la energía inicial del sistema puede usarse. 
> Lo que resta es la "energía libre" para realizar trabajo.

### Caso: Presión Constante
Considerando un proceso a $P$ constante,
$$
\begin{align}
dE & =dQ+d\mathbb{W} \\
 & =dQ_{P}-PdV \\
\iff dQ_{P} & =dE+PdV \\
P\text{ cte: } &dQ_{P}=d(E+PV) 
\end{align}
$$
y se define la **entalpía** como $H=E-(-P)V$:
$$
\begin{align}
dQ_{P}=dH \bigg/\int \\
\iff Q_{P}=H_{2}-H_{1}
\end{align}
$$
> $Q$ no es variable de estado, pero en proceso isobárico (a $P$ cte) es igual a la diferencia de $H$ que sí es variable de estado.

1. $Q_{P}>0$ : Se ingresa energía al sistema, proceso **endotérmico.**
2. $Q_{P}<0$ : Se emite energía, proceso **exotérmico.**

*obs:* no confundir con $\Delta E>0$ proceso *endergónico* y $\Delta E<0$ proceso *exergónico*.

| Proceso                               | Relaciones                          |
| ------------------------------------- | ----------------------------------- |
| Adiabático $Q=0$                      | $\mathbb{W}_{adb}=\Delta E$         |
| Isocórico $\mathbb{W}_{V}=\text{cte}$ | $Q_{V=\text{cte}}=\Delta E$         |
| Isotérmico $\Delta T=0$               | $\mathbb{W}_{T\text{cte}}=\Delta F$ |
| Isobárico $\Delta P=0$                | $Q_{P\text{cte}}=\Delta H$          |

##### Ejemplo: Reacciones Químicas
Se realizan a presión $P$ constante, entonces se usa entalpía $H$ para describirlas.

Se determinan puntos de referencia para la entalpía en una reacción química:
1. $T=25°C$
2. $P=101325 [Pa]$
las cuales determinan la **Entalpía de Formación Estándar** $\Delta H_{f}°$ que, para los elementos en su forma más común se define como 0: $\Delta H_{f}°=0$

*Ej: Ozono $O_{3}$* 
El $O_{3}$ requiere energía, entonces $\Delta H>0$
*Ej: Quemar grafito* $C+0_{2}\longrightarrow CO_{2}$ a $P$ constante
Se mide el calor desprendido de la reacción $Q_{P}$ y éste es igual a la variación de entalpía $\Delta H$. Luego de muchas mediciones, se determina el $\Delta H_{f}°(CO_{2})$

- Así, se construyen las tablas con las entalpías estándar para los procesos químicos.
*Ejemplo: Combustión de Glucosa*
$$
6CO_{2} (g)+6H_{2}O \longrightarrow C_{6}H_{12}O_{6}+O_{2}\\
$$
Luego, la entalpía del proceso es igual a: (Entalpía de Estados Iniciales) - (Entalpía de Estados Restantes), de la forma:
$$
\begin{align}
\Delta H & =\bigg(6\Delta H_{f}°(CO_{2} (g))+6\Delta H_{f}°( H_{2}O)\bigg) - \bigg(\Delta H_{f}°(C_{6}H_{12}O_{6})+\cancelto{ 0 \text{ por def} }{ \Delta H_{f}°(O_{2}) }\bigg)\\
 & =\bigg(6\cdot(-393,5)+6\cdot(-285,8)\bigg)-\bigg( -1273 \bigg)\ \left[ \frac{kJ}{\text{mol}} \right] \\
\iff \Delta H & =-2803 \left[ \frac{J}{K} \right]
\end{align}
$$
como $\Delta H<0$ corresponde a una reacción exotérmica.

### Caso: Temperatura T y Presión P constantes
La disponibilidad es
$$
T'dS-dE-P'dV>0
$$
proceso a T,P constantes y en condiciones de equilibrio con el medio $T'=T,P'=P$:
$$
\begin{align}
 & d(TS-E-PV)>0 \\
 & d\underbrace{ (E+PV-TS) }_{ dG }<0 \\
\iff &  dG<0
\end{align}
$$
> Para proceso a temperatura y presión constante, el equilibrio sucede cuando la energía libre de gibbs $G$ es mínima.

##### Ej: Con trabajo eléctrico
Si se tiene trabajo eléctrico $d\mathbb{W}_{e}=(d\mathbb{W}_{e}+\mathbb{W}_{PdV})+dQ$,
$$
\begin{align}
 & dE=d\mathbb{W}_{e}-PdV+TdS \\
\iff & d\mathbb{W}_{e}=dE+PdV-TdS \\
P,T\text{ ctes: }\implies & d(E+PV-TS) \\
\iff & d\mathbb{W}_{e}=dG \\
\iff & \mathbb{W}_{e}=\Delta G
\end{align}
$$
por lo tanto, $G$ es una medida de la disponibilidad de realizar $\mathbb{W}_{e}$ (o cualquier trabajo que no sea $PdV$).
$\mathbb{W}_{e}$ no es una variable de estado, pero a P,T cte es igual a la diferencia de $G$ que sí lo es.

## Ecuación de Euler
Escribiendo la energía $E$ en función de sus variables extensibles:
$$
E=(\chi_{1},\chi_{2},\chi_{3},\dots,)
$$
entonces sus variables intensivas $\xi_{i}$ son:
$$
\xi_{i}=\frac{ \partial E }{ \partial \chi_{i} } 
$$


para una función homogénea de grado $n$ $f(\lambda x_{1},\lambda x_{2},\dots,\lambda x_{N})=\lambda^{n}f(x_{1},x_{2},\dots,x_{N})$ y derivando con respecto a $\lambda$, usando notación $\frac{ \partial f }{ \partial x_{1} }=f_{1}$:
$$
f_{1}()x_{1}+f_{2}()x_{2}+\dots+f_{n}()x_{n}=n\lambda^{n-1}f
$$
para $\lambda=1$:
$$
f_{1}x_{1}+f_{2}x_{2}+\dots+f_{N}x_{N}=f
$$
Uso en termodinámica: Duplicando el tamaño de un sistema, se tiene que $E$ es homogénea de grado 1, o sea, si se aumenta el tamaño del sistema, este crece en $\lambda=1$. Si se duplica el tamaño, la energía aumenta al doble; Si se triplica el tamaño, la energía aumenta al triple.

### Relacion de Gibbs-Duhem
Diferenciando la ecuacion anterior:
$$E=d\sum_{i}\xi_{i}X_{i}=\sum_{i}d(\xi_{i}X_{i})$$
$$=\sum_i\xi_idX_i+\sum_i(d\xi_i)X_i$$
$$\begin{aligned}&\text{pero }dE=\sum_i\xi_idX_i \end{aligned}$$
- No todas las variables intensivas pueden variarse independientemente.
  *Ejemplo*: $SdT+Vd(-P)+\Theta d\phi=0$

# Gases
La ecuación de gas ideal corresponde a $PV=nRT$ y para un mol:
$$
PV=vRT
$$
con $v=\frac{V}{\text{nro de moles}}$

Viendo modelos que no corresponden al caso del gas ideal.
## Factor de Compresibilidad $Z$
$Z$ es el factor de compresibilidad y está tabulado para gases de uso común.
$$
Z(P,T)=\frac{Pv}{RT}
$$
### Comparación con Respecto a Gas Ideal
Obteniendo el volumen de la expansión de un gas en donde comienza en condiciones: $P_{1}=150[bar],T_{1}=25°C,V_{1}=40[L]$ hasta las condiciones: $P_{2}=1[bar], T_{2}=25°C$
1. Considerando el gas como ideal, se tiene la ecuación de gases ideales:
   $$
   \begin{align}
 & PV=NkT \iff \frac{PV}{T}=Nk \iff \frac{P_{1}V_{1}}{T_{1}}=\frac{P_{2}V_{2}}{T_{2}} \\
 & V_{2}=\left( \frac{P_{1}}{P_{2}} \right)V_{1} \iff V_{2}=\left( \frac{150}{1} \right)V_{1} \\
 & V_{2}=150\cdot 40 [L] \iff V_{2}=6000[L]=6[m^{3}]
\end{align}
   $$
   2. Considerando el gas con un factor de compresibilidad $Z_{1}=0,943,\ Z_{2}=0,999$:
      $$
\begin{align}
PV=NkTZ \\
\implies P_{1}V_{1}=NkT_{1}Z_{1} \\
\implies P_{2}V_{2}=NkT_{2}Z_{2}  \\
 \\
\frac{P_{2}V_{2}}{P_{1}V_{1}}=\frac{Nkt_{2}Z_{2}}{NkT_{1}Z_{1}} \iff \frac{P_{2}V_{2}}{P_{1}V_{1}}=\frac{Z_{2}}{Z_{1}} \\
\iff V_{2}=\left( \frac{150[bar]\cdot40[L]}{1[bar]} \right)\cdot\left( \frac{0,999}{0,943} \right) =6000[L]\cdot 1,06=6356[L]=6,36[m^{3}]
\end{align}
$$
así el error con respecto a al ecuación del gas ideal es de $\approx 6\%$

## Ecuaciones Viriales
Para el factor de compresibilidad $Z=Z(P,T)$ haciendo desarrollo de potencias:
$$
\begin{align}
 & \frac{Pv}{RT}=Z(P,T) \\
\iff  & \frac{Pv}{RT}=1+B'(T)+C'(T)^{2}+\dots
\end{align}
$$
y para volumen:
$$
\begin{align}
 & Z=Z(v,T) \\
\iff & Z(v,T)=1+\frac{B(T)}{v}+\frac{C(T)}{v^{2}}+\frac{D(T)}{v^{3}}+\dots
\end{align}
$$
los coeficientes $B(T)$ están tabulados para muchos gases.

## Ecuaciones Semiempíricas

### Ecuación de Clausius
 Plantea que se debe corregir el volumen, pues el gas no se encuentra en absolutamente todo el espacio disponible para él, ya que las partículas que lo componen chocan entre ellas. Entonces
 $$
\begin{align}
 & V_{\text{efectivo}}=V-b \\
\implies & P\cdot V_{\text{efectivo}}=RT \\
\iff & P(V-b)=RT
\end{align}
$$

### Ecuación de Van der Waals
Plantea que el gas ejerce una presión menor al recipiente debido a que las moléculas del gas cercanas entre sí, se atraen mutuamente, disminuyendo su momento.
Se tiene que
$$
\underbrace{ \left( P+\frac{a}{v} \right) }_{ P_{\text{efectiva}} }\cdot\underbrace{ (V-b) }_{ V_{\text{efectiva}} }=RT
$$
donde $a,b$ se conocen como las constantes de Van der Waalks y dependen del gas, que corresponden a la relación de atracción entre sus moléculas.
En la práctica se utilizan las relaciones para $a,b$:
$$
\begin{align}
a & =\frac{27R^{2}T_{c}^{2}}{64P_{c}} \\
b & =\frac{RT_{c}}{8P_{c}}
\end{align}
$$
donde
1. $T_{c}$ es la temperatura crítica del fluido: es la cual no se puede licuar el gas.
2. $P_{c}$ es la presión crítica, es la que se necesita para licuar a $T_{c}$
ambas son parámetros medibles.

### Ecuación de Redlich-Kwong
Es un reajuste numérico de la ecuación de gas ideal, ya que hay una disminución de la presión que es proporcional a la temperatura:
$$
P=\frac{RT}{V-b}- \frac{\frac{a}{\sqrt{ T }}}{\frac{V}{(v+b)}}
$$

## Procesos fuera del equilibrio

### Expansión Libre

Considerando un gas aislado, confinado a un volumen $V$ con una cavidad extra de volumen $\Delta V$, el gas pasa de tener un volumen $V$ a un volumen $V+\Delta V$. El proceso ocurre a energía $E$ constante por ser un sistema aislado, luego $Q=0,\mathbb{W}=0$.
Y se busca determinar si el gas se calienta o se enfría, esto es equivalente a calculas el **coeficiente de Joule**.
$$
\begin{align}
\frac{\Delta T}{\Delta V}\Biggr|_{E\text{ cte}}\iff  & \mu_{J}=\left( \frac{ \partial T }{ \partial V }  \right)_{E} \\
\vdots \\
\mu_{J}=\frac{1}{C_{V}}\left( T\left( \frac{ \partial P }{ \partial T }  \right)_{V}-P \right)
\end{align}
$$

### Expansión Forzada en Proceso de Joule-Thompson
Proceso en el cual una bomba hace circular un gas desde una presión alta a una baja a través de un obstáculo. Puede aumentar o disminuir la temperatura según el caso.

Utilizando un *volumen de control* se estudia cómo evoluciona un volumen de gas a lo largo de un flujo en una tubería.
Asumiendo proceso adiabático $Q=0$,
$$
\begin{align}
\mathbb{W} & =\mathbb{W}_{\text{izq}}+\mathbb{W}_{\text{der}} \\
\mathbb{W}_{\text{izq}} & =\int_{i}^{f} -P \, dv=-P_{2}(V_{f}-V_{i}) =P_{2}V_{2} \\
\dots W_{\text{der}} & =-P_{1}V_{1} \\
 & \vdots \\
\underbrace{ E_{1}+P_{1}V_{1} }_{ H_{1} } & =\underbrace{ E_{2}+P_{2}V_{2} }_{ H_{2} } \\
H_{1}=H_{2}
\end{align}
$$
luego, la entalpía en expansión forzada es constante.

#### Curvas Isentálpicas
Considerando la energía para gas ideal $E=\frac{r}{2}NkT;\ PV=NkT$. Si $H=E+PV$, entonces:
$$
H=NkT\left( \frac{r}{2}+1 \right)
$$
![[Pasted image 20251012171820.png]]

1. Se tienen dos zonas:
   - La zona de enfriamiento (en gris): Gas se enfriará al realizar el proceso de expansión forzada
   - La zona de calentamiento (en blanco): Gas se calienta en proceso de expansión forzada.

1. Curva de inversión es la que limita la zona de enfriamiento con la de calentamiento.
2. El punto de intersección de la curva de inversión con el eje de la temperatura es la temperatura de inversión máxima: Si el gas se encuentra a esa temperatura, independiente de la presión que se tenga, el gas sólo se va a calentar.

> Todos los gases se comportan igual: Tienen zona de enfriamiento y calentamiento, delimitadas por una curva de inversión.

Para saber si el gas se enfría o calienta:
viendo $\frac{\Delta T}{\Delta V}\Biggr|_{E\text{ cte}}\iff  \mu_{J}=\left( \frac{ \partial T }{ \partial P }  \right)_{H}$, usando relación cíclica: 
$$
\underbrace{ \left( \frac{ \partial T }{ \partial P } \right)_{H} }_{ \mu_{J-T} }\left( \frac{ \partial P }{ \partial H } \right)_{T}\underbrace{ \left( \frac{ \partial H }{ \partial T } \right)_{P} }_{ C_{P} }=-1
$$
entonces:
1. $$
   \frac{PV}{RT}=1
   $$
2. Van der Waals:
   $$
   \left( P+\frac{q}{v^{2}} \right)(V-b)=RT
   $$
   donde existe la temperatura crítica $T_{C}$, que corresponde al límite de temperatura en donde es imposible licuarlo; $P_{C}$, la presión mínima necesaria para licuar a $T_{C}$; $V_{C}$, el volumen molar a $P_{C},T_{C}$.
   Se define entonces la **temperatura reducida**:
   $$
T_{r}=\frac{T}{T_{c}},\ P_{r}=\frac{P}{P_{C}},\ V_{r}=\frac{V}{V_{C}}
   $$
   que son magnitudes adimensionales. Si se reemplazan en la ecuación de Van der Waals:
   $$
   \implies \left( P_{r}+\frac{3}{V_{r}^{2}} \right)(3V_{r}-1)=8T_{r}
   $$
   en donde ya no se encuentran las constante $a,c$ que dependen del gas (las constantes se pueden expresar con $P_{C}$ y se pueden despejar.

> Todos los gases son iguales, debidamente escalados.

y se define el **factor de compresibilidad crítico** $Z_{C}$:
$$
Z_{C}=\frac{P_{C}V_{C}}{RT_{C}}
$$
y hay grupos de gases que tienen el mismo factor de compresibilidad $Z$, y se comportan de manera similar. Así se pueden clasificar los gases.