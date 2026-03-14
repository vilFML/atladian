En computación gráfica se suelen usar lenguajes compilados (como C++), pero se va a usar el lenguaje interpretado Python, que es lo suficientemente rápido y eficiente. Esto pues las partes críticas de un programa, Python las hace en C.

## Estructuras de Datos
Python tiene naticamente ciertas estructuras de datos, o formas de almacenar un conjunto de información:
- Listas
- Tuplas
- Conjuntos
- Diccionarios

# Modelo 3d
Un modelo 3D se compone de:
1. **Vértices**: Coordenadas en dónde se encuentra el punto en el espacio, entonces se relaciona con la forma $(x,y,z)$
2. **Arcos**: Depende de la implementación, pero típicamente Indica qué vertices se unen, de la forma $(v_{1},v_{2})$
3. **Caras**: También depende de la implementación, pero generalmente indica los vértices y arcos que la componen, como: $(v_{1},v_{2},v_{3}), (A_{1},A_{2},A_{3})$

Para generar movimiento se requiere *transformar* lo anterior, ej: cambiar las coordenadas de los vértices.

##### Ej
```py
L1 = [1, 2, 3]
L2 = [4, 5, 6]

L3 = L1 + L2 # La 'suma' concatena las listas

```
la suma, en realidad, concatena las listas, comportamiento que también se tiene en las tuplas. Además *no se pueden cambiar sus elementos* después de ser creadas.

# Estructuras de Datos para CG
1. Listas
2. Tuplas
3. Conjuntos
4. Diccionarios

## Conjuntos

```py
c1 = {1, 2, 3, 4}
c2 = {4, 5, 6, 7}
```

Al aplicar el operador + indica error pues conjuntos solo tiene unión e intersección. 
- Al hacer unión de conjuntos, al ser una definición algebraica, *estos no soportan repetición de elementos*
  \* Esto es útil para evitar redundancia en elementos

## Diccionarios
Útiles para mantener un registro de los elementos que componen el mundo.

Como ejemplo.
```py
diccionario1 = {'x':4, 'y':5, 'z':6}
diccionario2 = {'x':4, 'y':5, 'z':6}
```
teniendo un diccionario, se puede sumar definiendo en base a una iteración `for` para cada uno de sus elementos:
```py
diccionario1 = {'x':1, 'y':2, 'z':3}
diccionario2 = {'x':4, 'y':5, 'z':6}

suma = { key: diccionario1[key] + diccionario2[key] for key in 'xyz' }
# es lo mismo que
suma = {key: d1[key] + d2[key] for key in ['x', 'y', 'z']}
```

en donde `key` se refiere a los 'nombres'. Luego `suma` es un diccionario que almacena la suma de *los valores* de las *llaves*, en donde se itera en cada llave $x,y,z$ de los diccionarios.

### Uso en CG
Se puede usar la forma de indexar de los diccionarios como para almacenar la posición, el modelo (lista de vértices), color (lista RGB), etc. de un modelo:

```py


DiccionarioPersonaje1 = {'pos':{'x':30, 'y':20, 'z':0}, 'modelo': [v1,v2,v3,...], 'color': [100, 70, 30], 'material':'opaco'}


DiccionarioMundo = {'modelo1':[...], 'ḿodelo2':{...}}
```
Con diccionarios se puede almacenar información de las propiedades acerca de un modelo del mundo.

# Ecosistema de Python

## SciPy


## NetworkX
Para manejar estructuras de datos en GrafosSe va a utilizar NumPy, SciPy, NetworkX

## Numpy
Biblioteca numérica, arreglos, matrices, operaciones matemáticas

### Arrays (Arreglos)
Los arrays o arreglos son similares a las listas, pero tienen propiedades diferentes:
1. Los elementos dentro de un array **deben ser del mismo tipo de dato.** Hay casos en donde transforma los tipos de datos a uno en particular para que sean todos del mismo tipo.
2. Se pueden sumar los elementos directamente con los operadores matemáticos.
3. Los arrays son multidimensionales, así *se pueden tener vectores, matrices o tablas.*

EJ:
```py
M1 = np.matrix([[1, 0, 0], [0, 1, 0], [0, 0, 1]] )

```



# APIs Gráficas

Las APIs ofrecen operaciones para instrucciones que realizará la GPU

## OpenGL
Es una *especificación* de API para generar gráficos en la GPU. El propósito es *abstraer* la generación de modelos 3D.
Nuevas implementaciones de operaciones en GPU que cumplan las especificaciones de OpenGL es una implementación de OpenGL, por ejemplo, en linux existe 'Mesa 3D'

> Una implementación de OpenGL solamente se encarga de la generación de gráficos, o sea solamente mostrar en pantalla. Lo demás se realiza de forma externa

# Shader Programs
Un modelo no necesariamente se ve solo de 1 color, si no que puede tener sombras. 

La apariencia visual de los modelos se calcula y determina con los shaders.


# Pipeline Gráfico

Se tiene un modelo que:
1. Se discretiza en pixeles
2. Se pintan los pixeles