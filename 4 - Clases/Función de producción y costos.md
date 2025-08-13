#economía
Una empresa utiliza factores de producción y los transforma en bienes y servicios. Qué y cómo produce la empresa, depende de:
1. Los precios de los insumos
2. Precios de venta posibles
3. Tecnología que posee

# Función de costos
La función que indica el gasto mínimo necesario para producir una cierta cantidad $q$ de producto, dada por los ... se llama función de costos, denota con $C(q)$ y tiene la forma:
***grafica 2 curvas de costos***

donde se vé que producir mucha cantidad $q$ comienza a ser cada vez más caro.

Y también se tiene la relación inversa, llamada **curva de ofertas**, la cual corresponde al precio de $q$ en función de la cantidad $q$ producida:
***dibujo P(q) vs q***
en donde se grafica la relación inversa: La curva de oferta inversa, $q_{s}^{-1}(P)$

# 
El objetivo de una firma es maximizar la utilidad, esto es: ***Ingresos - Costo de producción**.

## Competencia Perfecta
Si se hace una suposición de una situación conocida como **competencia perfecta**, la firma maximiza las utilidades para un precio $P$ según:
$$
\text{Max}\; \pi(q) = P\cdot q- C \cdot q
$$
Es una situación en donde la firma considera a el precio $P$ como un dato, osea no se cree que se puede modificar el precio de venta por sí mismo.
	Ejemplo: Panaderías y el precio del pan, donde si se tiene el precio muy alto del pan, no le compran.

1. Es realista: Existen modelos que operan así, pero hay situaciones donde hay muy pocas firmas (ej: monopolios o duopolios)
2. Los precios de los insumos están contenidos en $C(q)$ 
3. El modelo $\pi$ sirve para solamente un período específico de producción a cierto precio de venta $P$. Así, no hay posibilidad de 'guardar' producción para un futuro en que cambia el precio de venta $P$.
Para tener la cantidad $q$ producida, se puede derivar $\pi$ e imponer la condición de igualar a 0.

### Midiendo costos
En el modelo
$$
\text{Max}\; \pi(q) = P\cdot q- C \cdot q
$$
el costo de producción para una cantidad $q$, se puede tener con:
$$
C(q) = C\cdot F+C\cdot V(q)
$$
donde 
* $C\cdot F$ no depende de la cantidad $q$ de producción.
	  Ejemplo: El arriendo de un espacio, el sueldo de trabajadores.

* $C\cdot V(q)$ depende de la cantidad de producción $q$ 

¿Cómo se miden los costos? Hay costos de insumos contratados y costos propios:
1. Para los contratados se tiene que el costo es el mismo precio del contrato.
2. Para los propios se considera el **costo de oportunidad**.
	   Ejemplo: Panadería y el costo de oportunidad de poseer una bodega y equipos (y no arrendarlas), además del tiempo dedicado que puede ser utilizado en otro ingreso.

# Condiciones de Primer y Segundo grado
## Condición de Primer grado (CPO)
La primera derivada de una función, en economía se le denomina la condición de primer grado, en donde se hace:
$$
\pi'(P) =0
$$
en donde la cantidad de producción óptima $q'$ es donde el precio de venta $P = \pi'$ 

La primera derivada en economía corresponde al **costo marginal**, esto es, cuánto varía el costo al aumentar infinitesimalmente la cantidad producida $q$.
***dibujo 2 curvas con pendientes cambiando en cada sección.***

Para las curvas de costo marginal, para un precio de venta $P$ específico, es posible hacer una proyección hasta la curva para obtener la cantidad $q^{*}$ que corresponde al precio de venta elegido. Osea, ***la curva de costo marginal dice para qué precio, cuánto es posible producir.***


# Clase 11/08
Se puede tener el caso en donde el costo marginal es mayor en el inicio y en el final, y entremedio es menor. Así, para un precio dado, es posible tener 2 posibles costos. En esta situación se busca la mayor cantidad posible de producción.
*** gráfico costo marginal 2, elegir pi'' > o
Para esta situación, se busca entonces que la función que modela el costo sea convexa, matemáticamente: $C''(q)>0$, 

# Condición de Segundo Orden (CSO)
Para la condición de primer orden CPO, se buscaba que la primera derivada de la función que modela el costo sea 0: $C'(q)=0$
Y si se quiere que la cantidad óptima producida debe estar **en la parte creciente** de la función de costos, esto es:
$$
\begin{align}
\pi''(q)<0 \\ \\

\implies C''(q^{*})>0 \iff CMg'(q')>0
\end{align}
$$
# Función de Oferta
Corresponde a la función que, para cada precio $P$, se indica la la cantidad $q_{s}(P)$ que oferta la firma.
Y también corresponde a la función de costo marginal, con ello se puede determinar la cantidad a producir para dado precio.
	Para cada precio $P$, la cantidad ofertada por una firma será aquella cantidad $q$ **de la porción creciente** de la función de costo marginal $CMg(q)$, tal que: $P=CMg(q)$

