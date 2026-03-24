OpenGL es una especie de lenguaje 'primitivo':
manejo explícito de orientación a objetos, manejo de variables, entonces openGL es una máquina de punteros.

# Shaders
Son programas que permite 
# Pipeline
Aplicación -> Vertex Shader -> Rastering -> Fragment Shader -> Pantalla

## Aplicación
Tiene el código y el archivo de una figura geométrica. Es básicamente programar
Y se hace e la CPU y los siguientes procesos son en GPU

## Vertex Shader
Se escribe en un lenguaje parecido a $C$, corresponde a los parámetros que recibe el programa: Son los datos que recibe:
```C
vertex_shader= """
	# version 130
	in vec3 position;
	in vec3 color;
```
parámetro de entrada, uno de posición y otro ed color

Parámetro de salida: La información que se enviará a la siguiente etapa (el fragment shader)

Proceso principal

`gl_Position` es la posición final del vértice en coodernadas de 4D, por ahora el 4o parámetro es 1.0
## Rastering
Proceso en donde se pasa del mundo continuo a lo discreto:  A los pixeles que van a representar la geometría.
También se encarga de realizar el cálculo de la *interpolación*.
- No se modifica por el usuario pues es hecho por la GPU.
- 
## Fragment Shader
Se hace el procesamietno de los pixeles, como el *coloreo*.

Parámetro de entrada: El color definido en el vertex shader
```C
fragment_shader = """
	#version 130
	in vec3 fragColor;
	
	out vec4 outColor;
	
```

## Pantalla
Proceso en donde se muestra

## Vertex Shaders
Calcula la posicón y los atributos de cada **vértice**, como:
- Color
- Coordenadas de textura
- Vector Normal

# OpenGL
## Vértices
vértices contienen los atributos como posición y color

$\text{Vert}\to [V_{0x},V_{0y},V_{0z},V_{1x},V_{1y},\dots]$

## Índices
Los índices indican cuáles vértices conforman cada triángulo.

$\text{IND}\to[0,1,2,0,2,3]$

```py
# definiendo datos para cada vertice
# posiciones colores
vertexData = [ -0.5, -0.5, 0.0, 1.0, 0.0, 0.0,
				0.5, -0.5, 0.0, 0.0, 1.0, 0.0,
				0.5, 0.5, 0.0, 0.0, 0.0, 1.0,
				-0.5, 0.5, 0.0, 1.0, 1.0, 1.0]

# es importante usar datos de 32bits
vertexData = np.array(vertexData, dtype = np.float32)
# definir conexiones entre vértices.
# Se tiene un triangulo por cada 3 índices seguidos.
índices = np.array(
[0, 1, 2,
2, 3, 0], dtype = np.uint32)

```
en donde se dice que con $[0,1,2,$ se forma un triángulo y en $2,3,0]$ se forma otro.

## Estructura de Datos

## Vertex Buffer Object VBO
Almacena los datos asociados a los vértices.
 $\text{VBO}\to[V_{1x},V_{1y},V_{1z},V_{2x},\dots]$
## EBO
Son los índices de los elementos en VBO que formam las primitivas gráficas.
Sigue la misma idea que *las triadas de datos forman triángulos*.

## VAO
Asociación intermedia que le permite a openGL interpretar la información.

# Objetos 3D
Al trabajar con modelos 3D, no se implementan en código sino que se trabajan con aplicaciones como *blender*.
Se va a usar **trimesh**


## Formato .OBJ
Es uno de los más simples y tiene:
- v: Coordenadas de los vértices
- vt: Coor de texturas
- vn: vectores normales
- f: Triángulos

## Workflow
Pyglet permite abstraer el proceso ya que
*Trimesh* se encarga de cargar y preparar los datos en un formato adecuado para openGL. En específico, se tiene la lista de $v.vt, etc.$ y lo pasa al formato de openGL
y *Pyglet* se encarga de gestionar y graficar dichos datos.

1. función `load()` se entrega el modelo
2. función `rendering.mesh_to_vertexlist()` entrega la información de la malla entregada en formato.
3. 