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
- $v$: Coordenadas de vértices
- $vt$: Coordenadas de texturas
- $vn$: Vectores normales
- $f$: Triángulos


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

## Python en Modelación Gráfica

En computación gráfica se suelen usar lenguajes compilados (como C++), pero se va a usar el lenguaje interpretado Python, que es lo suficientemente rápido y eficiente para propósito de estudios. Esto, pues las partes críticas de un programa, Python las implementa en el lenguaje de programación C.

### Módulos, Paquetes y Librerías

- En python, un módulo es un archivo `.py`.
- Un paquete es **una carpeta** que contiene módulos, en conjunto con un archivo especial de nombre `__init__.py`
- Una biblioteca es una colección de paquetes y módulos reutilizables.

#### Módulos a Utilizar

Principalmente se van a usar:
1. `pyglet` para la gestión de ventanas, E/S (Entrada y salida e.g. teclado y mouse) y acceso a **OpenGL** para Python.
2. `numpy` para vectores, matrices y operaciones algebraicas.
3. `trimesh` para la carga y manipulación de mallas geométricas 3D.
4. `pymunk`: Simulación de física de cuerpos rígidos en 2D
5. `mesa` simulación basada en agentes
6. `grafica` un modulo propio del curso

##### Módulo grafica
El módulo `grafica` complementa `Pyglet` con herramientas que se van a desarrollar. Sus componentes principales son:
- `grafica.transformations`: matrices de transformación (traslación, rotación, escala) listas para usar con OpenGL.
- `grafica.scenegraph`: implementación de grafos de escena basada en networkx.
- `grafica.textures`: utilidades para cargar y gestionar texturas.
- `grafica.particle`: estructuras para simulación de partículas.
- `grafica.math`: funciones matemáticas auxiliares.
- `grafica.intersections`: pruebas de intersección geométrica.
- `grafica.arcball`: control de cámara interactivo mediante arcball.

##### Pyglet

Pyglet es una biblioteca que *abstrae* parte de la funcionalidad de OpenGL con un esquema cercano a Python. 

##### Trimesh

Trimesh una biblioteca que abstrae la carga y manipulación de modelos 3D. 

En particular, se va a utilizar la función `trimesh.load()` para cargar el objeto 3D al programa.

### Estructuras a Utilizar

Con Python se tienen tres formas de almacenar un conjunto de información: [[Listas]], Tuplas, Conjuntos y [[Diccionarios]].

#### Listas
Una lista es una secuencia *mutable* de longitud variable

#### Tuplas

Una tupla es una secuencia *inmutable*. Usualmente se usan para representar valores que son conceptualmente una unidad y que no debiesen cambiar. Se usan para almacenar una coordenada, un color o un tamaño.

```py
# posicion: (x, y, z)
posicion = (0.5, -1.0, 0.0)

# color: (r, g, b)
color_rojo = (1.0, 0.0, 0.0)

# resolucion: (ancho, alto)
resolucion = (1280, 720)

```

#### Arrays (Arreglos)

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


##### Diferencias con Listas

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


#### Conjuntos

Un conjunto se crea con `{}` e indicando los datos en su interior. Y cumplen propiedades similares a un conjunto matemático:
- Son semi-mutables: No se pueden modificar los elementos en su interior, pero *si* se pueden agregar o eliminar.
- No tienen un orden definido.
- No permiten valores duplicados.

Los conjuntos generalmente se utilizan para mantener un registro de los elementos disponibles en el mundo virtual que se estén graficando. Entonces tienen un uso mas en la lógica del mundo más que la implementación gráfica de este.

#### Diccionarios

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

### Celdas y REPL

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

### Ecosistema de Python

Se van a usar *Numpy, Scipy y Networkx*.

- Numpy: Es una bibioteca numérica con arreglos, matrices y operaciones matemáticas.
- SciPy: Permite utilizar modelos estadísticos, funciones científicas, matrices dispersas, etc.
- Networkx: Para utilizar redes, objetos conectados con otros y la manera de recorrer tales objetos.










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

