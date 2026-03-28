# Introducción a la Computación Gráfica

Una definición de computación gráfica es la **generación de imágenes desde escenas computacionales**, donde una escena computacional es la representación geométrica (en dos o tres dimensiones) de elementos dispuestos en un espacio.

En computación gráfica el programa *no es lineal*, a pesar de compartir la parte de inicialización y limpieza con un programa lineal. El programa tiene un bucle de ejecución potencialmente infinito y en cada bucle se tienen como mínimo tres acciones:
1. Se lee **interactividad** en la acción de un control, como el teclado o ratón.
2. Se **actualiza el estado del mundo** según al tiempo de ejecución y la interactividad.
3. Se **grafica el nuevo estado** del mundo usando shaders.

## Componentes

En general se tienen tres ejes a considerar: El modelo, la escena y el rendering.

1. **El modelo** corresponde a las geometrías que se quieren representar: Los objetos o el piso en donde se apoyan, por ejemplo.
2. **La escena** se define como el conjunto de elementos que aparecen posteriormente graficados en la imagen generada. Similar a una película, se disponen los elementos en una escena que se visualiza *a través de una cámara*. En esta se tienen **transformaciones** que se le aplican a los modelos para generar movimiento o para cambiar el tamaño de ellos (escalamiento).
3. El proceso de la generación de la imagen se llama **rendering**. En este contexto, se va a trabajar con el rendering en *tiempo real*, o sea el que se lleva a cabo *en el instante en que se interactúa con el sistema*. Un ejemplo evidente de esto son los videojuegos, a diferencia de una animación previamente renderizada, como una película.


# Modelo en Tres Dimensiones

Un modelo en tres dimensiones se compone de vértices, arcos y caras.

1. **Vértices**: Coordenadas en dónde se encuentra el punto en el espacio, entonces se relaciona con la forma $(x,y,z)$
2. **Arcos**: Depende de la implementación, pero típicamente Indica qué vertices se unen, de la forma $(v_{1},v_{2})$
3. **Caras**: También depende de la implementación, pero generalmente indica los vértices y arcos que la componen, como: $(v_{1},v_{2},v_{3}), (A_{1},A_{2},A_{3})$

Para generar movimiento se requiere *transformar* lo anterior, como por ejemplo, cambiar las coordenadas de los vértices.

## Objetos 3D

Al trabajar con modelos 3D, no se implementan en código sino que se trabajan con aplicaciones como *Blender*. Y se tienen distintos formatos para ellos como `.OFF`, `.PLY`, `.OBJ`, etc.

### Formato .OBJ

El formato `.OBJ` es un formato que almacena información de objetos 3D y es uno de los más simples.
Este formato utiliza los componentes:
--


# Python en Modelación Gráfica

En computación gráfica se suelen usar lenguajes compilados (como C++), pero se va a usar el lenguaje interpretado Python, que es lo suficientemente rápido y eficiente para propósito de estudios. Esto, pues las partes críticas de un programa, Python las implementa en el lenguaje de programación C.

## Módulos, Paquetes y Librerías

- En python, un módulo es un archivo `.py`.
- Un paquete es **una carpeta** que contiene módulos, en conjunto con un archivo especial de nombre `__init__.py`
- Una biblioteca es una colección de paquetes y módulos reutilizables.

### Módulos a Utilizar

Principalmente se van a usar:
1. `pyglet` para la gestión de ventanas, E/S (Entrada y salida e.g. teclado y mouse) y acceso a **OpenGL** para Python.
2. `numpy` para vectores, matrices y operaciones algebraicas.
3. `trimesh` para la carga y manipulación de mallas geométricas 3D.
4. `pymunk`: Simulación de física de cuerpos rígidos en 2D
5. `mesa` simulación basada en agentes
6. `grafica` un modulo propio del curso

#### Módulo grafica
El módulo `grafica` complementa `Pyglet` con herramientas que se van a desarrollar. Sus componentes principales son:
- `grafica.transformations`: matrices de transformación (traslación, rotación, escala) listas para usar con OpenGL.
- `grafica.scenegraph`: implementación de grafos de escena basada en networkx.
- `grafica.textures`: utilidades para cargar y gestionar texturas.
- `grafica.particle`: estructuras para simulación de partículas.
- `grafica.math`: funciones matemáticas auxiliares.
- `grafica.intersections`: pruebas de intersección geométrica.
- `grafica.arcball`: control de cámara interactivo mediante arcball.

