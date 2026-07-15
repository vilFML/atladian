Al usar módulos se están encapsulando funciones, variables e instrucciones para resolver un determinado problema. El módulo se puede **reutilizar** en otros programas.
Hay módulos que vienen disponibles para usar con python o se pueden crear módulos personales.

Para agregar un módulo a un programa se usa la palabra reservada `import`.

\* Listado de funciones siempre disponibles: [[Funciones en Python]]

# Uso de Módulos
## Agregar Módulo

Suponiendo que se quieren usar las funciones `randint()` y `uniform()` del módulo `random`:
1. Se debe importar el módulo usando `import` seguido del nómbre del módulo: `random`, quedando la línea como `import 'modulo'`
2. Para hacer uso de una función del módulo se debe indicar la función precedida por el nombre del módulo de donde viene, separados por un `.`, osea `modulo.funcion()`
```py
import random # importar el módulo al programa actual

# uso de funciones del modulo incluido+
n1 = random.randint(1, 2)
n2 = random.uniform(3 ,4)
```

### Dar alias a módulo
Como se debe escribir el nombre del módulo en cada implementación de sus funciones, se puede abreviar el nombre del módulo dándole un alias con la palabra `as` seguida del alias deseado, de la forma `import 'módulo' as 'alias'`
Al tener un alias en un módulo sólo se requiere indicar el alias y no el nombre completo al utilizar una función.
##### Ejemplo
```py
# import el módulo y se nombra 'r'
import random as r

# uso de funciones con alias del modulo
n1 = r.randint(1, 2)
n2 = r.uniform(3 ,4)
```

### Importar ciertas funciones de un modulo
Si se desean utilizar solo ciertas funciones de un módulo, se indica de qué modulo provienen con `from 'modulo'` seguido de las funciones que se agregan con `import 'funcion1', 'funcion2'` (se indica el nombre de las funciones separadas por coma `,`).
\* En este caso se pueden utilizar las funciones sin necesidad de anteponer el nombre del módulo.
##### Ejemplo
```py
# Importar solo las funciones randint y uniform del modulo random
from random import randint, uniform

# Uso de funciones
n1 = randint(1, 2)
n2 = uniform(3 ,4)
```



#### Importar funciones sin anteponer modulo
Es posible importar todas las funciones de un módulo e implementarlas en el programa sin necesidad de indicar a qué modulo pertenecen si se indican las funciones a agregar del módulo como un asterisco  `*`
##### Ejemplo
```py
# Se importan todas las funciones del modulo random
from random import *

# Uso de funciones
n1 = randint(1, 2)
n2 = uniform(3, 4)
```


# Módulos Preinstalados
Son módulos que vienen con una instalación de python, pero que para utilizar las funciones en cada módulo se deben incluir los módulos.
## Módulo math

El módulo `math` de Python ofrece funciones relacionadas con matemáticas:

| Función         | Significado  | Ejemplo             | Resultado   |
| --------------- | ------------ | ------------------- | ----------- |
| `math.sqrt(x)`  | $\sqrt{ x }$ | `math.sqrt(4)`      | `2.0`       |
| `math.pow(x,y)` | $x^{y}$      | `math.pow(4, 0.5)`  | `2.0`       |
| `math.exp(x)`   | $e^{ x }$    | `math.exp(1)`       | `2.7182...` |
| `math.log(x)`   | $\ln (x)$    | `math.log(math.e)`  | `1.0`       |
| `math.sin(x)`   | $\sin(x)$    | `math.sin(math.pi)` | `0.0`       |
| `math.cos(x)`   | $\cos(x)$    | `math.cos(math.pi)` | `-1.0`      |
| `math.tan(x)`   | $\tan(x)$    | `math.tan(math.pi)` | `0.0`       |
| `math.asin(x)`  | $\arcsin(x)$ | `math.asin(0)`      | `3.1415...` |
|                 |              |                     |             |
también trae constantes matemáticas:

| Constante  | Significado  | Valor          |
| ---------- | ------------ | -------------- |
| `math.e`   | $e$          | `2.7182...`    |
| `math.inf` | $\infty$     | `inf`          |
| `math.nan` | not a number | `nan`          |
| `math.pi`  | $\pi$        | `3.1415592...` |
## Módulo random
Es un módulo útil para implementar comportamientos aleatorios.

| Función               | Significado                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------- |
| `random.random()`     | Número `float` $N$ al azar en el intervalo $0,0 \leq x < 1,0$<br>\**no toma el valor 1,0* |
| `random.uniform(x,y)` | Número `float` $N$ al azar en el intervalo $x \leq N \leq y$                              |
| `random.randint(x,y)` | Número `int` $N$ al azar en el intervalo $x \leq N \leq y$                                |
###### Ejemplos:
1. `random.randint(0,1)` puede modelar el lanzamiento de una moneda, donde los valores `0` y `1` se asignan a cara o sello.
2. `random.randint(1,6)` puede modelar el lanzamiento de un dado.



# Módulos Propios
Para crear módulos se debe crear un archivo de extensión `.py` que contiene las definiciones de las funciones en su interior.
El módulo de las funciones que se desean agregar al programa **debe estar en la misma carpeta que el programa**.

##### Ejemplo
Se crea un módulo llamado *triángulo* que contiene:
1. Una función que calcula el perímetro de un ángulo.
2. Una función para calcular el área de un triángulo.

nombre de archivo: `triangulo.py`
```py
import math

# perimetro: num, num, num -> num
# calcula el perimetro de un triangulo de lados a, b y c
# ejemplo: perimetro(2,3,2) devuelve 7
def perimetro(a, b, c):
	return a + b + x

assert perimetro(2, 3, 2) == 7

#area: num, num, num -> num
# calcula el perimetro de un triangulo de lados a, b y c
# ejemplo: area (3,4,5) devuelve 6
def area(a, b, c):
	S = perimetro(a ,b, c) / 2
	return math.sqrt(S * (S - a) * (S - b) * (S - c))

assert area(3, 4 ,5) == 6

```

y para utilizar las funciones creadas, en un programa llamado `programa.py`:
```py
import triangulo

print('Area y perimetro de un triangulo)

l1 = float(input('ingrese el largo del primer lado: ')
l2 = float(input('ingrese el largo del segundo lado: ')
l3 = float(input('ingrese el largo del tercer lado: ')

print('Perimetro =', triangulo.perimetro(l1,l2,l3))
print('Area =', triangulo.area(l1,l2,l3))

```
