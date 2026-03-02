Los datos de tipo lógico (Boolean o Bool) son aquellos que sólo pueden tener uno de dos posibles valores: `True` o `False`.

Estos valores representan la verdad lógica en computación y se utilizan principalmente en **operaciones de comparación**:

| Expresión | Significado                    | Ejemplo  | Resultado |
| --------- | ------------------------------ | -------- | --------- |
| `x < y`   | ¿Es $x$ menor que $y$?         | `5 < 2`  | `False`   |
| `x <= y`  | ¿Es $x$ menor o igual que $y?$ | `2 <= 5` | `True`    |


## Comparaciones
### Numérica

### Con strings
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

## Operadores o Conectores Lógicos
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