## Estructuras a Utilizar

Con Python se tienen tres formas de almacenar un conjunto de información: [[Listas]], Tuplas, Conjuntos y [[Diccionarios]].

### Listas
Una lista es una secuencia *mutable* de longitud variable

### Tuplas

Una tupla es una secuencia *inmutable*. Usualmente se usan para representar valores que son conceptualmente una unidad y que no debiesen cambiar. Se usan para almacenar una coordenada, un color o un tamaño.

```py
# posicion: (x, y, z)
posicion = (0.5, -1.0, 0.0)

# color: (r, g, b)
color_rojo = (1.0, 0.0, 0.0)

# resolucion: (ancho, alto)
resolucion = (1280, 720)

```

### Arrays (Arreglos)

Los arrays o arreglos son parte de `Numpy`. (`nd.ndarray`). Son una colección de valores que corresponden **al mismo tipo numérico**, o sea una colección de `int` o `float`. Estos números se almacenan de forma compacta en la memoria, evitando acceder múltiples veces a la memoria al realizar operaciones. Son similares a las listas, pero tienen propiedades diferentes:
1. Los elementos dentro de un array **deben ser del mismo tipo de dato**. Hay casos en donde transforma los tipos de datos a uno en particular para que sean todos del mismo tipo.
2. Se pueden sumar los elementos directamente con los operadores matemáticos.
3. Los arrays son multidimensionales, así *se pueden tener vectores, matrices o tablas.*


```py
vertices = np.array([
	-1.0, -1.0, 0.0,
	 1.0, -1.0, 0.0,
	 1.0,  1.0, 0.0,
], dtype=np.foat32
```

El tipo de dato que almacena el array se indica con `dtype`. En GLSL (OpenGL Shading Language, el lenguaje en el que se va a trabajar) el tipo `float` es de $32$ bits y los tipos de datos que se usarán `vec3`, `mat4` y otros más, tienen esta precisión. Los arrays de *Numpy* utilizan `float64` por defecto y aunque la librería *Pyglet* se puede encargar de realizar la conversión de tipos desde un array a 32 bits, es buena práctica especificar el tipo `np.float32` al momento de crear las matrices.
\* La precisión de 32 bits es más que suficiente para el renderizado en tiempo real, pero es necesaria en simulaciones científicas por la acumulación de errores numéricos.


#### Diferencias con Listas

Para realizar un escalado de vértices, se deben multiplicar todas las componentes de una matriz por el factor. Esto en Python nativo se puede realizar mediante un ciclo `for` a cada elemento de la lista:
```py
vertices_escalados = []
for i in range(0, len(vertices), 3):
	vertices_escalados.append(vertices[i]   * 2.0)
	vertices_escalados.append(vertices[i+1] * 2.0)
	vertices_escalados.append(vertices[i+2] * 2.0)
```
mientras que con la librería Numpy, es mas simple pues el operador `*` opera sobre cada elemento del array:
```py
vertices_escalados = vertices * 2.0
```
por un lado es más corto y legible, y, por el otro lado, Numpy ejecuta la operación en el lenguaje C sobre todos los elementos a la vez. Esto es conveniente al trabajar con una cantidad grande de vértices.

Para multiplicar matrices, en Python:
```py
# Con listas anidadas y for:
resultado = [[sum(A[i][k] * B[k][j] for k in range(n)) for j in range(m)] for i in range(p)]

```
mientras tanto que Numpy implementa el operador `@`:
```py
resultado = A @ B
```


> Si se ve un ciclo `for` que recorre números haciendo aritmética, probablemente hay una implementación en Numpy más simple y eficiente.


### Conjuntos

Un conjunto se crea con `{}` e indicando los datos en su interior. Y cumplen propiedades similares a un conjunto matemático:
- Son semi-mutables: No se pueden modificar los elementos en su interior, pero *si* se pueden agregar o eliminar.
- No tienen un orden definido.
- No permiten valores duplicados.

Los conjuntos generalmente se utilizan para mantener un registro de los elementos disponibles en el mundo virtual que se estén graficando. Entonces tienen un uso mas en la lógica del mundo más que la implementación gráfica de este.

### Diccionarios

