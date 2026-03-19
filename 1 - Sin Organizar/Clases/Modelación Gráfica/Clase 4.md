Antes las tarjetas gráficas se encargaban de comunicar el computador con el monitor y de tener la imagen en su memoria.
Surgen distintos chips especializados y se tiene una falta de un estándar para ocupar las GPU.


1. Solo líneas
2. Sólidos con color
3. Texturas

En el año 1999 Nvidia produce la GeForce 256 a nivel de consumidor, que propone un estándar en arquitectura y también propone una definición de GPU como un procesador de chip único que integra:
1. Transformaciones
2. Iluminación
3. Configuración y recorte de triángulos (técnica de optimización que oculta los triángulos que no se están visualizando)
4. Un motor de graficación (Rendering)
5. Capacidad de procesar un mínimo de 10 millones de polígonos por segundo.

Definición moderna:
Co-procesador dedicado al procesamiento de gráficos u operaciones de coma flotante para aligerar la carga de trabajo de la CPU en aplicaciones como videojuegos o aplicaciones interactivas.
Con el tiempo, como las GPU se diseñaron para procesar una gran cantidad de datos de forma paralelo, se notó que las GPU servían para resolver *operaciones de coma flotante* (como el procesamiento necesario de datos masivamente para IA)

Una GPU puede ser discreta o integrada
1. Discreta: Tarjeta gráfica dedicada al procesamiento gráfico. Contiene múltiples núcleos y con su propia memoria especializada (VRAM)
2. Integrada: Chip de procesamiento que puede tener una parte dedicada para gráficos, y tienen acceso directo a la memoria RAM, así la memoria se comparte entre lo necesario para procesamiento gráfico.

# CPU vs GPU
Una CPU esta procesada para procesamiento general

GPU: Muchas más unidades de cómputo, pero a cambio menor control en cuanto a lo que sucede en cada módulo.

Si bien inicialmente se concebió como un apoyo a la CPU, se vio que pueden realizar muchas tareas en paralelo.

1. Vertex Shader: Realiza cálculos sobre los vértices de la escena
2. Geometry Shader: Opera sobre los elementos de la escena, generando vértices y primitivas (e.g: los triángulos).
3. Fragment Shader: Pinta la escena de acuerdo a al información de color.
4. Finalmente se pasa al frame-buffer (memoria) para luego mostrarlo en pantalla.

# OpenGL y Shaders
## OpenGL
Es una especificación que define una API para escribir aplicaciones que producen gráficos.
Funciona como una máquina lineal que procesa las distintas partes de la escena, o sea una máquina *de los estados* de la escena.

# Shaders


## Vertex- Shader
Se ejecuta en la etapa inicial del proceso y calcula la posición y atributos de cada vértice. Los atributos que se calculan son:
1. Color
2. Coordenadas de las texturas
3. Vector Normal

```c
vertex_shader = """
	#version 130
	in vec3 position;
	in vec color;
	
	out vec3 fragcolor;
	
	void main()
	{
	fragColor = color;
	gl_Position== vec4(position, 1.0f)
	}
```


gl_Positions: El único parámetro obligatorio que determina la posición final de un vértice.


## Fragment Shader
Se ejecuta después de la rasterización, en donde ya se está trabajando con pixeles. Este determina de qué color se deben 'pintar' cada pixel.


# Pipeline
Es la cadena de pasos necesarios para generar la imagen, se compone de la combinación de:
