
| Tipo de dato | Descripción                            | Ejemplo        |
| ------------ | -------------------------------------- | -------------- |
| int          | Números **enteros** (sin decimal)      | 1, -7, 0       |
| float        | Números reales (con decimales)         | 1.0, -9.2      |
| str          | Cadenas de texto                       | "Hola", 'Hola' |
| bool         | Dos posibles valores: `true` o `false` |                |

## De tipo Lógico (Boolean)
Los datos de tipo lógico (Boolean o Bool) son aquellos que sólo pueden tener uno de dos posibles valores: `True` o `False`.

Estos valores representan la verdad lógica en computación y se utilizan principalmente en **operaciones de comparación**:

| Expresión | Significado                    | Ejemplo  | Resultado |
| --------- | ------------------------------ | -------- | --------- |
| `x < y`   | ¿Es $x$ menor que $y$?         | `5 < 2`  | `False`   |
| `x <= y`  | ¿Es $x$ menor o igual que $y?$ | `2 <= 5` | `True`    |


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