Un diccionario asocia llaves a valores. Útil para agrupar propiedades relacionadas bajo un nombre, evitando variables sueltas, o sea:
```py
material_color = (0.8, 0.2, 0.1)
material_shininess = 32.0
material_texture = None
```
pasa a ser:
```py
material = {
	"color":	(0.8, 0.2, 0.1),
	"shininess": 32.0,
	"texture":   None,
}
```
así se tiene un código más compacto. Y se usa, por ejemplo para mapear nombres a recursos ya cargados como *shaders* o texturas y representar propiedades de objetos de la escena antes de enviarlos a la GPU, comúnmente un diccionario se construye:
```py
texturas = {}
for nombre in ["ladrillo", "madera", "metal"]:
	texturas[nombre] = cargar_textura(f"assets/{nombre}.png")

# y luego
textura_activa = texturas["ladrillo"]
```

## Celdas y REPL

En Python es posible verificar un sector del código utilizando **celdas**. Las celdas son un bloque de código delimitado por el marcador `# %%` y estos bloques son detectados por editores de código como *Zed* o *VScode*, permitiendo ejecutar cada celda por separado. Así, se pueden verificar secciones del código para una mejor depuración.

```py
# %% Celda 1: Importaciones
import numpy as np
import grafica.transformations as tr

# %% Celda 2: Construir una matriz de rotación
R = tr.rotationZ(np.pi / 4)
print(R)

# %% Celda 3: Verificar que preserva la norma del vector
v = np.array([1.0, 0.0, 0.0, 1.0], dtype=np.float32)
v_rot = R @ v
print(f"norma: {np.linalg.norm(v_rot[:3]):.4f}") # debe ser ~1.0
```
cada celda se ejecuta de manera independiente: Se puede modificar y volver a ejecutar sin afectar lo anterior ni lo siguiente. Al corregir el fragmento, este queda guardado en el mismo archivo `.py`.

## Ecosistema de Python

Se van a usar *Numpy, Scipy y Networkx*.

- Numpy: Es una bibioteca numérica con arreglos, matrices y operaciones matemáticas.
- SciPy: Permite utilizar modelos estadísticos, funciones científicas, matrices dispersas, etc.
- Networkx: Para utilizar redes, objetos conectados con otros y la manera de recorrer tales objetos.

# Herramientas Gráficas

## APIs Gráficas

Las [[API]]s gráficas ofrecen operaciones para instrucciones que realizará la GPU, existen OpenGL, Vulkan, DirectX (de Microsoft), Metal (de Apple).

### OpenGL

Es una **especificación** de API para generar gráficos en la GPU. El propósito es *abstraer* la generación de modelos 3D. 

Nuevas implementaciones de operaciones en GPU que cumplan las especificaciones de OpenGL es una implementación de OpenGL, por ejemplo, en linux existe 'Mesa 3D'

> Una implementación de OpenGL solamente se encarga de la generación de gráficos, o sea solamente mostrar lo buscado en pantalla. Lo demás se realiza de forma externa con Qt, SDL o Pyglet.

OpenGL funciona como una máquina lineal que procesa las distintas partes de la escena, se dice que es una *máquina de los estados* de la escena. En donde el usuario configura su *estado actual* y los *parámetros que reciben* los estados.

#### Especificando Objetos
Los vértices contienen los atributos como `position` y `color` 
los índices indican cuáles vértices conforman cada triángulo.

```py
# definiendo datos para cada vertice
				# posiciones       colores
vertexData = [ -0.5, -0.5, 0.0, 1.0, 0.0, 0.0,
				0.5, -0.5, 0.0, 0.0, 1.0, 0.0,
				0.5, 0.5, 0.0, 0.0, 0.0, 1.0,
				-0.5, 0.5, 0.0, 1.0, 1.0, 1.0]

# es importante usar datos de 32bits
vertexData = np.array(vertexData, dtype = np.float32)

# definir conexiones entre vértices.
# Se tiene un triangulo por cada 3 índices seguidos.
índices = np.array([0, 1, 2,
					2, 3, 0], dtype = np.uint32)


```



#### Procesamiento (Estructura de Datos)

OpenGL opera con **vértices e índices** que, a bajo nivel, la información de estos elemtnos se almacena en *tres estructuras* llamadas *Vertex Buffer Object* (VBO), *Element Buffer Object* (EBO) y *Vertex Array Object* (VAO)