Cada color del CMY(K) es el complementario a un color en RGB. Entonces para cada color que se tiene de CMY, corresponde a la cantidad *que falta* de uno en RGB
- Cyan es el opuesto del Rojo
- Magenta el opuesto de Verde
- Amarillo el opuesto de Azul
entonces las fórmulas para cada uno serían:
$$
\begin{array}
aC = 1-R \\
M = 1 - G \\
Y = 1 - B
\end{array}
$$
Por otro lado, se determina **K** como el valor de *oscuridad común*, lo que corresponde a la cantidad de negro implícita en los tres canales. Esto se puede ver como que **la cantidad de negro (de base) es el mínimo entre los tres colores**:
$$
K = min(C',M',Y')\iff K = min(1-R, 1-G, 1-B)
$$
Por último se debe *normalizar* los valores entre $[0,1]$, ajustando los valores a la nueva escala.
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

## Representación de Imágenes


Una imagen digital es una colección estructurada de colores organizados en una cuadrícula bidimensional. Cada celda corresponde a un píxel, el que contiene la información de color específica para su ubicación en la pantalla. 
Se va a utilizar una matriz de vectores RGB, en donde cada componente contiene la información de un píxel, con la posibilidad de agregar una cuarta componente para la transparencia (el canal alfa).
Formalmente, de define un color en el espacio RGB como un vector de tres dimensiones, o sea:
$$
\text{Color}_{\text{RGB}}=(r,g,b)\in[0,1]^{3}
$$
y si se incluye el canal alfa para la transparencia:
$$
\text{Color}_{RGBA}=(r,g,b,\alpha)\in[0,1]^{4}
$$
donde cada componente $r,g,b,\alpha \in \mathbb{R}$ y, en la práctica son valores `float` entre 0 y 1, o también pueden ser `int` tomando valores entre 0 y 255.

Una imagen, formalmente se define como una matriz tridimensional, de la forma:
$$
I\in[0,1]^{n\times m\times c}
$$
donde $n$ es el número de filas (como la altura de la imagen), $m$ es el número de columnas (ancho) y $c$ es el número de *canales* de cada píxel (3 o 4 si se incluye la transparencia).

- La **resolución** de la imagen corresponde a un valor $r = n\times m$, que indica el número total de celdas (píxeles) que compone la imagen.

- Para el almacenamiento en memoria, depende de si se incluye la transparencia:
  $$
  \text{Tmñ}(\text{Color}_{\text{RGB}}) = 4\cdot\text{Tmñ}(float) = 4\cdot4=16 \text{ bytes}
  $$
  o si no se incluye:
  $$
  \text{Tmñ}(\text{Color}_{\text{RGB}}) = 3\cdot\text{Tmñ}(float) = 3\cdot4=12 \text{ bytes}
  $$


### Modelo *raster*

Representar imágenes como una matriz de píxeles se conoce como **raster**, y por eso se conoce el proceso de 'mostrar algo' como *rastering*. Un **raster** es un tipo de imagen que se compone de una cuadrícula de píxeles organizados en filas y columnas, y cumple que:
- Es de *resolución fija*. Entonces se pierde nitidez al hacer zoom.
- Como guarda información de todos los píxeles, es costoso en almacenamiento. Por ello, existen distintos formatos de compresión como JPG, PNG, BMP (sin compresión).
  \* JPG elimina la información de transparencia y a los colores muy cercanos los asigna como iguales.
Las imágenes *raster* son ideales para fotografías y contenido con detalles complejos.

### Modelo Vectorial

Una *imagen vectorial* es una imagen que se compone de modelos paramétricos definidas por ecuaciones matemáticas: líneas, curvas, polígonos y sus propiedades. Esto permite escalar la imagen reevaluando las funciones según la resolución, por ello se dicen que estas imágenes tienen *resolución infinita*. 
A diferencia de las imágenes *raster*, el peso de un archivo depende de la complejidad de los modelos paramétricos y no de las dimensinoes de la imagen. *Por ejemplo:* SVG, EPS, PDF.
El modelo vectorial es usado en ilustraciones, tipografía, diagramas y cualquier gráfico que requiera precisión o escalabilidad. 


## Arquitectura

El proceso por el que pasan los datos de una imagen hasta que se muestra en pantalla requiere de una arquitectura específica. Entre otros, se tienen los componentes: Framebuffer, Video Controller.


### Frame Buffer

En el núcleo del procesamiento se encuentra el *Frame Buffer*, que corresponde a una región de memoria dedicada a almacenar la representación de la imagen que se va a mostrar en pantalla finalmente y cada celda de esta memoria contiene la información de un píxel: color y transparencia.
En sistemas modernos este *buffer* se encuentra en la memoria visual (VRAM) dentro de la tarjeta de video.

En ocasiones se usan dos áreas de la memoria (o incluso tres):
1. El *front buffer* dedicado a la imagen que se está mostrando.
2. El *back buffer* dedicado al siguiente cuadro.
esta técnica se llama *page flipping* y provee una visualización fluida.
\* El *tearing* sucede cuando se modifica el buffer que se está mostrando actualmente.



### Video Controller

Como interfaz entre el contenido del *frame buffer* y la pantalla se tiene el controlador de video (*video controller*). Este lee la memoria *buffer* y lo envía a la pantalla, realizando la conversión de los datos digitales a las señales requeridas por las tecnologías de pantalla (LCD,OLED, etc.), además de los estándares de conexión (HDMI, DisplayPort, etc.). 
El controlador de vídeo realiza el procesamiento una frecuencia específica, medida en cuadros por segundo *FPS* o Hertz $[Hz]$ . Usualmente son 60 cuadros por segundo, aunque en aplicaciones que se requiera una mejor respuesta y baja latencia se aumenta a $120[Hz],144[Hz],240[Hz]$.
Antiguamente el video controller contenía la paleta de colores que se iban a utilizar, pero las GPU modernas pueden calcular el color con un fragment shader.

### Fragment Program

Un *fragment program* (o *pixel shader* en DirectX) es un tipo de programa ejecutado en la GPU para cada píxel (o fragmento) de la imagen. Este determina el color final de cada píxel según parámetros de escena, configuración y la estética deseada.
Los *fragment program* son parte de un pipeline más amplio de renderización: la *rendering pipeline*.

### Especificar Colores

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


#### Esquema Directo

El esquema directo corresponde a *utilizar más bits* para representar un mayor espectro de colores, almacenando directamente los colores, codificando 1 bit para cada componente RGB.
Querer mostrar un mayor espectro de colores es costoso en memoria.

*Por ejemplo* para pantallas de resolución 1920x1080, si para cada color se disponen 8 bits, se tendría $1920 \times 1980 = 3801600$ píxeles. Si para cada uno se usan 8 bits, entonces $3801600 \times 8 = 30412800$ bits, o sea $3.8016$ MB para una imagen. Entonces, si se usan 32 bits para cada color o si se tiene una pantalla de resolución $4K$ aumenta la memoria que se necesita.

#### Esquema Indirecto

El esquema indirecto corresponde a almacenar los colores que se tienen disponibles en una *tabla separada*. Similar a una 'paleta de colores' para las imágenes que se van a mostrar. Aparte, **en el *framebuffer* se almacena un índice a un color**, indicando en qué píxeles de utilizan

Este esquema permite hacer modificaciones a lo que se muestra en pantalla de forma relativamente sencilla, al manipular los índices en el buffer para representar un cambio en los colores.

\*Este esquema se usaba en consolas hasta la Super Nintendo y permite dar la sensación de movimiento en una imagen al hacer variar los colores de forma cíclica.

# GPU

A fines de la década de los '80, las tarjetas gráficas cumplían funciones muy básicas: La comunicación entre el computador y el monitor, gestionar la imagen en la memoria y procesamiento de gráficos en 2D. Con el tiempo, se aumentó el poder de cómputo de estas unidades y se producen diversos chips, generando distintas bibliotecas, controladores, etc.
En el 1999 NVidia lanzó al mercado la tarjeta gráfica GeForce 256, que la definieron como la primera GPU ya que se propusieron estándares para estas unidades: Definen una GPU como un procesador único que integra transformaciones, configuración y recorte de triángulos, un motor de graficación (rendering) y la capacidad de procesas un mínimo de 10 millones de polígonos por segundo.

> La **definición** moderna de GPU es: La GPU (*Graphics Processing Unit*) es un co-procesador dedicado al procesamiento de gráficos u operaciones de coma flotante para aligerar la carga de trabajo de la CPU en aplicaciones como videojuegos o aplicaciones interactivas.

La GPU corresponde al *chip* central de procesamiento **dentro** de una tarjeta de video, es este caso es una GPU *discreta* o *dedicada*, o también este chip puede ser una parte dentro de la CPU, denominada como GPU *integrada*.

Los chips GPU de primera generación operaban con una *pipeline* fija. O sea, los procesos que se requerían para mostrar la imagen en pantalla no se podían modificar. Las GPU modernas cuentan con co-procesadores no modificables para algunas operaciones gráficas (como el *rastering*), pero la mayor parte de sus operaciones son programables.

Una GPU tiene muchas más unidades de cómputo que una CPU, pero a cambio, se tiene un menor control en cuanto a lo que sucede en cada módulo. Si bien inicialmente se concebió como un apoyo a la CPU, se vio que pueden realizar muchas tareas en paralelo. En particular, para mostrar una imagen en pantalla interesan:
1. *Vertex Shader*: Realiza cálculos **sobre los vértices** de la escena
2. *Geometry Shader*: Opera **sobre los elementos** de la escena, generando vértices y primitivas (e.g: los triángulos).
3. *Fragment Shader*: **Pinta la escena** de acuerdo a al información de color.
4. Finalmente se pasa al frame-buffer (memoria) para luego mostrarlo en pantalla.

##### Diferencia con CPU

Para entender la diferencia entre GPU y CPU es útil examinar las componentes internas de cada una. Ambas comparten componentes pero las tienen en distintas proporciones:
1. **Core (Núcleo)**: Corresponde a la unidad que ejecuta instrucciones y realiza cálculos aritméticos. Dependiendo de su complejidad puede realizar operaciones más o menos básicos.
2. **Unidad de Control**: Componente que coordina la ejecución de instrucciones dentro de un núcleo: Qué operación, el orden y gestiona el flujo del programa (por ejemplo las instrucciones condicionales). Si se soportan instrucciones más complejas, el núcleo se concentra al control aún mas.
3. **Caché**: Memoria de poca capacidad pero de mucha velocidad que almacena datos de acceso frecuente. Más caché permite reutlizar datos sin tener que buscarlos en la memoria principal y se organiza según *L1, L2, L3* donde *L1* es la más rápida, pero de menor capacidad y *L3* es lo contrario.
4. **Memoria (DRAM)**: Unidad de almacenamiento principal de datos. Para una CPU, corresponde a la RAM usual del sistema y para GPU la RAM visual (o VRAM).

Las diferencias se pueden ver en la siguiente tabla:

| Componente          | CPU                                   | GPU                                                       |
| ------------------- | ------------------------------------- | --------------------------------------------------------- |
| *Cores*             | Pocos, grandes y complejos            | Muchos, pequeños y simples                                |
| Unidad de Control   | Grande, dedicada a cada núcleo        | Mínima, controla muchos núcleos                           |
| Memoria *Caché*     | Posee los tres niveles *L1, L2, L3*   | Solo tiene *L2*                                           |
| Memoria RAM         | RAM del sistema                       | RAM dedicada (o del sistema si GPU es integrada)          |
| Modelo de Operación | Variedad de tareas en paralelo (MIMD) | Una misma operación sobre muchos datos en paralelo (SIMD) |
Una CPU es un **procesador generalista**: Tiene pocos núcleos, pero ejecuta instrucciones variadas y complejas independientemente (Modelo MIMD); múltiples niveles de caché permiten mejor gestión y ramificación de procesos. 
Una GPU aplica las mismas instrucciones a múltiples datos simultáneamente, por ello le es útil tener muchos núcleos, una unidad de control mínima y reducida memoria caché. Esta arquitectura permite procesar millones de polígonos por segundo, necesario para aplicaciones 3D.

## Rendering

La renderización es parte un procesamiento secuencial llamado *rendering pipeline*, en la cual cada componente procesa la información y se transmite al siguiente. En general, se tienen los procesos de:
1. Aplicación
2. Procesamiento Geométrico
3. Recorte
4. Rasterización
5. Procesamiento de Píxeles
también se pueden incluir el controlador de video y el procesamiento de señal en el monitor.

El punto de partida del *pipeline* es una escena. *Por ejemplo*: La *Caja de Cornell*: Contiene múltiples objetos con propiedades específicas y una fuente de luz.

1. **Aplicación**: Es la etapa que se encarga de la construcción, actualización y de mantener el mundo virtual renderizado. Realiza simulaciones, captura entradas del sistema, monitorea el estado de la red y otras tareas.
Cuando la etapa de aplicación construye la escena, esta es transmitida a la GPU como una lista de primitivas gráficas: puntos, líneas y triángulos, siendo esta última la primitiva fundamental. La GPU realiza cálculos geométricos sobre los vértices con los [[#Shader Programs]]
2. **Rasterización**: Convierte los triángulos dentro del volumen de visión en píxeles y, en general, no es programable.
3. **Procesamiento de Píxeles**: Determina el color correspondiente a cada píxel, según sea visible o no en la imagen final; El proceso se realiza según los atributos del triángulo y su iluminación.


# Workflow

Pyglet permite abstraer el proceso de generación de imágenes, ya que *Trimesh* se encarga de cargar y preparar los datos en un formato adecuado para entregarlos a OpenGL.
En específico, se tiene la lista de $v,vt$ etc. que se convierte a un formato compatible con OpenGL y *Pyglet* se encarga de gestionar y graficar dichos datos.

Se tienen las funciones:
- `load()`que entrega el modelo al programa.
-  `rendering.mesh_to_vertexlist()` entrega la información de la malla como una lista de elementos con diversa información del modelo (como los vértices, los triángulos que forman, etc.)

##### Ejemplo

```py
bunny = tm.load("assets/Stanford_Bunny.stl")
bunny_vertex_list = tm.rendering.mesh_to_vertexlist(bunny)

nvertices = bunny_vertex_list[0]
vertices_index = bunny_vertex_list[3]
vertices_coord = bunny_vertex_list[4][1]

bunny_gpu = pipeline.vertex_list_indexed
	(
		nvertices,
		GL.GL_TRIANGLES,
		vertices_index
	)
	
bunny_gpu.position[:] = vertices_coord
```
en donde:
```py
nvertices = bunny_vertex_list[0]
vertices_index = bunny_vertex_list[3]
vertices_coord = bunny_vertex_list[4][1]
```
respectivamente, se extraen los datos que se necesita de la malla:
- La cantidad de vértices
- Las triadas de índices de los vértices que conforman un triángulo
- El listado de coordenadas $(x,y,z)$ de cada vértice.
\* Recordar que los datos son entregados por trimesh y estos estan en un arreglo unidimensional para OpenGL

```py
bunny_gpu = pipeline.vertex_list_indexed
	(
		nvertices,
		GL.GL_TRIANGLES,
		vertices_index
	)
```
se reserva el espacio en la GPU. Para ello se indica, respectivamente:
- La cantidad total de vértices
- El modo de dibujo (`GL.GL_TRIANGLES`)
- El listado de índices de vértices que conforman los triángulos.

```py
bunny_gpu.position[:] = vertices_coord
```
finalmente, se asigna el listado de vértices $(x,y,z)$ a la posición dentro del pipeline.

Eventualmente dentro del *gameloop*, se activa el pipeline e indica que se dibuje el conejo.
```py
pipeline.use()
bunny_gpu.draw(GL.GL_TRIANGLES)
```


## Dibujando en OpenGL

Se tienen distintas formas de graficar triángulos en OpenGL. Usualmente se trabaja con `GL_TRIANGLES`, pero existen se tienen otros modos que pueden ser ventajosos para otros casos.

```py
glBindVertexArray(vao)
glDrawElements(GL_TRIANGLES, len(indices), GL_UNSIGNED_INT, None)
```

# Animación Basada en la Física

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
Las fuerzas dependen de la posición, tiempo y velocidad. Y algunas fuerzas son la de gravedad, resortes, viscosidad, resistencia del viento, etc.

> Para masas puntuales, las fuerzas son vectores

### Fuerza de Gravedad

Para modelar la gravedad, se tiene solamente una dependencia de la *masa* de la partícula. Luego, $f(X,t)$ es una constante, y de forma vectorial, la fuerza que se le ejerce a la $i$ésima partícula es:
$$
f_{i}=
\left( \begin{matrix}
0 \\
0 \\
-m_{i}\cdot g
\end{matrix} \right)
$$



\* El humo se puede modelar como partículas con la gravedad invertida.

## Esquema de Trabajo

El esquema usual de los programas que modelan partículas sigue un orden, generalmente:
1. Creación
2. Actualización

### Creación

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
en el código, el ciclo `for` se encarga de:
- Crea las partículas en una posición determinada $(0,0,0)$
- Tanto en $x$ como en $y$ no se aplica ninguna velocidad en el inicio. Pero sí se aplica una velocidad en $z$.
- Además, con la función `random()` se agrega una aleatoriedad en las otras direcciones $x,y$.

### Actualización

Se actualiza la posición de las partículas por cada *frame*. Para cada cuadro se tiene un intervalo infinitesimal $dt$:
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
se espera que el $dt$ sea constante: En cada $dt$ la partícula sigue una trayectoria tangente, que se actualiza luego de terminar $dt$

Se debe notar que en la modificación de color se está modificando la cuarta componente del array: $(R,G,B,A)$, osea $A$ que corresponde a la transparencia. Cada vez es más transparente y cuando tenga una transparencia tal que la partícula no se ve en pantalla, el `if` destruye la partícula.

## Ecuaciones Diferenciales Ordinarias (EDO)

En computación gráfica, las EDOs de interés describen el movimiento de partículas bajo fuerzas.
Como se va a trabajar con fuerzas, se va a trabajar con 
$$
\vec{F}=m\vec{a} \iff \vec{F}=m \frac{d^{2}\vec{x}}{dt^{2}}
$$
donde $\vec{x},\vec{F}$ son vectores; $\vec{F},m$ son conocidos (para $m$, la partícula es una masa puntual) y **se quiere resolver la ecuación para** $\vec{x}$, así, se tiene una Ecuación de Segundo Orden.
Para reducir la ecuación diferencial, se puede usar que la primera derivada de la posición es la velocidad y la segunda derivada de la posición, o sea la derivada de la velocidad es la fuerza dividida en la masa.
$$
\implies 
\left\{
	\begin{array}{ll}
		\frac{ d \vec{x} }{ d t } =\vec{v} \\
		\frac{ d \vec{v} }{ d t } = \frac{\vec{F}}{m}
	\end{array}
\right.
$$
esto es útil pues resolver sistemas mayores a uno es complejo.

## Métodos de Integración Numérica

La mayoría de las ecuaciones diferenciales que se tienen en la realidad no tienen soluciones analíticas exactas. Para trabajar con ellas se va a usar la *integración numérica*, que aproximan soluciones con métodos iterativos: No se predice la posición de una partícula en un tiempo arbitrario usando cierta expresión, si no que se calcula la siguiente posición (en el cuadro siguiente) pues sí se conoce el cambio. Y a partir de ese instante, se obtiene el siguiente y así sucesivamente, para pequeños instantes de tiempo $dt$, conocido como paso temporal.

Resolver sistemas de primer orden no es siempre sencillo, pero se tienen maneras conocidas para resolver. Luego, al derivar $f$:
$$
f(X,t)= \frac{ d x }{ d t }=\frac{ d  }{ d t } \left( \begin{matrix}
\vec{x} \\
\vec{v}
\end{matrix} \right) = 
\left( \begin{matrix}
\vec{v} \\
\frac{\vec{F}(x,v)}{m}
\end{matrix} \right)
$$
Esto se puede extender para $N$ masas, **apilando los vectores $x$ y $\vec{v}$ en un solo vector** de tamaño 6N:
$$
X = \left( \begin{matrix}
x_{1} \\
v_{1} \\
\dots \\
x_{N} \\
v_{N}
\end{matrix} \right)
;\ 
f(X,t)=
\left( \begin{matrix}
v_{1} \\
F_{1}(X,t) \\
\vdots \\
v_{N} \\
F_{N}(X,t)
\end{matrix} \right)
$$
con $x_{1},v_{1}$ es la información de la partícula 1, y así para las siguientes.

La fuerza sobre la partícula $i$ es dependiente de $X$, entonces esta considera la información de todas las partículas para calcular las fuerzas sobre la partícula $i$ésima. Si las partículas no interactúan entre sí, entonces $F_{i}$ solo depende de la posición y de la velocidad de la misma partícula.

La trayectoria de una partícula se puede modelar con
$$
\frac{dX(t)}{dt}=f(x(t),t)
$$
con $\frac{dX(t)}{dt}$ el desplazamiento, y la fuerza $f$ es dependiente de la posición $X(t)$ y del tiempo $t$.

Luego, dada una función $f(X(t),t)$, la idea es computar $X(t)$. Para ello se requiere una posición inicial $X(T=0)$ y tener valores $X(t)$ conocidos para $t >t_{0}$

### Interpretación

La interpretación es que $X(t)$ indica **el camino a seguir** en un espacio, pues esta responde a la pregunta: ¿Dónde estará $X$ después de un intervalo de tiempo infinitesimal $dt$? Los diagramas se pueden interpretar como una 'foto' en el tiempo de las posiciones de la partícula, y $f=\frac{ d X }{ d t }$ es un vector que, en cada punto del espacio de fase, apunta en la dirección deseada.

### Método de Euler

Este método es el más simple para resolver una EDO de forma numérica.
Dada una EDO
$$
\frac{ d y }{ d t } = f(t,y)
$$
con condición inicial $y(t_{0})=y_{0}$. Y la fórmula de iteración (o actualización por cuadro) es:
$$
y_{n+1}=y_{n}+h\cdot f(t_{n},y_{n})
$$

Donde $h$ es el tamaño del paso temporal y $t_{n+1}=t_{n}+h$. Esta fórmula proviene de la aproximación lineal de la serie de Taylor.
Este modelo corresponde a una aproximación por piezas del camino. La idea es caminar por las tangentes de la curva y el tamaño de $h$ controla la precisión de la aproximación (o trayectoria del movimiento), de forma que un paso más pequeño está dado por un menor valor de $h$:
![[Pasted image 20260326093353.png]]
desde abajo hacia arriba se incrementó la precisión al reducir el valor de $h$

**La implementación** de un paso de Euler se reduce a:
```py
def euler_step(f, t, y, h):
	return y + h * f(t, y)
```
pero se tiene un costo, pues el método acumula error. Además el método no conserva energía ni momento.

\* El método de euler no representa un círculo, si  no que una espiral, pues se basa en la tangente.
### Método Runge-Kutta de 4° Orden (RK4)

El método *RK4* evalúa la derivada en cuatro puntos diferentes para cada paso de la integración.
Para una EDO de la forma:
$$
\frac{ d y }{ d t } = f(t,y)
$$
la fórmula *RK4* es:
$$
\begin{array}{ll}
k_{1}=f(t_{n},y_{n}) \\
k_{2}=f\left( t_{n}+\frac{h}{2}, y_{n}+\frac{h}{2}k_{1} \right) \\
k_{3}=f\left( t_{n}+\frac{h}{2},y_{n}+\frac{h}{2}k_{2} \right) \\
k_{4}=f(t_{n}+h, y_{n}+hk_{3}) \\
y_{n+1}=y_{n}+ \frac{h}{6}(k_{1}+2k_{2}+2k_{3}+k_{4})

\end{array}
$$
donde cada $k_{i}$ evalúa la función en diferentes posiciones: $k_{1}$ al inicio, $k_{4}$ al final y $k_{2},k_{3}$ en los pasos intermedios. Y el **valor final es un promedio ponderado de estas evaluacoines**.
Este método evalúa mejor que el método de Euler (bajo el mismo paso de tiempo), pero tiene un mayor costo computacional.

El método *RK4* recalcula la pendiente desde cada punto para ir, efectivamente, al punto final.

### Método Verlet

Este método se centra en la integración de la posición sin calcular la velocidad.
De las ecuaciones cinemáticas de movimiento, se tiene que:
$$
x(t+\Delta t) = x(t) + v(t) \cdot \Delta t + \frac{1}{2} \cdot a \cdot \Delta t^{2}
$$
$$
v(t+\Delta t) = v(t) + a \cdot \Delta t
$$
en donde se asume una aceleración $a$ constante. Puede ser que no siempre se tenga pues en algunos sistemas la aceleración depende de la posición (e.g. un resorte).
Haciendo una expansión de Taylor y sumando ambas ecuaciones:
$$
x(t+\Delta t) + x(t - \Delta t) = 2 \cdot x(t) + a(t) \cdot \Delta t^{2} + o(\Delta t^{4})
$$
y despejando para la posición siguiente $x(t+\Delta t)$, se tiene la **ecuación del método de Verlet**:
$$
x(t+\Delta t) = 2 \cdot x(t) - x(t - \Delta t) + a(t) \cdot \Delta t^{2}
$$
en donde:
- $x(t+\Delta t)$ es la nueva posición a calcular.
- $x(t)$ es la posición actualmente conocida.
- $x(t-\Delta t)$ es la posición previa conocida.
- $a(t)$ es la fuerza aplicada.
La ecuación de Verlet permite calcular la posición siguiente de la partícula en función de las dos posiciones anteriores: La actual y la anterior, sin depender directamente de la velocidad. 
Reescribiendo la ecuación de forma "discreta":
$$
\begin{array}
 &  &  X_{N-1} = 2 \cdot X_{N} - X_{N-1} + f(X_{N},t) \cdot h^{2}  \\
\iff & x_{t+1} = 2\cdot x_{t} - x_{t-1} + f(x_{t})\cdot \Delta t^{2}
\end{array}
$$
en los códigos en donde se implementa, en el bloque de actualización del *frame* se tiene usualmente:
```py
aux = vertice.posicion

vertice.posicion = 2 * vertice.posicion - vertice.posicionPrevia + vertice.fuerza * delta_t * delta_t

vertice.posicionPrevia = aux

```

#### Variación: Velocity-Verlet

El método de Verlet tiene una variación que permite **obtener la velocidad** según la posición siguiente calculando ella primero, de la forma:
$$
x_{t+1} = x_{t} + v_{t} \cdot \Delta t + \frac{1}{2} \cdot f(X_{t}) \cdot \Delta t^{2}
$$
y luego para obtener la velocidad siguiente:
$$
v_{t+1} = v_{t} + \frac{f(x_{t}) + f(x_{t + 1})}{2} \cdot \Delta t
$$
En vez de ir guardando la posición actual y previa, se requiere guardar la *posición y velocidad actuales*.