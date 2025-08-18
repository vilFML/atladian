La economía estudia el cómo los agentes toman decisiones cuando los recursos son escasos. Esto involucra descartar una alternativa por la que se escoge, lo que tiene asociado un costo de oportunidad.
- La toma de la decisión requiere un análisis de costo versus beneficio.

El tiempo es un bien que se debe administrar, 
- Por ejemplo: Escoger tiempo libre versus tiempo para producción (trabajo)

Se busca encontrar un modelo que permita estudiar cómo las personas escogen qué hacer con el tiempo: si tomarlo como tiempo libre o trabajar.




# Curva de demanda
Es un tipo de aplicación de la toma de decisiones de agentes en contexto de escasez.
Se va a determinar cómo es la toma de decisión de un individuo para extrapolar la información a un modelo que considere variables como el precio.

## Función de utilidad individual (del consumidor)
se define como:
$$
U(x,y)=v(x)+c
$$
con,
- $x$: la cantidad consumida del bien
- $c$, el consumo de otros bienes.

Es una función creciente para ambos bienes, donde
- $v(x)$ es la utilidad asociada al bien $x$
- $c$ es la utilidad asociada al consumo de otros bienes.

El consumidor busca maximizar la utilidad de $U(x,y)$, pero tiene su ingreso $I$ como restricción:
$$
\begin{align}
\text{max}_{x,c} & \;v(x)+c  \\
 s.a.:&\ \ p\cdot x+c=I
\end{align}
$$
$I$ es el ingreso del individuo para el consumo de $x$ y $c$ y $p$ es el precio del bien $x$.

Si se hace el reemplazo de $c = I -p\cdot x$ en la función a maximizar, se tiene la utilidad como:
$$
\text{max }_{x}\ v(x)-p·x+I 
$$
así, la condición de primer orden [[Función de producción y costos#Condición de Primer grado (CPO)|(CPO)]] es:
$$
v'(x)=p
$$
la condición de primer orden dice que la utilidad $v(x)$ se maximiza cuando la utilidad marginal $v'(x)$ es igual al precio $p$ del artículo $x$, considerando que la curva de $v(x)$ sea cóncava: $v''(x)<0$
- Cada unidad adicional que se consume aumenta su utilidad, pero ésta va disminuyendo mientras más bienes se consumen.

### Curva de demanda
Cuando se grafica el precio $p$ del bien '$x$' con respecto a la cantidad consumida $x$ de bienes, se obtiene la curva que representa la cantidad óptima de consumo para cada precio:
![[Pasted image 20250817201650.png]]
la curva entrega la cantidad $x_{1}$ óptima a consumir dado el precio $p$ del bien.
- Segunda derivada negativa: a medida que el precio baja, el consumo del bien aumenta.

### Excedente del consumidor
Dado un ingreso fijo $I$ y una curva de demanda, al variar el precio el consumo del bien varía.
Para la situación en que el precio baja desde un precio $p_{0}$ a $p_{1}$, el consumo del bien varía desde $x_{0}$ a $x_{1}$, hay una variación en la utilidad del consumidor, denotado como variación del excedente del consumidor.
La variación del excedente $\Delta \text{EC}$ corresponde a la variación de las utilidades:
$$
\Delta \text{EC} = U(x_{1})-U(x_{0})
$$
donde $U(x_{i})=V(x_{i})-p_{i}·x_{i}+I$ es la utilidad óptima a precio $p_{i}$, expresando la utilidad y reagrupando términos:
$$
\begin{align}
\Delta \text{EC}= & \left( v(x_{1})-p_{1}·x_{1}+I \right) - \left( v(x_{0})-p_{0}·x_{0}+I \right)  \\
\Delta \text{EC}= & v(x_{1})-p_{1}·x_{1}+p_{1}x_{0}-v(x_{0})+p_{0}x_{0}) \\
\Delta \text{EC}= & v(x_{1})-v(x_{0})+(p_{0}-p_{1})x_{0}-p_{1}(x_{1}-x_{0})
\end{align}
$$
![[Pasted image 20250817204547.png]]
1. El término $v(x_{1})-v(x_{0})$, por teorema del fundamental de cálculo:
   $$
   \int_{x_{0}}^{x_{1}}v'(x)dx=v(x_{1})-v(x_{0})=A+C
   $$
   lo que representa el área bajo la curva entre los puntos $x_{0}$ y $x_{1}$ y corresponde a la *diferencia de la utilidad por el aumento del consumo de bienes.*
   - Área $A$

1. El término $B=(p_{0}-p_{1})x_{0}$ es el aumento de la utilidad por la reducción de un precio más alto $p_{0}$ a uno más bajo $p_{1}$ de una cantidad $x_{0}$ fija de bienes.
   - Área $B$

1. El término $-C=-p_{1}(x_{1}-x_{0})$ representa el gasto adicional por el aumento en la cantidad de consumos, desde una menor cantidad $x_{0}$ a una mayor cantidad $x_{1}$.
   - Área $C$

Por lo tanto, el excedente neto del consumidor $\Delta EC$, corresponde a:
$$
\Delta EC=A+B
$$

![[Pasted image 20250817204915.png]]