1. *Vertex Buffer Object* (**VBO**):
   Almacena los datos asociados a *cada vértice* en un bloque contiguo en la memoria. En la práctica **es solo una secuencia de números**. Por ejemplo, para un cuadrilátero:
   $$
   [\underbrace{ -1, -1 }_{ V_{0} }, \underbrace{ 1, -1 }_{ V_{1} }, \underbrace{ 1, 1 }_{ V_{2} }, \underbrace{ -1, 1 }_{ V_{3} }]
   $$
   así, cada vértice tiene su coordenada correspondiente.

2. *Element Buffer Object* (**EBO**):
   Contiene los **índices**, los cuales indican cómo se agrupan los vértices en el *VBO* en primitivas gráficas (o sea triángulos). Para el ejemplo anterior se tienen dos triángulos de índices
   $$
   [\underbrace{ 0, 1, 2 }_{ \text{Triangulo 1} }, \underbrace{ 2, 3, 0 }_{ \text{Triangulo 2} }]
   $$
   el primer triángulo ocupa los vértices $V_{0},V_{1},V_{2}$ y el segundo ocupa $V_{2}, V_{3},V_{0}$.
   Esta forma de organizar la información en índices permite reutilizarlos para otros triángulos.

3. *Vertex Array Object* (**VAO**):
   Le indica a OpenGL cómo interpretar los números del VBO, pues sin esta instrucción el VBO es una secuencia de float sin estructura deifnida. Un ejemplo es que dice '2 `float` consecutivos corresponden a un atributo `vec2 position`, u otro ejemplo es que los primeros dos float consecutivos son la posición y los siguientes tres son el color de tal vértice.
   
Esta estructura se puede visualizar de la forma:

![[Pasted image 20260328125824.png]]
y se puede observar que cada vértice tiene asociada información de su posición y color; Y, como es un arreglo de una dimensión, se debe saber la distancia entre vértices y, dentro de un vértice, entre su propia información (En el ejemplo: posición y color).

##### Implementación

```py
# El dato del vertice (Vertex Data) debe estar asociada a un VBO
glBindBuffer(GL_ARRAY_BUFFER, vbo)
glBufferData(GL_ARRAY_BUFFER, len(vertexData) * SIZE_IN_BYTES, vertexData, GL_STATIC_DRAW)

# Conexiones entre vértices son almacenadas en el EBO
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, ebo)
glBufferData(GL_ELEMENT_ARRAY_BUFFER, len(índices) * SIZE_IN_BYTES, índices, GL_STATIC_DRAW)

```

```py
# binding the proper buffers
glBindVertexArray(vao)
glBindBuffer(GL_ARRAY_BUFFER, vbo)
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, ebo)

# configurar donde se encuentran los datos de posición y color en el VBO
# un vertice tiene 3 enteros para cada posición (c/u de 4 bytes)
# y 3 enteros para el color (c/u de 4 bytes), por lo que 3*4 + 3*4 = 24 bytes

position = glGenAttribLocation( shaderProgram, "position")
glVertexAttribPointer(position, 3, GL_FLOAT, GL_FALSE, 24, ctypes.c_void_p(0))
glEnableVertexAttribArray(position)

color = glGenAttribLocation( shaderProgram, "color")
glVertexAttribPointer(color, 3, GL_FLOAT, GL_FALSE, 24, ctypes.c_void_p(12))
glEnableVertexAttribArray(color)

```




## pyglet

Pyglet es una biblioteca que *abstrae* parte de la funcionalidad de OpenGL con un esquema cercano a Python. 

## Trimesh

Trimesh una biblioteca que abstrae la carga y manipulación de modelos 3D. 

En particular, se va a utilizar la función `trimesh.load()` para cargar el objeto 3D al programa.




# Pipeline Gráfico

Un **pipeline** es la especificación de todos los *shaders* (en la práctica es la compilación de ellos) que se usarán para generar la imagen de un elemento. También se puede ver como *el orden* en que se ejecutan los programas necesarios para mostrar un modelo en pantalla.

![[Pasted image 20260325101717.png]]
implementado de la forma:

```py
# cargamos nuestros shaders (shaders básicos).
# el shader de vértices solo lee pos y color de cada vértice 
with open(Path(os.path.dirname(__file__)) / "vertex_program.glsl") as f:
	vertex_source_code = f.read()
# y el shader de píxeles solo lee el color del pixel
with open(Path(os.path.dirname(__file__)) / "fragment_program.glsl") as f:
	fragment_source_code = f.read()

vert_shader = pyglet.graphics.shader.Shader(vertex_source_code, "vertex")
frag_shader = pyglet.graphics.shader.Shader(fragment_source_code, "fragment")
pipeline = pyglet.graphics.shader.ShaderProgram(vert_shader, frag_shader)

```
con la variable `pipeline` se especifican los Shaders a utilizar.

