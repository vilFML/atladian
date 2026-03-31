Materia: Mod. Gráficas
	Fecha cátedra: 31/03/26
	Fecha digitalización: 31/03/26
	*tags:* 

# Rendering Pipeline

1. Aplicación
2. Vertex Processing
3. Rasterización
4. Procesamiento de color (o píxeles)

La etapa de aplicación sucede en la CPU y la GPU se encarga desde la segunda etapa (pues es mejor para hacer procesamiento en paralelo).

La etapa de aplicación determina la matemática detrás de la escena. Ubica cierto vértice en cierto punto y el resto se encarga de las operaciones para mostrarlo en pantalla.
## Aplicación

En esta etapa se tiene mayor control del programa, pues se ejecuta principalmente el código que se escribe, y usualmente se ejecuta en la CPU.

- Tiene objetos geométricos que se llaman modelos 3D o 2D
- **Cámara y Escena**: Los modelos se posicionan y orientan, y hay una *cámara que los observa*; se visualiza cierta parte de la escena, se puede configurar el punto de vista con la que se observa el mundo virtual
- **Propiedades**: Los objetos tienen propiedades como sus colores, cómo interactuan con fuentes de luz y también propiedades materiales (es opaco, es brillante, etc)
Por lo tanto, dependiendo de dónde se posiciona la cámara, se tiene una 'foto' de cierto momento en la escena. Y con el efecto de cambiar la imagen a cierta frecuencia se tiene un 'video'.

Las primitivas gráficas son los triángulos. Para los cuadrados se dice que no tienen buenas propiedades, pues los triángulos:
* Pueden aproximar cualquier superficie
* Tienen una normal *bien definida*, o sea siempre son planares. Esto es, si se toma un triángulo, sus vértices siempre viven en el mismo plano, luego, obtener el vector normal del triángulo es simple.
* Todo se convierte en triángulos.
\* En los cuadrados no siempre se tiene la misma orientación para todas sus caras (ej. un cuadrado que se dobla por al medio).


## Vertex Processing

Tiene un sub-pipeline:
1. Vertex Shading: Se encarga de transfroamar (*view transform*) y busca llevar al mundo a un sist. de coordenadas estándar.
2. Proyección: El posicionamiento de la cámara; Se tiene una escena y se quiere simular que se posicoina la cámara en cierto punto de visto. Se encarga de realizar ciertas transformaciones geométricas de forma que posiciona el mundo para que se vea desde cierta perspectiva.
3. Clipping: Ahorra recursos al no convertir toda la escena en píxeles, si no que solamente los píxeles de los elementos que se observan según la perspectiva.
4. Screen Mapping (Mapeo): Desde que se tiene el punto de vista, se hace una 'transformación' a la resolución de la pantalla que se este usando.
Finalmente, se pasa todo a la etapa de *Rastering*.

### Proyección

Se simulan las distintas proyecciones para los elementos, las perspectiva 'humana' es solo una de ellas. Por ej:
- Frontal.
- Elevación oblicua
- Isométrica
- Perspectiva de un punto
etc.

Lo que hace es convertir el espacio visible en un **volumen de visualización**

### Clipping

Luego del volumen de visualización, se van a tener elementos fuera del punto de vista: Completamente, parcialmente visibles o totalmente fuera.
Luego, **ignora** los elementos que no se ven, y se procesan solamente los elementos que se van a ver.

Se cortan los elementos y lo que queda adentro se recalcula para que, si algo se corta, sea consistente (se rellena, se agrega un vértice, etc).

### Screen Map

Lo que sobrevive al clipping, convierte las coordenadas de los vértices desde el volumen de vista hacia las coordenadas necesarias para la resolución de la pantalla o ventana.
A cada vértice le asigna una coordenada en un símil a un 'plano cartesiano' para la resolución buscada.

## Rasterización

Es un proceso generalmente automático (no se puede intervenir), en donde se convierten las primitivas gráficas a píxeles.

¿Cómo determinar si un píxel es cubierto por un triángulo? 
Algunos procesos se hacen de forma que, dependiendo del porcentaje del píxel que esté cubierto: e.g si se cubre el 50% entonces se colorea el 50% (50% opaco), esto es costoso.
Como se está graficando en 3D, hay muchas combinaciones para un solo píxel (si se intersecta con otro triángulo, de otro color, etc.). Luego, el problema no es sencillo y hay varios métodos:


### Sampling

Se pinta si el objeto contiene al píxel y no pintarlo en cualquier otro caso. Básicamente, se considera el punto central del píxel y se determina qué triángulo lo contiene. Si hay una mezcla se hace un promedio o promedio ponderado.
   - El super sampling toma más muestras de píxeles.
Eventualmente, se tienen los casos borde, en esos casos se usa la regla **top-left**:




**Corolario 1**: Un píxel cubeirto por una arista inferior o derecha, no se considera.

**Corolario 2**: 



**OpenGL** implementa este renderizado. DirectX implementa la regla contraria.

#### Aliasing

Con el sampling se tiene una distorsión cuando una línea se ve como una escalera 

Una forma de arreglarlo es agregar más resolución (mayor cantidad de triángulos), pero esto es costoso al agregar muchos.

También se puede agregar el supersampling, en donde se toma (en vez de un punto) se muestrean más puntos y el color final es el promedio de los colores que se detectan para los puntos

![[Pasted image 20260331093739.png]]

. Esto permite tener una mayor precisión pues puede ser más representativo del color que debería tomar el píxel.
![[Pasted image 20260331093706.png]]
luego, la parte 'escalonada' se vé mas suave o difuminada.

## Pixel Processing

Ya se tiene la información del elemento: color, textura, material, etc. Y falta decidir el color que le corresponde a cada píxel. Se usa la interpolación con coordenadas baricéntricas, en donde si un píxel se encuentra más cerca de un vértice de un cierto color, este tendrá preponderancia en la contribución del color.

![[Pasted image 20260331094530.png]]




## Conclusiones

El rendering depende del motor gráfico que se utilice como el Unreal Engine.

Usualmente se usa un método denominado **Skinning**: Toma un esqueleto de un modelo en una pose de referencia y se modifican sus vértices de acuerdo a la animación, además a este se le agregan texturas, colores, etc.