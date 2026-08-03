
| Tipo de dato | Descripción                            | Ejemplo        |
| ------------ | -------------------------------------- | -------------- |
| int          | Números **enteros** (sin decimal)      | 1, -7, 0       |
| float        | Números reales (con decimales)         | 1.0, -9.2      |
| str          | Cadenas de texto                       | "Hola", 'Hola' |
| bool         | Dos posibles valores: `true` o `false` |                |

## Datos numéricos
Python distingue entre números enteros (``int``) y números de punto flotante (``float``).

```python
n=5 # int
print(n, type(n))
x=3.14 # float
print(x, type(x))
```

    5 <class 'int'>
    3.14 <class 'float'>

Sobre estos datos se pueden ejecutar las operaciones aritméticas habituales.

```python
print(n+1)
print(n/2) # noten la diferencia con Python 2.7
print(n//2) # división entera
print(x**2)
```

    6
    2.5
    2
    9.8596

## Datos Lógicos (Boolean)
Los datos de tipo lógico (Boolean o Bool) son aquellos que sólo pueden tener uno de dos posibles valores: `True` o `False`.

Estos valores representan la verdad lógica en computación y se utilizan principalmente en **operaciones de comparación**:

| Expresión | Significado                    | Ejemplo  | Resultado |
| --------- | ------------------------------ | -------- | --------- |
| `x < y`   | ¿Es $x$ menor que $y$?         | `5 < 2`  | `False`   |
| `x <= y`  | ¿Es $x$ menor o igual que $y?$ | `2 <= 5` | `True`    |

### Comparaciones
#### Numérica

#### Con strings
Cuando se comparan textos, se usa la comparación lexicográfica o de diccionario, en donde cada carácter adquiere un valor de acuerdo con su posición en la tabla Unicode.
Se cumple que A < Z < a < z.

##### Ejemplo
```py
x = 'gatito'
y = 'perrito'
z = 'gatito'

print('Resultado de z == y: ', z == y)
print('Resultado de z == x: ', z == x)
print('Resultado de z > y: ', z > y)

```

### Operadores o Conectores Lógicos

Las operaciones lógicas se indican con palabras en lugar de símbolos.

```python
t=True
f=False
print(t and f)
print(t and not f)
print(n>0)
```

    False
    True
    True


Permiten operar expresiones lógicas entre sí usando las reglas de la lógica proposicional. Con los conectores lógicos se pueden crear *condiciones compuestas* de múltiples criterios que deben cumplirse.

| Conector  | Interpretación                                                                                          |
| --------- | ------------------------------------------------------------------------------------------------------- |
| `X and y` | Se evalúa a `True` si es que tanto `x` como `y` son `True`. `False` en cualquier otro caso.             |
| `x or y`  | Se evalúa a `True` si al menos `x` o `y` es `True`. Si ambos son `False`, entonces se evalúa a `False`. |
| `not x`   | Niega el valor de verdad de la expresión `x`.                                                           |

Para expresiones con múltiples operadores, se tiene un orden de prioridades.

| Prioridad | Operador                                            | Signo                            |
| --------- | --------------------------------------------------- | -------------------------------- |
| Mayor     | Exponenciación                                      | `**`                             |
|           | Operadores positivo y negativo                      | `+x`, `-x`                       |
|           | Multiplicación, División, División Entera y Módulo. | `*`, `/`, `//`, `%`              |
|           | Adición y Substracción                              | `+`, `-`                         |
|           | Comparadores booleanos                              | `==`, `!=`, `<`, `<=`, `>`, `>=` |
|           | Booleano *Not*                                      | `not`                            |
|           | Booleano *and*                                      | `and`                            |
| Menor     | Booleano *or*                                       | `or`                             |

##### Ejemplo: Conectores Booleanos:
```py
x = 5
y = 5
z = 7

print('Resultado de x == y and y < z: ', x == y and y < 5)

z = 4
print('Resultado de x == y and y < z: ', x == y and y < z)

print('Resultado de x == y or y < z', x == y or y < z)

```

1. La primera expresión es cierta debido a que ambas expresiones son ciertas.
2. La expresión en el segundo paso es falso debido a que 5 no es menor que 4 por redefinicion de z
3. Sin embargo, la expresión con `or` es cierta, ya que basta con que **una** expresión sea cierta.

## Strings
Los strings se escriben entre comillas simples o dobles, y existen muchas operaciones definidas para ellos.

```python
h="Hola"
print(h)
print(len(h))
m='mundo'
print(h + " " + m)
print(h.upper())
```

    Hola
    4
    Hola mundo
    HOLA

# Listas
Una lista es una secuencia de datos, posiblemente de distintos tipos, de largo variable.
```python
L=[3,2,1]
print(L)
L.append(0)
print(L)
x=L.pop()
print(L)
print(x)
```

    [3, 2, 1]
    [3, 2, 1, 0]
    [3, 2, 1]
    0

Los elementos de la lista se indexan partiendo desde cero.

```python
print(L[0])
print(L[2])
print(L[-1]) # contando desde el extremo derecho
```

    3
    1
    1

## Funciones

### Construir una lista
Una lista se puede construir como una declaración, indicando los elementos que tendrá en sus respectivas posiciones:
```py
Lista = [50,4.5,'gato']
```

también se puede construir en base a iterar una fórmula, para ir 'rellenando' los espacios con los resultados que se obtienen:
```py
C = [n**2 for n in range(1,7)]
```
    [1, 4, 9, 16, 25, 36]

### Agregar elementos
Se puede agregar un elemento *después del último elemento* con la función `'Lista'.append()`

### Extraer elementos
Con la función `'Lista'.pop()` se puede acceder a un elemento de la lista y, además, extraerlo de ella. 
- Por defecto se realiza al último elemento.

### Acceso a los Elementos
Se puede acceder a los elementos en una lista indicando su posición en ella, de la forma: `Lista[n]`, en donde se accede al dato en la n-ésima posición.
La primera posición en una lista es de posición `0`, o sea: `Lista[0]` corresponde al primer elemento en la lista.
- También se puede comenzar contando las posiciones desde el final de la lista, si se indica un número negativo, `Lista[-1]` es el último elemento de la lista.

También se puede recorrer la lista a través de una iteración en su subíndices:
```py

Lista = [5000,75.34,'perro']

for i in range(0,len(Lista)):
	print(Lista[i])
```

O bien, iterando *sobre los elementos* en la lista con la función `for`:
```py
Lista = [5000,75.34,'perro']

for l in L:
	print(l)
```


# Convertir entre tipos de datos
Funciones para convertir entre tipos de datos:
\*poner dato a convertir dentro de paréntesis.

1. Convertir a int: `int()`
2. Convertir a float: `float()`
3. Convertir a string: `str()`

*ejemplo:*
```py
int(2.7)
```

```py
float(7)
```

```py
str(11)
```

```py
str(2.7)
```

también se pueden convertir cadenas de texto a números:
```py
>>> int('70')
70


>>> float('2.5')
2.5
```

Y se debe notar el tipo de dato que se busca almacenar:
```py
int('2.5')
```

```py
float('perro')
```