El modelo se procesa de forma que:
1. Se discretiza en píxeles
2. Se pintan los píxeles

El pipeline consiste en:
1. *Vertex Shader*:
2. *Fragment Shader*:

## Shader Programs

Un **Shader** es un programa que permite procesar vértices, geometría y píxeles, generando así efectos gráficos. Estos programas se implementan en  lenguajes similar a *C*: *GLSL* si se utiliza OpenGL, o *HLSL* si se utiliza DirectX.

Cada programa requiere de parámetros de entrada y retorna parámetros u otra información asociada.

\* Un modelo no necesariamente se ve solo de un solo color, si no que puede tener sombras. La apariencia visual de los modelos se calcula y determina con los *shaders*.


### Vertex Shader

Es el programa que se ejecuta **en la etapa inicial del Pipeline**

El Vertex Shader **trabaja con los vértices del modelo**: Se encarga de manipular y definir sus atributos gráficos y entrega los píxeles que se van a pintar en la pantalla, de forma que **calcula la posición y los atributos de cada vértice**. Entre los atributos se tienen:
- Color
- Coordenadas de Texturas
- Vector Normal
y la posición resultante debe estar en coordenadas del volumen de vista.

Por ejemplo, se muestra un Shader básico que calcula la posición y los atributos de cada vértice de un modelo:
```C
vertex_shader = """
	#version 130
	in vec3 position;
	in vec3 color;
	
	out vec3 fragColor;
	
	void main()
	{
		fragColor = color;
		gl_Position = vec4(position, 1.0f)
	}
	"""
```
y se pueden identificar las secciones:

#### Parámetros

1. **Parámetros de Entrada**
```C
	in vec3 position;
	in vec3 color;
```
Se entregan al programa dos parámetros: Un parámetro de posición llamado `position` y otro de color denominado `color`. Además, ambos son especificados como vectores de tres dimensiones con `vec3`.

Con este proceso se indica que **cada vértice del modelo debe tener posición y color**.

2. **Parámetros de Salida**
```C
	out vec3 fragColor;
```
corresponde a la información que se envía al siguiente programa (el *Fragment Shader*) y, en este caso el resultado es **un color** en el vértice que se denomina `fragColor`.

3. **Función Principal (main)**

```C
	void main()
		{
			fragColor = color;
			gl_Position = vec4(position, 1.0f)
		}
```
en el proceso principal del *Vertex Shader* se observa que la variable `fragColor` que se entregará al siguiente programa es asignada directamente como el color que recibe `color`. O sea este *Vertex Shader* no le realiza ninguna modificación al color que recibe, simplemente lo entrega al siguiente programa.

Por otro lado, se tiene una variable que se calcula **obligatoriamente** en el *Vertex Shader*: La variable `gl_Position`, que corresponde a la posición final del vértice. Esta debe ser un **vector de 4 dimensiones** en donde las primeras tres componentes corresponden a la posición del vértice (en este caso no se modifica y se asigna directamente como la posición anterior `position`) y la cuarta componente corresponde a un `float` (por ahora).

\* La posición requiere un vector de 4 coordenadas pues es necesario para representar *coordenadas homogéneas*. La cuarta componente permite manejar transformaciones proyectivas.

### Fragment Shader

El *Fragment Shader* determina **el color** de cada píxel según los atributos del modelo. Específicamente, según los atributos de los vértices que rodean al píxel que se va a colorear.

Este *Shader* se ejecuta para cada píxel de cada objeto en la escena, o sea se ejecuta después del proceso de **rasterización**.
\* Puede que algunos píxeles queden fuera de la pantalla por haber *Shaders* a distinta profundidad o fuera de la zona de renderizado.

Por ejemplo, un *Fragment Shader* básico:
```C
vertex_shader = """

	#version 130
	in vec3 fragColor;
	
	out vec4 outColor;
	
	void main()
	{
		outColor = vec4(fragColor, 1.0f)
	}
	"""
```


#### Parámetros

