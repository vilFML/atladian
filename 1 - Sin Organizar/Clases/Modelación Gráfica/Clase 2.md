# Color
El color es la percepción del cerebro de un cierto rango de ondas electromagnéticas. Los humanos tienen su espectro visible entre los $400 \text{ y } 700 [nm]$ 

## Calor
Mediante la generación de calor, se puede emitir luz.

Conectando a Maxwell con la Termodinámica: *cada objeto alrededor produce color y su frecuencia es determinada por su temperatura.*

Dependiendo del material del que está construido el objeto, se tiene un cierto espectro de emisión: LED (frío o cálido), incandescente, halógeno, etc.

## Modelo
La descripción fundamental del color es la intensidad o absorción de la luz como *una función de la frecuencia de la onda.*

**El color que se observa es una mezcla de adiciones y sustracciones**. El color no es una propiedad intrínseca del objeto, sino el resultado de una interacción entre la fuente de luz, las propiedades del objeto y el sistema visual humano.

## Sistema Visual
La luz que llega a los ojos, atraviesa la córnea y el cristalino hasta llegar a la retina. En esta se encuentran fotorreceptores: los bastones.
Los bastones se dividen en tres tipos. Cada uno es sensible a diferentes regiones del espectro visible.
1. Tipo S: sensible a ondas cortas, tonalidades azules
2. Tipo M: Ondas medias, tonalidades verdes
3. Tipo L: Onda larga, tonalidades rojas.


## Percepción
Si bien el cerebro recibe cierta información, este rellena la información que falta: Por ej, bajar la saturación del color de una frutilla, de igual manera el cerebro va a 'buscar' el color rojo de ellas.

# Modelos de Color
Es una representación matemática de cómo se organizan los colores en un sistema. Una presentación vectorial

## Modelo RGB
El modelo RGB es un modelo aditivo, compuesto de 3 colores:
1. Red
2. Gree
3. Blue
en donde un vector
$$
(\begin{matrix}
R \\
G \\
B
\end{matrix})
$$
en donde cada número $R,G,B$ corresponde a un `float` que indica cuánta contribución de cada color se desea.

El modelo RGB se suele representa como un cubo, en donde cada vector de 3 dimensiones corresponde a un cierto color:
- El origen $(0,0,0)$ corresponde al negro.
- El vector $(255,255,255)$ corresponde al blanco
![[Pasted image 20260317091310.png]]

Luego, una imagen corresponde a una combinación de la contribución de cada color Rojo, azul y verde.


### Pantallas
Las pantallas se componen de una grilla de pixeles. Cada pixel se compone de los 3 colores R, G, B. Este recibe la información de la tupla $(R,G,B)$ que indica cuánta contribución de cada color emite.

## Modelo CMY(K)
Modelo que utilizan las impresoras. Corresponde a *quitarle color* al fondo blanco, en donde cada color *bloquea* a su opuesto. 
Se componen de 
1. Cyan
2. Amarillo
3. Magente
4. Negro (Opcional)
los cuales son los colores complementarios a RGB

## Modelo HSV
Modelo interpretable usado en diseño y psicología, en donde representa usando coordenadas esféricas.
En vez de utilizar la cantidad de contribución de cada color, se definen:
1. **Hue**: El tono o color (percibible por el ojo humano) base en el arco circular de un cono, señalado como un *ángulo*
2. **Saturation**: Intensidad del color señalado, codificado como la *distancia desde el centro hasta el arco*.
3. **Value**: Señala el brillo, codificada como la *altura* del cono.

![[Pasted image 20260317091519.png]]


## Conversiones
### RGB a HSV

Como RGB y HSV son cada uno la transformación del otro, se puede convertir un color entre ellos:

Sea $MAX$ el mayor valor de los componentes RGB y $MIN$ el menor valor de los componentes RGB, se tienen fórmulas dependiendo se qué color es el $MAX$

$$
1_A(x) = 
\left\{
	\begin{array}{ll}
		\text{indef si }MAX = MIN \\
		60°\cdot \frac{G-B}{MAX-MIN}+0°, \text{si } MAX=R, G\geq B \\
		60°\cdot \frac{G-B}{MAX-MIN}+360°\text{si } MAX=R, G<B \\
		60° \cdot \frac{B-R}{MAX-MIN}+120°\text{si } MAX = G \\
		60° \cdot \frac{R-G}{MAX-MIN}+240°\text{si } MAX = B 
	\end{array}
\right.
$$
$$
S = 
1_A(x) = 
\left\{
	\begin{array}{ll}
		1\; , \text{si } x\in A \\
		0\; , \text{si } x\notin A
	\end{array}
\right.
$$
en el caso indefinido se tiene que $MAX=MIN$, entonces $MAX-MIN=0$ y se tendría una división por $0$.


### HSV a RGB
Se calculan las variables auxiliares;
$$
H_{i}= \left[ \frac{H}{60} \right] mod; H\leq 360
$$


### CMY(K) a RGB
$$

$$


# Interpolación de Colores

Al mostrar un objeto en la pantalla, no es muy práctico señalar cada color en absolutamente todos los puntos. Para evitar esto, se tiene la *interpolación* de colores.

Se define cuál es el color en dos puntos, y para los puntos entre medio se utiliza una combinación lineal de cada uno de los puntos en los extremos, señalando la contribución de estos dos puntos.

El color $C$ en un punto ubicado entremedio de dos puntos inicial $P_{0}$ y final $P_{1}$, se tiene según:
$$
C = RGB_{P_{0}}\cdot(1-t) + RGB_{P_{1}}\cdot t
$$
en donde $t$ es el parámetro que señala la contribución de cada uno de los puntos inicial $P_{0}$ y final $P_{1}$.

*Por ejemplo*, se puede tener un punto inicial completamente rojo $(255,0,0)$ y el final solamente verde $(0,255,0)$ y para un punto entre medio arbitrario, se elige un $t$ que indica la contribución de cada color.
`t = 0.5` se traduce en un color $(255,0,0)\cdot 0,5 + (0,255,0) * 0.5 =(127,127,0)$

# Canal Alfa
El componente *alfa* corresponde a la **transparencia** de cada color.

# Representación de Imagenes
Una imagen se representa como una matriz de vectores RGB. Este modelo se conoce como **raster** (y por eso se conoce el proceso de mostrar algo como *rastering*).

Una imagen **raster** es un tipo de imagen que se compone de una cudrícula de pixeles organizados en filas y columnas.
- Por ser de resolución fija, se pierde initidez al hacer zoom.
- Es costoso se almacenar pues se guarda la información de cada pixel. Por ello existen distintos formatos de compresión como JPG, PNG, BMP (sin compresión)

JPG elimina la información de transparencia y a los colores muy cercanos los asigna como iguales.

## Representación Vectorial
Son imagenes que compone de modelos paramétricos 