# Función de Producción 
1. Identificar combinaciones factibles para la producción: ¿Qué combinaciones de insumos permiten producir una cantidad dada de producto?
2. De las combinaciones de insumos factibles, ¿Cuál es la de menor costo?
	Ej: Producción de autos en GM: necesita trabajo, cobre, acero, electricidad, etc.

Se va a simplificar la cantidad de insumos a 2 (sin pérdida de generalidad): 
- Trabajo o labor $L$
- Capital $K$: Maquinaria o 'robots'

La función de producción asigna a cada combinación de insumos, la mayor cantidad posible de producción para un cierto período, considerando la tecnología que dispone la firma, y se denota:
$$
q = f(K,L)
$$
donde,
- $q$ son las unidades producidas
- K es la unidad de capital (máquinas, tierra)
- $L$ son las unidades de trabajo (horas-hombre)

Ejemplo: **Función de Producción de Cobb-Douglass**
$$
f(K,L)=a\cdot F^{\beta}\cdot L^{1-\beta}
$$
La función de producción:
1. Asume eficiencia máxima tecnológica,
2. Es individual para cada firma, pues pueden variar en tecnología disponible
3. Se asume que se poseen los insumos, ya que la función no indica cómo obtener los insumos.
4. Lo producido también pueden ser servicios.
	Ej: Singapur, Hong-Kong, tuvieron crecimiento por ofrecer servicios financieros.

# Productividad Marginal

Corresponde a la medida del beneficio para la firma el contrato de una unidad más de insumo.
$$
PmgL(K,L)=\frac{\partial}{\partial L}f(K,L)=f_{L}(K,L)
$$
$f$ es unidad de producción, así $PMgL$ indica cuánto aumenta la producción al contratar 1 hora más de un trabajador, con K constante.
Para contexto de eficiencia tecnológica, se requiere que la tasa de crecimiento en ambas variables sea creciente, esto es:
$$
f_{K}>0,\; f_{L}>0
$$
es posible que sea $\geq$ pues hay situaciones en donde aumentar un insumo no implica un aumento inmediato en la producción, si no que se requiere un aumento también de otro insumo. (Ej: Martillos para trabajadores)
El gráfico de la productividad marginal es:
![[Pasted image 20250812165001.png|Productividad marginal]]
de donde se puede ver que la productividad marginal crece, pero eventualmente se estanca el crecimiento para comenzar a descender (la producción deja de crecer). Que sucede por la explotación del insumo que se está aumentando. Esto se conoce como **Ley de los retornos decrecientes de los insumos.**
Se observa que en $L^{*}$ aumentó la producción con la contratación de un trabajador especpifico (ya que se está aumentando $L$), pero las firmas usualmente no eligen esto. 
- Hay otra forma de medir la productividad con la *productividad media del trabajo*, que se calcula por la cantidad de trabajadores $L$.
  $$
PMeL = \frac{f(K,L)}{L}=\frac{q}{L}
$$
## Isocuantas de Producción (O curva de nivel)
Corresponde a un gráfico que muestra una curva por cada posible combinación de $K$ y $L$ que permiten producir una determinada cantidad de un bien. 
Gráficamente:
![[Pasted image 20250812170305.png]]
	Cada curva es una combinación específica, que dan una cantidad $q_{i}$ de bienes.
donde, cada isocuanta para un determinado $q_{i}$ se denota como $K(L,q_{i})$ y esta indica, para cada valor de labor $L$, el mínimo de maquinaria $K$ necesaria para producir $q_{i}$

### Tecnología de Leontieff
Es una posible forma de isocuanta, donde se indica que se requiere 1 de un recurso por 1 del otro recurso, resultando de la forma:
***curva wea leontieff (cuadrada)***

## Tasa Marginal de Sustitución de Capital por Trabajo (TST)

Dada una cierta isocuanta $K(L,q)$, es posible calcular la tasa a la cual se puede sustituir capital $K$ por labor $L$, sin afectar la producción. De la forma:
$$
TST_{K,L}=-\frac{\mathcal{d}}{\mathcal{d}L}K(L,q)
$$
	Esto es:
	 Si se disminuye la labor (trabajadores)
	-> disminuye la producción
	¿Cuánto capital $K$ se requiere para reemplazar la pérdida y mantener la cantidad $q$ de producción?

Viendo las isocuantas de producción, y como la TST es el opuesto de la tasa (derivada <-> tangente), se vé que esta es mayor cuando se tienen menos trabajadores $L$:
![[Pasted image 20250812172248.png]]
Esto se debe a que a una menor cantidad de trabajadores, cada uno es más valioso para la producción de bienes, entonces perder uno genera un mayor impacto y se requiere más capital para reemplazarlo.