1. **Parámetros de Entrada**:
En general, los parámetros de entrada son los atributos de los vértices, pero interpolados.
```C
	in vec3 fragColor;
```
En este caso el parámetro de entrada es la variable `fragColor` entregada por el Shader anterior, que corresponde al color del vértice.

2. **Parámetros de Salida**:
```C
	out vec4 outColor;
```
Y el resultado es la variable `outColor`, correspondiendo al **color del píxel** o incluso un píxel descartado. También puede generar información auxiliar que puede ser leída por otro Fragment Shader (por ej. un Fragment Shader de profundidad).

3. **Función Principal (main)**
```C
	void main()
	{
		outColor = vec4(fragColor, 1.0f);
	}
```
Dentro del programa se realizan los cálculos para realizar efectos de iluminación, de texturas, etc.

# Color

El color es la percepción del cerebro de un cierto rango de ondas electromagnéticas. Los humanos tienen su espectro visible entre los $400 \text{ y } 700 [nm]$ Conectando a Maxwell con la Termodinámica: *cada objeto alrededor produce color y su frecuencia es determinada por su temperatura*. Mediante la *generación de calor*, se puede emitir luz, y, dependiendo del material del que está construido el objeto, se tiene un cierto espectro de emisión: LED (frío o cálido), incandescente, halógeno, etc.

Con respescto al sistema visual: La luz que llega a los ojos atraviesa la córnea y el cristalino hasta llegar a la retina. En esta se encuentran fotorreceptores: los bastones. Estos se dividen en tres tipos, cada uno es sensible a diferentes regiones del espectro visible:
1. Tipo S: sensible a ondas cortas, tonalidades azules
2. Tipo M: Ondas medias, tonalidades verdes
3. Tipo L: Onda larga, tonalidades rojas.

## Modelos de Color
La descripción fundamental del color es la intensidad o absorción de la luz como *una función de la frecuencia de la onda.*

**El color que se observa es una mezcla de adiciones y sustracciones**. El color no es una propiedad intrínseca del objeto, sino el resultado de una interacción entre la fuente de luz, las propiedades del objeto y el sistema visual humano.

Un **modelo de color** es una representación matemática (de forma vectorial) de cómo se organizan los colores en un sistema.

### Modelo RGB
El modelo RGB es un modelo aditivo, compuesto de 3 colores:
1. Red
2. Gree
3. Blue

en donde un vector de la forma:
$$
\left( \begin{matrix}
R \\
G \\
B
\end{matrix} \right)
$$
contiene cada número $R,G,B$, con rangos que van, para tipo `int` entre los $[0,255]$, y en `float` en el rango $[0.0, 1.0]$. Los números indican cuánta contribución de cada color se tiene.

El modelo RGB se suele representa como un cubo, en donde cada vector de 3 dimensiones corresponde a un cierto color:
- El origen $(0,0,0)$ corresponde al negro.
- El vector $(255,255,255)$ corresponde al blanco

![[Pasted image 20260317091310.png]]
así, se tienen colores 'puros' en las esquinas.
> Una imagen corresponde a una combinación de la contribución de los colores rojo, azul y verde.


#### Pantallas
Las pantallas se componen de una grilla de píxeles. Cada píxel se compone de los tres colores R, G, B. Este recibe la información de la tupla $(R,G,B)$, indicando cuánta contribución de cada color emite el píxel.

### Modelo CMY(K)

El modelo CMY(K) es un **modelo sustractivo**. Funciona en base a *quitarle color* al fondo blanco, en donde cada color **bloquea** a su opuesto. El modelo se compone de los colores:
- Cyan
- Magenta
- Yellow
- Negro (opcional)

Estos colores son complementarios a los del modelo RGB.

### Modelo HSV

El modelo HSV es un modelo interpretable usado usualmente en diseño y psicología, y es representado usando coordenadas esféricas. Funciona en base a que, en vez de utilizar la cantidad de contribución de cada color, se definen:
1. **Hue**: El tono o color (percibible por el ojo humano) base en el arco circular de un cono, señalado como un *ángulo*
2. **Saturation**: Intensidad del color señalado, codificado como la *distancia desde el centro hasta el arco*.
3. **Value**: Señala el brillo, codificada como la *altura* del cono.

![[Pasted image 20260317091519.png]]

### Conversiones
#### RGB a HSV

Como RGB y HSV son cada uno la transformación del otro, se puede convertir un color entre ellos:

Sea $MAX$ el mayor valor de los componentes RGB y $MIN$ el menor valor, se tienen fórmulas **dependiendo qué color es el** $MAX$

