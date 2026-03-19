La GPU solamente genera triángulos, entonces si se quiere, por ejemplo, hacer un cuadrado, se deben hacer dos triángulos.

# Pipeline Gráfico

### Vertex Shading
Se ejecuta por cada vértice

### Proyección


Para modificar la perspectiva de la geometría



## Shader
Primero se define la variable de entrada y al final se debe definir la variable de salida.

Para la entrada, se debe definir la posici


la variable gl_Position es obligatoria

## Vertex Shader

```C
#version 330

in vec3 position;
in vec3 color;

void main(){
	fragColor = color;
		gl_Position = vec4
}
```




## Fragment Shader
```C
#version 330

in vec3 fragColor;
out vec4 outColor;

void main()
{
	outColor = vec4 (fragColor, 1.0f);
}
```

# Colores y Transparencia

Se tienen tres modelos de color: RGB, CMY(K) y HSV

# P2
$C'=1-R$ es la cantidad de cuánta ausencia de rojo hay

