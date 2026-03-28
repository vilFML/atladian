# Física basada en partículas

## Sistema de Partículas

Un sistema de partículas es una colección de elementos *puntuales*, los cuales son descritos por su **estado actual**, dado por:
1. Posición $(x,y,z)$
2. Velocidad
y opcionales como masa, edad, color, etc. Y la idea es que estas propiedades cambien en el tiempo para generar los efectos deseados.
Por ej: El disparo de un cañón, en donde las partículas cambian su posición en el tiempo y también pueden cambiar su color desde el momento del disparo en adelante.

El movimiento de las partículas depende de **campos de fuerzas** externos y, eventualmente, fuerzas internas entre partículas.

Las partículas también pueden tener un tiempo de vida asociado (*time to live* TTL)

Un sistema de partículas se caracteriza por tener
- una fuente emisora de partículas (muchas), 
- un **campo de fuerza** que define las fuerzas externas que afectan a las partículas

Para ello se utilizan las **leyes de la mecánica** y se integran sus ecuaciones diferenciales.

En los casos más simples, se puede permitir que cada partícula sea *indepediente* de las demás, o que interactúen entre ellas.

Sobre todo en la emisión, suele haber aleatoriedad. Generando efectos interesantes.

### Ejemplo: Problema de los Boids

Un *boid* es cuando se hace que las partículas tengan un *comportamiento*, simulando bandadas de pájaros o masas de gente.
En este caso las partículas interactúan entre sí, entonces pierde su independencia con respecto a otras.
Se tiene:
- Separación: Hay movimiento para evitar estar muy cerca de un vecino
- Alineación: Que haya orientación *hacia el promedio de orientación* de una vecindad de unidades
- Cohesión: Movimiento para que la separación relativa entre los vecinos sea la misma.

Se aplica en masas de pájaros, de gente o un cardumen de peces.También se usa en otros fenómenos como la caída de lluvia que se encuentra con un obstáculo.


## Fuerzas a usar

Se va a trabajar con fuerzas que *cambian el movimiento* de un sistema. 

Para masas puntuales, las fuerzas son vectores

### Fuerza de Gravedad

Para modelar la gravedad se tiene una dependencia de la *masa* de la partícula

\* El humo se puede modelar como partículas con la gravedad invertida.

## Ciclo de vida

El esquema usual de los programas que modelan partículas es:

```py
PartList = []
dispersión = 0.1
k = 1000

# generar k partículas, inicialmente en la misma posición generadora
# pero con un factor aleatorio para determinar la dirección de velocidad
for i in range(k):

	p = nuevaParticula()
	p.posición = (0, 0, 0)
	p.velocidad = (0, 0, 1) + dispersión * (random(), random(), random())
	
	PartList.append(p)

```
esto se manidiesta que tanto enx como en y no se aplica ninguna velocidad inicialmente, solamente hacia arriba. Y además con la función `random()` se agrega una aleatoriedad en las otras direcciones x,y. 
El ciclo `for` crea las partículas en una posición determinada $(0,0,0)$ y después a cada una le asigna una velocidad tal que sea hacia arriba y una aleatoriedad con `random()` en las otras direcciones

Después de la creación, en la actualización 

```py
# en cada paso de la simulación, para cada instante de tiempo dt
while True:

	dt = tiempoActual - tiempoAnterior
	
	# para cada partícula, se calculan su nueva posición y velocidad
	# (y otras posibles propiedades)
	for particle in PartList:
	
		particle.posición += particle.velocidad * dt # nueva pos.
		particle.velocidad -= g*dt                   # nueva vel.
		particle.color[3] -= 0.01 * dt               # nuevo color
		
		# se dibuja la particula
		dibujar(particle)
		# y se puede sacar de la simulación si es que ocurre alguna condición
		if particle.color[3] <= 0:
			
			PartList.remove(particle)

```
se espera que el $dt$ sea constante: en cada deltaT la partícula sigue una trayectoria tangente, que se actualiza luego de terminar $dt$

se debe notar que en la modificación de color se está modificando la 4a componente del array: $(R,G,B,A)$, osea $A$ que corresponde a la transparencia. Cada vez es más transparente y cuando tenga una transparencia tal que la partícula no se ve en pantalla, el `if` destruye la partícula.

# Ecuaciones Diferenciales Ordinarias (EDO)

La aplicación de fuerzas se reduce a solucionar EDOs.

La trayectoria de una partícula se puede modelar con
$$
\frac{dX}{dT}=f(x(T),T)
$$
con $\frac{dX}{dT}$ el desplazamiento y la fuerza es dependiente de la posición $X(T)$ y del tiempo $T$.
Se requiere una posición inicial $X(T=0)$ y 

# Recuerdo EDO