$$
H = 
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
\left\{
	\begin{array}{ll}
		0\; , \text{si } MAX = 0\\
		1- \frac{MIN}{MAX}\; , \text{en otro caso }
	\end{array}
\right.
$$
$$
V = MAX
$$
se tiene un caso indefinido pues en el denominador de la fracción a realizar hay una diferencia entre $MAX$ y $MIN$ y como $MAX=MIN \implies MAX-MIN=0$, resultando en una división por $0$.


#### HSV a RGB
Se calculan las variables auxiliares;
$$
H_{i}=\left\lfloor  \frac{H}{60}  \right\rfloor  mod 6; H \leq 360
$$
$$
f=\left( \frac{H}{60} mod6 \right)- H_{i}
$$
$$
p=V (1-S)
$$
$$
q = V(1-f\cdot S)
$$
$$
t = V( 1-( 1 - f) \cdot S)
$$

Con esto, se tienen casos según el valor que tome $H_{i}$:
- 0, entonces: $R = V, G = t, B = p$
- 1, entonces: $R = q$, $G = V$, $B = p$
- 2, entonces: $R = p$, $G = V$, $B = t$
- 3, entonces: $R = p$, $G = p$, $B = V$
- 4, entonces: $R = t$, $G = p$, $B = V$
- 5, entonces: $R = V$, $G = p$, $B = q$

#### CMY(K) a RGB
$$

$$

## Interpolación de Colores (con RGB)

Al mostrar un objeto en la pantalla, no es práctico indicar el color para todos los píxeles.  Una alternativa es la *interpolación* de los colores de píxeles.

La interpolación corresponde a definir cuál es el color en dos puntos y utilizar una combinación lineal de los colores en los extremos, señalando la contribución de cada uno.
Se implementa señalando el color $C$ en un punto ubicado entremedio de dos puntos: inicial $P_{0}$ y final $P_{1}$, según:
$$
C = RGB_{P_{0}}\cdot(1-t) + RGB_{P_{1}}\cdot t
$$
en donde $t$ es un parámetro que señala la contribución de cada uno de los puntos en los extremos $P_{0}, P_{1}$.

Por ejemplo: Se puede tener un punto inicial completamente rojo $(255,0,0)$ y el final solamente verde $(0,255,0)$ y para un punto entre medio arbitrario, se elige un $t$ que indica la contribución de cada color.
`t = 0.5` se traduce en un color $(255,0,0)\cdot 0,5 + (0,255,0) * 0.5 =(127,127,0)$

## Canal Alfa

El canal o componente *alfa* corresponde a la **transparencia** de cada color. Las instrucciones de cada píxel necesita: 
- Rojo
- Verde
- Azul
- Alfa
cada uno entregado por 8 bits, dando un total de 32 bits para cada píxel.

## Representación de Imagenes

Una imagen se representa como una matriz de vectores RGB, en donde cada componente contiene la información de un píxel. Este modelo de representación de imágenes se conoce como **raster** (y por eso se conoce el proceso de 'mostrar algo' como *rastering*).

Entonces una imagen **raster** es un tipo de imagen que se compone de una cuadrícula de píxeles organizados en filas y columnas, y cumple que:
- Es de *resolución fija*. Entonces se pierde nitidez al hacer zoom.
- Como guarda información de todos los píxeles, es costoso en almacenamiento. Por ello, existen distintos formatos de compresión como JPG, PNG, BMP (sin compresión).
  \* JPG elimina la información de transparencia y a los colores muy cercanos los asigna como iguales.

## Representación Vectorial

Una *imagen vectorial* es una imagen que se compone de modelos paramétricos definidas por ecuaciones matemáticas. Esto permite escalar la imagen reevaluando las funciones según la resolución, por ello se dicen que estas imágenes tienen *resolución infinita*. *Por ejemplo:* SVG, EPS, PDF.

# Arquitectura

Para el proceso de imágenes en el computador, se tienen las componentes: Framebuffer, Video Controller


## Framebuffer

El *framebuffer* es el área de memoria que almacena la imagen.
En ocasiones se usan dos áreas de la memoria, lo que se conoce como doble-buffer, en donde un *framebuffer* se encarga del frame actual y el otro del frame siguiente, graficando el cuadro actual y modificando el siguiente.

## Video Controller

Accede al *framebuffer* para refrescar la pantalla. Este obtiene los valores de los píxeles durante un ciclo de refresco, típicamente son 60 cuadros por segundo.
Antiguamente el video controller contenía la paleta de colores que se iban a utilizar, pero las GPU modernas pueden calcular el color con un fragment shader.

## Especificar Colores

Para especificar colores, una forma es almacenarlos directamente en el *framebuffer*. *Por ejemplo*: Para un framebuffer de 3 bits se puede usar 1 bit para cada color (rojo, verde, azul) y así se pueden representar 8 colores.


| Código | Red | Green | Blue | Color Mostrado |
| ------ | --- | ----- | ---- | -------------- |
| 0      | 0   | 0     | 0    | Negro          |
| 1      | 0   | 0     | 1    | Azul           |
| 2      | 0   | 1     | 0    | Verde          |
| 3      | 0   | 1     | 1    | Cyan           |
| 4      | 1   | 0     | 0    | Rojo           |
| 5      | 1   | 0     | 1    | Magenta        |
| 6      | 1   | 1     | 0    | Amarillo       |
| 7      | 1   | 1     | 1    | Blanco         |


### Esquema Directo

El esquema directo corresponde a *utilizar más bits* para representar un mayor espectro de colores, almacenando directamente los colores, codificando 1 bit para cada componente RGB.
Querer mostrar un mayor espectro de colores es costoso en memoria.

*Por ejemplo* para pantallas de resolución 1920x1080, si para cada color se disponen 8 bits, se tendría $1920 \times 1980 = 3801600$ píxeles. Si para cada uno se usan 8 bits, entonces $3801600 \times 8 = 30412800$ bits, o sea $3.8016$ MB para una imagen. Entonces, si se usan 32 bits para cada color o si se tiene una pantalla de resolución $4K$ aumenta la memoria que se necesita.

### Esquema Indirecto

El esquema indirecto corresponde a almacenar los colores que se tienen disponibles en una *tabla separada*. Similar a una 'paleta de colores' para las imágenes que se van a mostrar. Aparte, **en el *framebuffer* se almacena un índice a un color**, indicando en qué píxeles de utilizan

Este esquema permite hacer modificaciones a lo que se muestra en pantalla de forma relativamente sencilla, al manipular los índices en el buffer para representar un cambio en los colores.

\*Este esquema se usaba en consolas hasta la Super Nintendo y permite dar la sensación de movimiento en una imagen al hacer variar los colores de forma cíclica.

# GPU

A fines de la década de los '80, las tarjetas gráficas cumplían funciones muy básicas: La comunicación entre el computador y el monitor, gestionar la imagen en la memoria y procesamiento de gráficos en 2D. Con el tiempo, se aumentó el poder de cómputo de estas unidades y se producen diversos chips, generando distintas bibliotecas, controladores, etc.
En el 1999 NVidia lanzó al mercado la tarjeta gráfica GeForce 256, que la definieron como la primera GPU ya que se propusieron estándares para estas unidades: Definen una GPU como un procesador único que integra transformaciones, configuración y recorte de triángulos, un motor de graficación (rendering) y la capacidad de procesas un mínimo de 10 millones de polígonos por segundo.

La definición moderna de GPU es:
La GPU (*Graphics Processing Unit*) es un co-procesador dedicado al procesamiento de gráficos u operaciones de coma flotante para aligerar la carga de trabajo de la CPU en aplicaciones como videojuegos o aplicaciones interactivas.

La GPU corresponde al *chip* central de procesamiento **dentro** de una tarjeta de video, es este caso es una GPU *discreta* o *dedicada*, o también este chip puede ser una parte dentro de la CPU, denominada como GPU *integrada*.

Una GPU tiene muchas más unidades de cómputo que una CPU, pero a cambio, se tiene un menor control en cuanto a lo que sucede en cada módulo. Si bien inicialmente se concebió como un apoyo a la CPU, se vio que pueden realizar muchas tareas en paralelo. En particular, para mostrar una imagen en pantalla interesan:
1. *Vertex Shader*: Realiza cálculos **sobre los vértices** de la escena
2. *Geometry Shader*: Opera **sobre los elementos** de la escena, generando vértices y primitivas (e.g: los triángulos).
3. *Fragment Shader*: **Pinta la escena** de acuerdo a al información de color.
4. Finalmente se pasa al frame-buffer (memoria) para luego mostrarlo en pantalla.