Como se va a trabajr con fuerzas, se va a trabajr con 
$$
\vec{F}=m\vec{a} < = > \vec{F}=m \frac{d^{2}\vec{x}}{dT^{2}}
$$

la primera derivada de la posición es la velocidad $\frac{ d X }{ d T }=V$ y la segunda derivada de la posición, o sea la derivada de la velocidad: $\frac{ d V }{ d T }=\frac{F}{m}$

Luego, si a cada partícula se le asigna cuál es su posición y velocidad, modelando cuál va a ser su trayectoria, se va a tener un vector con la información de su posición $\vec{x}$ y su velocidad $\vec{v}$ en todo momento.
$$
X = \left( \begin{matrix}
\vec{x} \\
\vec{v}
\end{matrix} \right)
$$
o sea
$$
X = \left( \begin{matrix}
x_{1} \\
v_{1} \\
\dots \\
x_{N} \\
v_{N}
\end{matrix} \right)
$$
con $x_{1},v_{1}$ es la información de la partícula 1, y así para las siguientes.

además


### Interpretación

La interpretación es que $X(T)$ indica **el camino a seguir** en un espacio.

Para encontrar una solución numérica al problema se integra la edo. Para ello, si se tiene un estado $X$, se puede mirar el valor de la función *cerca* del estado actual en el espacio y **se mueve una pequeña distancia en tal dirección**. O sea:
$$
dX = dt \cdot f(X, t)
$$

usando el método de Euler, de la relación anterior $dX = dT \cdot f(X, t)$, se hace
$$
(X_{1}-X_{0})=(t_{1}-t_{0})\cdot f(X,t)
$$
y, si se define $h =t_{1}-t_{0}$ y $X_{0}=X(t_{0})$, entonces:
$$
(X_{1},X_{0}) = h \cdot f(X_{0},t_{0})
$$
$$
X_{1} = X_{0} + h \cdot f(X_{0},t_{0})
$$


el tamaño de $h$ controla la precisión de la aproximación (la precisión de la trayectoria que se va a seguir:
![[Pasted image 20260326093353.png]]
desde abajo hacia arriba se incrementa la precisión al reducir el valor de $h$

Para tener la posición siguiente se necesita la posición anterior y el valor de la fuerza en la posición anterior.
$$
X_{N}=X_{N-1} + \Delta t \cdot f(X_{N-1}, T)
$$
con $X_{0}$ conocido.

El método de euler no representa un círculo, si  no que una espiral, pues se basa en la tangente.

#### Método RK4
recalcula la pendiente desde cada punto para ir, efectivamente, al punto final.

#### Método Verlet



$$
x(t+\Delta t) = x(t) + v(t) \cdot \Delta t + \frac{1}{2} \cdot a \cdot \Delta t^{2}
$$
$$
v(t+\Delta t) = v(t) + a + \Delta t
$$
asumiendo $a$ constante, pero no siempre se puede tener pues la aceleración depende de la posición en algunos sistemas.
Haciendo una expansión de Taylor y sumando ambas ecuaciones:
$$
x(t+\Delta t) + x(t - \Delta t) = 2 \cdot x(t) + a(t) \cdot \Delta t^{2} + o(\Delta t^{4})
$$
y despejando, se tiene la **ecuación del método de Verlet**:
$$
x(t+\Delta t) = 2 \cdot x(t) - x(t - \Delta t) + a(t) \cdot \Delta t^{2}
$$
en donde:
- $x(t+\Delta t)$ es la nueva posición a calcular.
- $x(t)$ es la posición actualmente conocida.
- $x(t-\Delta t)$ es la posición previa conocida.
- $a(t)$ es la fuerza aplicada.
que permite calcular la posición futura en función de las dos posiciones anteriores: La actual y la anterior, sin depender directamente de la velocidad. Reescrito, de forma 'discreta':
$$
X_{N-1} = 2 \cdot X_{N} - X_{N-1} + f(X_{N},T) \cdot h^{2}
$$
implementandolo:
```py
aux = vertice.posicion

vertice.posicion = 2 * vertice.posicion - vertice.posicionPrevia \ + vertice.fuerza * delta_t * delta_t

vertice.posicionPrevia = aux

```

#### Variación: Velocity-Verlet

Se obtiene la posición siguiente en función de la posición y *velocidad* actual. Esto permite **obtener la velocidad**:
$$
x_{t+1} = x_{t} + v_{t} \cdot \Delta t + \frac{1}{2} \cdot f(X_{t}) \cdot \Delta t^{2}
$$
y la velocidad:
$$
v_{t+1} = v_{t} + \frac{f(x_{t}) + f(x_{t + 1})}{2} \cdot \Delta t
$$
las ecuaciones de van entregando la una a la otra la información que necesita pues la 1a necesita la velocidad actual y la 2a entrega la velocidad actual.